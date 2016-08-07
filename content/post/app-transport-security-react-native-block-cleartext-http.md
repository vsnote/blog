+++
date = "2016-08-07T11:54:40+08:00"
title = "App Transport Security has blocked a cleartext HTTP"
url = "app-transport-security-react-native-block-cleartext-http.html"
+++

我有一个 React Native 项目，API 启用了 HTTPS，在本地 iOS simulator 上构建时报了这个错：

{{< highlight console >}}
2016-08-07 00:08:10.861 HotTweet[44115:1709324] App Transport Security has blocked a cleartext HTTP (http://) resource load since it is insecure. Temporary exceptions can be configured via your app's Info.plist file.
2016-08-07 00:08:10.871 HotTweet[44115:1708447] *** Assertion failure in -[RCTBatchedBridge loadSource:](), /Users/sam/myProjects/hotTweetApp/node_modules/react-native/React/Base/RCTBatchedBridge.m:180
2016-08-07 00:08:10.874 HotTweet[44115:1708447] *** Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'bundleURL must be non-nil when not implementing loadSourceForBridge'
*** First throw call stack:
(
	0   CoreFoundation                      0x00000001070c0d85 __exceptionPreprocess + 165
	1   libobjc.A.dylib                     0x0000000105f19deb objc_exception_throw + 48
	2   CoreFoundation                      0x00000001070c0bea +[NSException raise:format:arguments:] + 106
	3   Foundation                          0x0000000105b63e1e -[NSAssertionHandler handleFailureInFunction:file:lineNumber:description:] + 169
	4   HotTweet                            0x00000001057269fa -[RCTBatchedBridge loadSource:] + 746
	5   HotTweet                            0x000000010572504c -[RCTBatchedBridge start] + 332
	6   HotTweet                            0x0000000105724dd4 -[RCTBatchedBridge initWithParentBridge:] + 1124
	7   HotTweet                            0x000000010575f611 -[RCTBridge createBatchedBridge] + 65
	8   HotTweet                            0x000000010575f5b1 -[RCTBridge setUp] + 385
	9   HotTweet                            0x000000010575e874 -[RCTBridge initWithDelegate:bundleURL:moduleProvider:launchOptions:] + 516
	10  HotTweet                            0x000000010575e602 -[RCTBridge initWithBundleURL:moduleProvider:launchOptions:] + 146
	11  HotTweet                            0x00000001056cc3c7 -[RCTRootView initWithBundleURL:moduleName:initialProperties:launchOptions:] + 183
	12  HotTweet                            0x00000001056b37f5 -[AppDelegate application:didFinishLaunchingWithOptions:] + 245
	13  UIKit                               0x0000000108fb49ac -[UIApplication _handleDelegateCallbacksWithOptions:isSuspended:restoreState:] + 272
	14  UIKit                               0x0000000108fb5c0d -[UIApplication _callInitializationDelegatesForMainScene:transitionContext:] + 3415
	15  UIKit                               0x0000000108fbc568 -[UIApplication _runWithMainScene:transitionContext:completion:] + 1769
	16  UIKit                               0x0000000108fb9714 -[UIApplication workspaceDidEndTransaction:] + 188
	17  FrontBoardServices                  0x000000010be4b8c8 __FBSSERIALQUEUE_IS_CALLING_OUT_TO_A_BLOCK__ + 24
	18  FrontBoardServices                  0x000000010be4b741 -[FBSSerialQueue _performNext] + 178
	19  FrontBoardServices                  0x000000010be4baca -[FBSSerialQueue _performNextFromRunLoopSource] + 45
	20  CoreFoundation                      0x0000000106fe6301 __CFRUNLOOP_IS_CALLING_OUT_TO_A_SOURCE0_PERFORM_FUNCTION__ + 17
	21  CoreFoundation                      0x0000000106fdc22c __CFRunLoopDoSources0 + 556
	22  CoreFoundation                      0x0000000106fdb6e3 __CFRunLoopRun + 867
	23  CoreFoundation                      0x0000000106fdb0f8 CFRunLoopRunSpecific + 488
	24  UIKit                               0x0000000108fb8f21 -[UIApplication _run] + 402
	25  UIKit                               0x0000000108fbdf09 UIApplicationMain + 171
	26  HotTweet                            0x00000001056b3bcf main + 111
	27  libdyld.dylib                       0x000000010a69192d start + 1
)
libc++abi.dylib: terminating with uncaught exception of type NSException
(lldb) 
{{< /highlight >}}

这是 [iOS 9 加入的 App Transport Security](https://developer.apple.com/library/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 特性造成的 - 因为我们本地的 React Native 开发服务器未启用 HTTPS。

所以我们在开发时，需要打开 `Info.plist` 文件，把 `NSAllowsArbitraryLoads` 置为 `true`，而在构建发布版本里，将其置为 `false` - 除非你的 API 未启用 HTTPS。