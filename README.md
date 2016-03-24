# shareByOther
Get any great articles，and save

文章来源：http://www.cnblogs.com/yaann/p/5110236.html

C4－Cordova在iOS平台的使用

一、创建工程及运行
　　1、安装部署工具

　　　　ios-sim和ios-deploy工具，可以使你通过命令行在iOS模拟器和iOS设备上面启动app。

        $ npm install -g ios-sim
        $ npm install -g ios-deploy    
　　2、Create a New Project

        $ cordova create hello com.example.hello "HelloWorld"
        $ cd hello
        $ cordova platform add ios
        $ cordova prepare              # or "cordova build"    
　　3、部署运行app

　　　　部署在一个已经连接的iOS设备上：

        $ cordova run ios --device
　　　　部署在一个默认的iOS模拟器上：

        $ cordova emulate ios
二、config.xml详解
　　config.xml文件控制了app的一些基本设置信息。

　　1、EnableViewportScale (boolean类型, 默认是false): 设置为true，允许meta标签的视窗在用户限定的范围内缩放或者禁用。

        <preference name="EnableViewportScale" value="true"/>    
　　像如下的html一样来创建一个视窗，可以禁止缩放，可以在渲染的WebView里灵活缩放。

        <meta name='viewport' content='width=device-width, initial-scale=1, user-scalable=no' />
　　2、MediaPlaybackAllowsAirPlay (boolean类型, 默认是true): 设置false会阻止view对Air Play的支持。默认在UIWebView和WKWebView是可用的。

        <preference name="MediaPlaybackAllowsAirPlay" value="false"/>
　　3、MediaPlaybackRequiresUserAction (boolean类型, 默认是false): 设置true禁止HTML5上面的音视频响应自动播放属性的设置或者js代码的调用引起的自动播放事件。

        <preference name="MediaPlaybackRequiresUserAction" value="true"/>
　　4、AllowInlineMediaPlayback (boolean类型, 默认是false): 设置true允许HTML5内联媒体在屏幕范围内播放，通过浏览器支持控制而不是远胜控制。可以通过给任意<video>元素添加webkit-playsinline属性来实现。

        <preference name="AllowInlineMediaPlayback" value="true"/>
　　5、BackupWebStorage (string类型, 可以设置为none，local或者默认是cloud): 设置cloud允许备份数据到iCloud。设置local仅允许通过iTunes同步备份。设置none禁止备份。 

        <preference name="BackupWebStorage" value="local"/>
　　6、TopActivityIndicator (string类型, 默认是gray): 控制ActivityIndicator在状态栏的显示，可选的有whiteLarge, white, and gray。

        <preference name="TopActivityIndicator" value="white"/>    
　　7、KeyboardDisplayRequiresUserAction (boolean类型, 默认是true): 设置为false允许键盘响应inputs元素的调用。

        <preference name="KeyboardDisplayRequiresUserAction" value="false"/>
　　8、SuppressesIncrementalRendering (boolean类型, 默认是false): 设置true的话，元素渲染到屏幕前会等待所有的内容获取完全。

        <preference name="SuppressesIncrementalRendering" value="true"/>
　　9、GapBetweenPages (float类型, 默认是0): 表示页面间距。

        <preference name="GapBetweenPages" value="0"/>
　　10、PageLength (float类型, 默认是0): 在页面滚动方向上的页面长度。当页面滚动方式是由右到左或者由左到右的时候，这个属性代表的是每个页面的宽度。当页面滚动方式是由上到下或者由下到上的时候，这个属性代表的是每个页面的高度。默认值是0，意味着页面的尺寸有视图决定。

        <preference name="PageLength" value="0"/>
　　11、PaginationBreakingMode (string类型, 默认是page): 可选项有page和column。这个属性决定了CSS属性设置的column-和page-breaking是否能生效。此属性设置了column的时候，由CSS控制的页面元素内容就会由column-breaking替代page-breaking。

        <preference name="PaginationBreakingMode" value="page"/>    
　　12、PaginationMode (string类型, 默认是unpaginated): 可选项有unpaginated, leftToRight, topToBottom, bottomToTop, and rightToLeft。这个属性决定了webview的内容在充满视窗的时候是分页还是显示一个长的滑动的view。如果设置了分页格式，内容元素的分页会导致webview调用PageLength和GapBetweenPages的value去布局内容。

        <preference name="PaginationMode" value="unpaginated"/>
　　13、UIWebViewDecelerationSpeed (string类型, 默认是normal): 可选项有normal, fast。这个属性控制了滑动的减速度。默认的normal是最接近原生app效果的，而fast选项是针对移动端Safari的。

        <preference name="UIWebViewDecelerationSpeed" value="fast" />
　　14、ErrorUrl (string类型, 默认无设置): 如果设置了，在app里引用此本地页面文件会报错。

        <preference name="ErrorUrl" value="myErrorPage.html"/>
　　15、OverrideUserAgent (string类型, 默认无设置): 如果设置了，设置的值就会替代webview原来的UserAgent（用户代理），在确定获取远端页面的请求是由app发出的还是由浏览器发出的时候UserAgent是很有用的。使用警告，这可能导致服务兼容问题。大多数情况下，用AppendUserAgent代替。

        <preference name="OverrideUserAgent" value="Mozilla/5.0 My Browser" />
　　16、AppendUserAgent (string类型, 默认无设置): 如果设置了，设置的值就会加到webview原来的UserAgent后面。设置OverrideUserAgent的时候，此设置会被忽略。

        <preference name="AppendUserAgent" value="My Browser" />
　　17、target-device (string类型, 默认是universal): 可选项有handset, tablet, universal。此属性直接显示在Xcode工程的TARGETED_DEVICE_FAMILY上面。注意，如果你的target设置了universal，你提交应用的时候需要同时提供iPhone和iPad的截屏，否则可能被拒。

        <preference name="target-device" value="universal" />
　　18、deployment-target (string类型, 默认无设置): 设置了应用支持的iOS系统最低版本。详细信息可以查看苹果官方文档Deployment Target Settings

        <preference name="deployment-target" value="7.0" />
　　19、CordovaWebViewEngine (string类型, 默认是 'CDVUIWebViewEngine'): 设置WebView的引擎插件提供给本地的app，插件必须遵守CDVWebViewEngineProtocol协议。设置的value必须匹配已安装的WebView引擎插件在'feature'标签内的名字。此设置通常为自动设置安装。

        <preference name="CordovaWebViewEngine" value="CDVUIWebViewEngine" />
　　20、SuppressesLongPressGesture (boolean类型, 默认是false): 设置为true避免了iOS9+的长按webview显示一个放大镜控件的效果出现。测试你的应用程序，因为这可能影响文本选择的功能。

        <preference name="SuppressesLongPressGesture" value="true" />
　　21、Suppresses3DTouchGesture (boolean类型, 默认是false): 设置为true避免支持3D Touch的设备在用户用力长按webview的时候出现一个放大镜控件。请测试你的应用，因为这禁止了onclick操作，但是ontouchend依然生效。如果此设置为true，SuppressesLongPressGesture同样会被设置为true并有效。

        <preference name="Suppresses3DTouchGesture" value="true" />
　　22、CDVSystemSchemesOverride (string类型, 默认是 maps,tel,telprompt):  用逗号分隔的URL schemes列表里的URL是被允许进入系统的，而不是由科尔多瓦WebView本身。

        <preference name="CDVSystemSchemesOverride" value="maps,tel,telprompt" />
