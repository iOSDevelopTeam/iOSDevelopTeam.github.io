---
layout:     post
title:    Cycript
subtitle:   iOS逆向 Cycript 之修改微信钱包
date:       2018-06-17
author:     BeyoundCong
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
- iOS
- 逆向
- Cycript
---
#### Cycript介绍

- Cycript 是 Objective-C++、ES6（JavaScript）、Java 等语法的混合物。可以用来探索、修改、调试正在运行的 Mac\iOS APP。
- 官网： http://www.cycript.org/
- 文档： http://www.cycript.org/manual/
- 通过Cydia安装Cycript，即可在iPhone上调试运行中的APP。

#### Cycript安装以及用法

- 首先在 cydia 中搜索并安装

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fseanp1mjuj30av04iq31.jpg)

- 用法

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fseaprvmgyj30ot04v0tu.jpg)

  

- Cycript 开启和退出

  开启

  ```
  cycript
  cycript -p 进程ID
  cycript -p 进程名称
  ```

  退出

  ```
  取消输入：Ctrl + C
  退出：Ctrl + D
  清屏：Command + R
  ```

#### Cycript - 在桌面弹出提示框

- 先连接手机 USB转发端口 或者 ssh root@ip。

- 通过 ps -e 命令查看进程，找到 要调试的进程。

- 例如(在我的手机上找到):

  ```
  434 ??         1:24.53 /System/Library/CoreServices/SpringBoard.app/SpringBoard
  ```

  然后我们开启 Cycript 以下 2 种方式都可以

  ```
  cycript -p 434 进程ID
  cycript -p SpringBoard 进程名称
  ```

  推荐使用进程名称，因为这个名称一般是不会变的。

- 然后我们接着在上面写个弹框

  ```
  var alert = [[UIAlertView alloc] initWithTitle: @"hi!" message: @"hello word！" delegate: nil cancelButtonTitle: @"OK" otherButtonTitles: nil] 
  [alert show]
  ```

  如图所示

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fseb80crumj31gq048400.jpg)

