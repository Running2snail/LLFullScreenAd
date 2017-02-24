# LLFullScreenAd
快速添加全屏广告功能，仿网易新闻和蘑菇街全屏广告。
=
![](https://github.com/Running2snail/LLFullScreenAd/raw/master/FullScreenAdGif/fullScreenAd1.gif) 
![](https://github.com/Running2snail/LLFullScreenAd/raw/master/FullScreenAdGif/fullScreenAd2.gif) 
## 添加方式
在AppDelegate添加如下两个方法
 <a id="AppDelegate.m"></a>AppDelegate.m
```objc
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    self.window.backgroundColor = [UIColor whiteColor];
    self.window.rootViewController = [[ViewController alloc] init];
    [self.window makeKeyAndVisible];
    
    [self addADView];       // 添加广告图
    [self getADImageURL];
    return YES;
}

/** 添加广告图 */
- (void)addADView
{
    LLFullScreenAdView *adView = [[LLFullScreenAdView alloc] init];
    adView.tag = 100;
    adView.duration = 5;
    adView.waitTime = 5;
    adView.skipType = SkipButtonTypeCircleAnimationTest;
    adView.adImageTapBlock = ^(NSString *content) {
        NSLog(@"%@", content);
    };
    [self.window addSubview:adView];
}

/** 获取广告图URL */
- (void)getADImageURL
{
    // 此处推荐使用tag来获取adView，勿使用全局变量。因为在AppDelegate中将其设为全局变量时，不会被释放
    LLFullScreenAdView *adView = (LLFullScreenAdView *)[self.window viewWithTag:100];
    
    // 模拟从服务器上获取广告图URL
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(1 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
        
        NSString *urlString = @"http://s8.mogucdn.com/p2/170223/28n_4eb3la6b6b0h78c23d2kf65dj1a92_750x1334.jpg";
        
        [adView reloadAdImageWithUrl:urlString]; // 加载广告图（如果没有设置广告图设置为空）
    });
}

```
###有问题或者好的建议欢迎加入iOSQQ群共同探讨<br>
iOS-Ant-Bang互助社区 426981364<br>
iOS技术交流群 461069757 
