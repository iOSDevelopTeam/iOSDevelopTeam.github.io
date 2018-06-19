---
layout:     post
title:    逆向利器-dumpdecrypted
subtitle:  dumpdecrypted 破ipa包的壳
date:       2018-06-19
author:     BeyoundCong
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
- iOS
- 逆向
- dumpdecrypted
---
#### 安装 dumpdecrypted 

- 从 **APPStore** 商店下载安装的APP 默认都被苹果加了一层壳，加了壳后我们就无法使用dump导出头文件等其它操作，我们需要用工具 dumpdecrypted 砸了这个壳。

- [dumpdecrypted ](https://github.com/stefanesser/dumpdecrypted) 点击它去下载

- 下载后 cd 到 dumpdecrypted-master ，执行 make 命令

  如报错

  >xcrun: error: SDK "iphoneos" cannot be located

  查看 Makefile 的源码

  ``` 
  GCC_BIN=`xcrun --sdk iphoneos --find gcc`
  GCC_UNIVERSAL=$(GCC_BASE) -arch armv7 -arch armv7s -arch arm64
  SDK=`xcrun --sdk iphoneos --show-sdk-path`
  
  CFLAGS = 
  GCC_BASE = $(GCC_BIN) -Os $(CFLAGS) -Wimplicit -isysroot $(SDK) -F$(SDK)/System/Library/Frameworks -F$(SDK)/System/Library/PrivateFrameworks
  
  all: dumpdecrypted.dylib
  
  dumpdecrypted.dylib: dumpdecrypted.o 
  	$(GCC_UNIVERSAL) -dynamiclib -o $@ $^
  
  %.o: %.c
  	$(GCC_UNIVERSAL) -c -o $@ $< 
  
  clean:
  	rm -f *.o dumpdecrypted.dylib
  ```

  可以看到 第三行  `xcrun --sdk iphoneos --show-sdk-path`  发现是 Xcode 路径判断错了，需要给 Xcode 命令行工具指定路径

  > ```
  > sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer/
  > ```

   在 终端 再执行 下 `xcrun --sdk iphoneos --show-sdk-path`  如果出现跟下面的路径 就说明 OK！

  ``` 
  /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS11.3.sdk (版本是根据你安装的来显示的)
  ```

  最后执行  make  如果 dumpdecrypted-master 文件夹下出现了下面俩个文件就行了

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fsgjeytv4ej30yc0bejt1.jpg)

- iOS10 以上的系统，如果不对 .dylib 签名的话，砸壳会报这个错

  > dyld: could not load inserted library 'dumpdecrypted.dylib' because no suitable image found.  Did find:dumpdecrypted.dylib: required code signature missing for 'dumpdecrypted.dylib'

  我们要对 dumpdecrypted.dylib 进行签名

  ```
  ## 列出可签名证书
  security find-identity -v -p codesigning
  ## 为dumpecrypted.dylib签名
  codesign --force --verify --verbose --sign "iPhone Developer: xxx xxxx (xxxxxxxxxx)" dumpdecrypted.dylib
  ```

#### 对 ipa 进行砸壳

-  先定位 ipa 的位置并记录

  ```
  1, ssh root@设备的iP地址
  2, ps -e       （查看进程）
  3, cycript -p  （附加进程）
  4, [[NSFileManager defaultManager] URLsForDirectory:NSDocumentDirectory
                                            inDomains:NSUserDomainMask][0]
  ```

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fsgjvn2vppj31lk0psgzp.jpg)

- 通过 scp 拷贝 dumpdecrypted.dylib 到 App 的 Documents 的目录下

  ```
  scp dumpdecrypted.dylib root@10.8.172.13:/var/mobile/Containers/Data/Application/DF56C02A-3E71-43CD-A7CB-B31E7716F1C4/Documents/
  ```

  或者 通过 iFunBox 直接找到 Documents 然后把 dumpdecrypted.dylib 导入进去。

- 砸壳 里面用到的路径都是之前保存过的。

  ```
  1、cd /var/mobile/Containers/Data/Application/DF56C02A-3E71-43CD-A7CB-B31E7716F1C4/Documents/
  2、DYLD_INSERT_LIBRARIES=dumpdecrypted.dylib /var/containers/Bundle/Application/44506CE0-DC8F-4752-8339-D59909D96B42/iQiYiPhoneVideo.app/iQiYiPhoneVideo
  ```

- 验证是否成功

  看下 Documents 下是否有 XXXAPP.decrypted 文件（其实就是被破壳的文件）

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1fsgk4atak3j31bi0dujui.jpg)

#### 对破壳过的文件进行 class-dump 出头文件

- 用到的命令

- ```
  class-dump -H .decrypted路径  -o 保存头文件路径
  ```



感谢您的阅读，有什么问题请留言，作者看到会第一时间回复。



QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。
