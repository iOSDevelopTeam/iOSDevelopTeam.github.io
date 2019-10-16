---
layout:     post
title:      知识星球
subtitle:   iOS基础知识实践(一)
date:       2019-10-16
author:     shavekevin
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 基础知识
---
###  1.#基础题#继承之后打印显示问题 
A 类 有方法 
```
- (id)printClass {return self;}
```
B 继承自A  实现
```
- (id)printClass {return [super printClass];}
```
在B初始化方法里打印以下结果是什么？为什么？
```
NSLog(@"%@",[self printClass]);
NSLog(@"%@",[super printClass]);
```
答：答案都是输出B类的对对象。
 这里主要考察的是OC中关于self和super的理解。 一般的我们都知道self是指向的调用这几个方法的这个类的本身。那么super呢。其实super是一个Magic Keyword，
它的本质是一个编译器标示符，和self都指向同一个消息接受者。他们的不同点在于super会告诉编译器，调用class这个方法的时候，要去父类的方法，而不是本类里的。
 当使用self调用方法的时候，会从当前类的方法列表中开始找，如果没有，就从父类再找；而当使用super的时候，则从父类的方法列表中开始找，然后调用父类的这个方法。
 这也就是为什么不推荐在init方法中使用点语法。如果想访问实例变量iVar应该使用下划线(_iVar) 而非点语法(self.ivar)
 
#### 总结:
1. 当我们在调用`[self class]`的时候，实际先调用的是`objc_msgSend`函数，第一个参数是当前`B`这个实例，然后在`B`类里面去找`-(Class)class;` 这个方法,如果没有就去父类(A)里面找,如果也没有那就到了基类NSObject类。而在runtime中对class方法的实现返回的是当前类本身。


2. 当我们在调用`[super class]`的时候，会被转换成`objc_msgSendSuper`函数，第一步先构造objc_super结构体，结构体第一个成员就是self，第二个成员就是
 `(id)class_getSuperclass(objc_getClass("B"))`实际上这个时候返回的是SKObjectObject 第二步是从A类中去找`-(Class)class;`
 没有，然后去NSObject中去找，最后内部是使用`objc_msgSend(objc_super receiver`, `@selector(class))`去调用。 这个时候的调用和`[self class ]`基本一样。所以结果返回仍然是`B`。


#### 参考链接：