- 作用在手机的效果图

  ![](http://ww1.sinaimg.cn/mw690/006hs9KEgy1fseb8slav5j30hs0vknk7.jpg)

  

#### Cycript 修改微信钱包

- 因为有些命令要经常用到，所以可以把它们封装成一个 .cy 文件

- 我们现在用到 MJ 封装好的一个文件 [mjcript.cy](https://github.com/CoderMJLee/mjcript)

  里面的代码

  ```
  (function(exports) {
  	var invalidParamStr = 'Invalid parameter';
  	var missingParamStr = 'Missing parameter';
  
  	// app id
  	MJAppId = [NSBundle mainBundle].bundleIdentifier;
  
  	// mainBundlePath
  	MJAppPath = [NSBundle mainBundle].bundlePath;
  
  	// document path
  	MJDocPath = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES)[0];
  
  	// caches path
  	MJCachesPath = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES)[0]; 
  
  	// 加载系统动态库
  	MJLoadFramework = function(name) {
  		var head = "/System/Library/";
  		var foot = "Frameworks/" + name + ".framework";
  		var bundle = [NSBundle bundleWithPath:head + foot] || [NSBundle bundleWithPath:head + "Private" + foot];
    		[bundle load];
    		return bundle;
  	};
  
  	// keyWindow
  	MJKeyWin = function() {
  		return UIApp.keyWindow;
  	};
  
  	// 根控制器
  	MJRootVc =  function() {
  		return UIApp.keyWindow.rootViewController;
  	};
  
  	// 找到显示在最前面的控制器
  	var _MJFrontVc = function(vc) {
  		if (vc.presentedViewController) {
          	return _MJFrontVc(vc.presentedViewController);
  	    }else if ([vc isKindOfClass:[UITabBarController class]]) {
  	        return _MJFrontVc(vc.selectedViewController);
  	    } else if ([vc isKindOfClass:[UINavigationController class]]) {
  	        return _MJFrontVc(vc.visibleViewController);
  	    } else {
  	    	var count = vc.childViewControllers.count;
      		for (var i = count - 1; i >= 0; i--) {
      			var childVc = vc.childViewControllers[i];
      			if (childVc && childVc.view.window) {
      				vc = _MJFrontVc(childVc);
      				break;
      			}
      		}
  	        return vc;
      	}
  	};
  
  	MJFrontVc =  function() {
  		return _MJFrontVc(UIApp.keyWindow.rootViewController);
  	};
  
  	// CG函数
  	MJPointMake = function(x, y) { 
  		return {0 : x, 1 : y}; 
  	};
  
  	MJSizeMake = function(w, h) { 
  		return {0 : w, 1 : h}; 
  	};
  
  	MJRectMake = function(x, y, w, h) { 
  		return {0 : MJPointMake(x, y), 1 : MJSizeMake(w, h)}; 
  	};
  
  	// 递归打印controller的层级结构
  	MJChildVcs = function(vc) {
  		if (![vc isKindOfClass:[UIViewController class]]) throw new Error(invalidParamStr);
  		return [vc _printHierarchy].toString();
  	};
  
  	// 递归打印view的层级结构
  	MJSubviews = function(view) { 
  		if (![view isKindOfClass:[UIView class]]) throw new Error(invalidParamStr);
  		return view.recursiveDescription().toString(); 
  	};
  
  	// 判断是否为字符串 "str" @"str"
  	MJIsString = function(str) {
  		return typeof str == 'string' || str instanceof String;
  	};
  
  	// 判断是否为数组 []、@[]
  	MJIsArray = function(arr) {
  		return arr instanceof Array;
  	};
  
  	// 判断是否为数字 666 @666
  	MJIsNumber = function(num) {
  		return typeof num == 'number' || num instanceof Number;
  	};
  
  	var _MJClass = function(className) {
  		if (!className) throw new Error(missingParamStr);
  		if (MJIsString(className)) {
  			return NSClassFromString(className);
  		} 
  		if (!className) throw new Error(invalidParamStr);
  		// 对象或者类
  		return className.class();
  	};
  
  	// 打印所有的子类
  	MJSubclasses = function(className, reg) {
  		className = _MJClass(className);
  
  		return [c for each (c in ObjectiveC.classes) 
  		if (c != className 
  			&& class_getSuperclass(c) 
  			&& [c isSubclassOfClass:className] 
  			&& (!reg || reg.test(c)))
  			];
  	};
  
  	// 打印所有的方法
  	var _MJGetMethods = function(className, reg, clazz) {
  		className = _MJClass(className);
  
  		var count = new new Type('I');
  		var classObj = clazz ? className.constructor : className;
  		var methodList = class_copyMethodList(classObj, count);
  		var methodsArray = [];
  		var methodNamesArray = [];
  		for(var i = 0; i < *count; i++) {
  			var method = methodList[i];
  			var selector = method_getName(method);
  			var name = sel_getName(selector);
  			if (reg && !reg.test(name)) continue;
  			methodsArray.push({
  				selector : selector, 
  				type : method_getTypeEncoding(method)
  			});
  			methodNamesArray.push(name);
  		}
  		free(methodList);
  		return [methodsArray, methodNamesArray];
  	};
  
  	var _MJMethods = function(className, reg, clazz) {
  		return _MJGetMethods(className, reg, clazz)[0];
  	};
  
  	// 打印所有的方法名字
  	var _MJMethodNames = function(className, reg, clazz) {
  		return _MJGetMethods(className, reg, clazz)[1];
  	};
  
  	// 打印所有的对象方法
  	MJInstanceMethods = function(className, reg) {
  		return _MJMethods(className, reg);
  	};
  
  	// 打印所有的对象方法名字
  	MJInstanceMethodNames = function(className, reg) {
  		return _MJMethodNames(className, reg);
  	};
  
  	// 打印所有的类方法
  	MJClassMethods = function(className, reg) {
  		return _MJMethods(className, reg, true);
  	};
  
  	// 打印所有的类方法名字
  	MJClassMethodNames = function(className, reg) {
  		return _MJMethodNames(className, reg, true);
  	};
  
  	// 打印所有的成员变量
  	MJIvars = function(obj, reg){ 
  		if (!obj) throw new Error(missingParamStr);
  		var x = {}; 
  		for(var i in *obj) { 
  			try { 
  				var value = (*obj)[i];
  				if (reg && !reg.test(i) && !reg.test(value)) continue;
  				x[i] = value; 
  			} catch(e){} 
  		} 
  		return x; 
  	};
  
  	// 打印所有的成员变量名字
  	MJIvarNames = function(obj, reg) {
  		if (!obj) throw new Error(missingParamStr);
  		var array = [];
  		for(var name in *obj) { 
  			if (reg && !reg.test(name)) continue;
  			array.push(name);
  		}
  		return array;
  	};
  })(exports);
  ```

- 通过 iFunBox 把 这个 .cy 文件先导入到 iPhone 的 `/usr/lib/cycript0.9` 中

- 先 `cycript -p WeChat `  开启 cycript

- 导入mjcript.cy 文件  `@import mjcript ` 

- 进入钱包页面 ，调用  `choose (UILabel) `  查找当前页面的所有 UILabel ，通过 commadn + F 来找 0.00（也就是你零钱下面的钱数）

  ```
  #"<MMUILabel: 0x11c4c6200; baseClass = UILabel; frame = (145.5 84.9048; 29 13); text = '\xc2\xa50.00';
  ```

- 修改这个 MMUILabel 的坐标以及 text

  ```
  #0x11c4c6200.frame = MJRectMake (0,84.9048,320,13)
  #0x11c4c6200.textAlignment = NSTextAlignmentCenter
  #0x11c4c6200.text = @"$666666666.66"
  ```

- 注意：这个只是修改的内存地址，如果退出再进来地址会改变，需要重新获取  MMUILabel 的内存地址！

- 成功的图片

  ![](http://ww1.sinaimg.cn/mw690/006hs9KEgy1fsebv85sbwj30hs0vkq4z.jpg)



####有问题请留言，作者看到第一时间会回复。



QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。