[刨根问底Objective－C Runtime（1）－ Self & Super]( https://blog.csdn.net/u011344883/article/details/41512683)


### 2.#基础题#runloop和线程有什么关系？

  总的来说，RunLoop正如其名，loop表示一种循环，和run放在一起就表示一直运行着的循环。实际上，runloop和线程是紧密相连的。
  可以这样说runloop是为了线程而生，没有线程，它就没有存在的必要。run loops是线程的基础架构部分，cocoa和corefundation都提供了run loop对象
  方便配置和管理线程run loop。 每个线程，包括程序的主线程 多有与之相对应的run loop 对象。
  
#### runloop和线程的关系
 
  1.主线程的runloop默认是启动的。
  在iOS 的应用程序里面，程序启动后会有一个如下的main函数
  
```
 int main(int argc, char * argv[]) {
      @autoreleasepool {
          return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
      }
  }
```
  重点是这个UIApplicationMain()函数，这个方法会为main thread 设置一个NSRunLoop对象，这就解释了：为什么我们可以应用在无人操作的时候休息。需要它干活的时候又能马上响应。
 

   2.对于其他线程来说，runloop默认是没有启动的。如果你需要更多的线程交互则可以手动配置和启动。如果线程只是去执行长时间的已确定的任务则不需要。
 


   3.在任何一个cocoa程序的线程中，都可以通过下面的代码来获取当前线程的runloop
   ```NSRunLoop *currentLoop = [NSRunLoop currentRunLoop];```
   
#### 参考链接：
[Objective-C之run loop详解](https://blog.csdn.net/wzzvictory/article/details/9237973)

### 3.#基础题# NSTimer会不会产生循环引用？如果产生了怎么解决？

答：会产生循环引用。产生循环引用的链条是： 对象强引用`timer`  `timer` 强引用对象。。 并且runloop也引用了`timer`。 如果我们按照正常的像block一样解除循环引用的方法是行不通的。因为虽然对象对timer的引用为弱引用，但是timer对对象的引用却还是强引用。
解决方法：参考yykit中的YYWeakProxy。它的原理是：对象-> timer -> proxy(这里的proxy继承自NSProxy)-> (消息转发)target -> 对象。
这个时候target为弱引用。如果对象的引用计数为0了，那么target就会被置为nil。这样就打破循环引用了。

可参考链接：[YYKit--YYWeakProxy](https://juejin.im/post/5a30f86ef265da4325294b3b)

 还有一种解决方法是：在vc中使用视图将要消失的时候 停掉定时器 并且置为nil。（在停掉定时器的时候，runloop也被移除）
 还有另外一种方式是 不用target 使用block的初始化方式。 这种缺点是iOS10+并且由于是block所以要处理block循环引用的问题。(注意:这样写不保险，首先不能确定这里消失的时机 是否要停掉定时器.)
 
```
 if (@available(iOS 10.0, *)) {
        self.schemeTimer = [NSTimer timerWithTimeInterval:1.0f repeats:YES block:^(NSTimer * _Nonnull timer) {
        }];
    } else {
        // Fallback on earlier versions
    }
```

  
1. 如果NSTimer当前处于NSDefaultRunLoopMode中，此时界面上有滚动事件发生，则RunLoop会瞬间切换至UITrackingRunLoopMode模式。这意味着NSTimer会被暂停调用响应方法，直至滚动事件被处理完，当滚动事件被处理完后，RunLoop又会被瞬间切换至NSDefaultRunLoopMode模式，此时线程会查看该mode下是否有相应事件等待处理，有则继续，没有的话，runloop会进入休眠状态，直至被事件再次唤醒
 
2. 占位mode：NSRunLoopCommonModes，它包含以上两种mode，处于该mode下的事件会在两种mode下都有效。也即mode切换过程中不会中断事件的处理。

3. （如果想让NSTimer同时在两种mode下都有效，该怎么办呢？
 答：要么将该NSTimer单独添加至两种mode下，要么一次性加入两种mode下NSRunLoopCommonModes。
 
4. Mode应用场景：轮播时，如果想拖拽查看某一页时暂停定时器；上下滑动UITableView时，不影响分页滚动界面的自动滚动。
 
 正常情况下，轮播时，定时器会自动暂停等待，不需要额外的暂停操作，但是当拖拽事件结束后，会发现恢复自动滚动瞬间，滚动的比较快，影响体验；所以正确的做法是先invalidate & nil,拖拽结束后再重新创建NSTimer。
 
 
 
 ### 4.#基础题#  使用NSTimer有什么缺点？你还知道哪些可以实现定时器？
答：定时器的缺点：

 1. 精确度不够，由于定时器在一个runloop中被检测一次，所以在这一次的runloop中如果做了耗时的操作，当前runloop持续的时间超过了定时器的间隔时间，那么下次执行的时间就会被延后。这就导致了精度的问题。解决方法:可以在子线程处理数据，然后在主线程进行打印或者做其他与UI相关的处理。
 2. runloop模式的影响，由于runloop有在scrollview滑动的时候有另外一种模式 如果设置runloop模式的时候设置成default模式 那么在scrollview滚动的时候当前定时器会暂停执行。直到滑动结束runloop模式切换为default的时候才会恢复。
  3. 循环引用。具体原因见： https://t.zsxq.com/mEMZrfU  或者本文第三题
  
  实现方式：
 
通过以下三种方式也可以实现NSTimer `mach_absolute_time() ` `CADisplayLink` 以及GCD的`dispatch_source_t`

 1. 使用mach_absolute_time()来实现更高精度的定时器。iPhone上有这么一个均匀变化的东西来提供给我们作为时间参考，就是CPU的时钟周期数（ticks）。 通过mach_absolute_time()获取CPU已运行的tick数量。将tick数经过转换变成秒或者纳秒，从而实现时间的计算。见matchAbsoluteTime。  理论上来说这个是最精准的定时器->纳秒级别的定时器。
 
2. CADisplayLink是一个频率能达到屏幕刷新率的定时器类。iPhone屏幕刷新频率为60帧/秒，也就是说最小间隔可以达到1/60s。 所以一般来说这个设置的时候是以1s为基准的。CADisplayLink的使用也需要手动加到runloop中，使用的时候仍然需要注意循环引用。
    
3. GCD实现使用了dispatch_source_t 来实现，使用的时候注意要创建、配置、开启timer。由于这里调用的时候用的是block 所以要注意block产生的循环引用问题。


#### CADisplayLink 和NSTimer 的不同之处：

 1. 原理不同 CADisplayLink以特定模式注册到runloop后，每当屏幕显示内容刷新结束的时候，runloop就会向CADisplayLink指定的target发送一次指定的selector消息， CADisplayLink类对应的selector就会被调用一次。
 NSTimer以指定的模式注册到runloop后，每当设定的周期时间到达后，runloop会向指定的target发送一次指定的selector消息。
 
 2. 精确度不同
  NSTimer的精确度就显得低了点，比如NSTimer的触发时间到的时候，runloop如果在忙于别的调用，触发时间就会推迟到下一个runloop周期。更有甚者，在OS X v10.9以后为了尽量避免在NSTimer触发时间到了而去中断当前处理的任务，NSTimer新增了tolerance属性，让用户可以设置可以容忍的触发的时间范围。
 
 3. 使用场合不同
 CADisplayLink使用场合相对专一，适合做界面的不停重绘，比如视频播放的时候需要不停地获取下一帧用于界面渲染。
 NSTimer的使用范围要广泛的多，各种需要单次或者循环定时处理的任务都可以使用。
 
 总结：一般来说NSTimer已经足够用，如果想要精度高一点的可以使用gcd的或者CADisplayLink，但是CADisplayLink 有限制。刷新频率根据系统的屏幕刷新频率，这也限制了使用的场景。mach_absolute_time 这个精确度更高一点一般用于计算函数的执行时间。
 
 参考链接：[NSTimer到底准不准?](https://blog.csdn.net/luolianxi/article/details/78618549)
 
 编辑/整理：小风
 
## 说明：

这是一个根据面试题总结的答案，并非全部原创。
[工程代码在这里](https://github.com/shaveKevin/iOSInterViewDemo) 
这里更新会落后于星球，星球内容存活时间为一年。星球收费是为了设置门槛，如果想要免费看最新的内容请联系微信：shavekevin001 邀请入星球。(加的时候请备注星球来的)
![WechatIMG7](https://tvax1.sinaimg.cn/large/a5a05ef3gy1g7ynnnga3zj20j60puq66.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。




