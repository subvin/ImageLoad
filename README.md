# ImageLoad


## iOS webp svg  和 gif 图片的加载

### 以下给出调研中得到的三个第三方图片加载库


|第三方库名|github 地址|可加载图片类型| star 数| fork 数| Commits |
|---|---|---|---|---|---|
| SDWebImage |[https://github.com/rs/SDWebImage](https://github.com/rs/SDWebImage)| png,jpg,gif 等 | 16963 | 4661 |目前 1241 次提交，更新频繁，最新跟新日期|
| FLAnimatedImage | [https://github.com/Flipboard/FLAnimatedImage](https://github.com/Flipboard/FLAnimatedImage) | gif |5354|830|目前 204 次提交，2015年 到 2016年2 月更新频繁，已许久没有更新。|
| PINRemoteImage | [https://github.com/pinterest/PINRemoteImage](https://github.com/pinterest/PINRemoteImage) | gif,webp | 2756 | 264 |目前 484 次提交，常常更新，最近一次更新 2017.2.23 。|
| YYWebImage |[https://github.com/ibireme/YYWebImage](https://github.com/ibireme/YYWebImage)| webp,gif 等 | 2610 | 473 |目前 104 次提交，更新频率低：最近一次提交 2016。10 23 日。|
|SVGKit|[https://github.com/SVGKit/SVGKit](https://github.com/SVGKit/SVGKit)|svg | 2598 | 586 |目前 704 次提交，每个月都有提交记录，较为频繁，最近一次更新 2017.2.16。|



### 用法

#### 1、FLAnimatedImage  

##### 1.1 导入安装 
将 FLAnimatedImage 和 FLAnimatedImageView 类放入工程即可使用，或者以Cocoapods 的形式进行引入 ：	pod 'FLAnimatedImage' 

##### 1.2 使用
	FLAnimatedImage *image = [FLAnimatedImage animatedImageWithGIFData:[NSData dataWithContentsOfURL:[NSURL URLWithString:@"https://upload.wikimedia.org/wikipedia/commons/2/2c/Rotating_earth_%28large%29.gif"]]];
	FLAnimatedImageView *imageView = [[FLAnimatedImageView alloc] init];
	imageView.animatedImage = image;
	imageView.frame = CGRectMake(0.0, 0.0, 100.0, 100.0);
	[self.view addSubview:imageView];
	

####2、	YYWebImage 

##### 2.1 cocoapods 导入    
在 Podfile 中添加 pod 'YYWebImage'。执行 pod install 或 pod update。注意：pod 配置并没有包含 WebP 组件, 如果你需要支持 WebP，可以在 Podfile 中添加 pod 'YYImage/WebP'。你可以调用 YYImageWebPAvailable() 来检查一下 WebP 组件是否被正确安装。


##### 2.2 手动安装

1. 下载 YYWebImage 文件夹内的所有内容。
2. 将 YYWebImage 内的源文件添加(拖放)到你的工程。
3. 链接以下 frameworks:
	* UIKit
	* CoreFoundation
	* QuartzCore
	* AssetsLibrary
	* ImageIO
	* Accelerate
	* MobileCoreServices
	* sqlite3
	* libz
4. 导入 `YYWebImage.h`。
5. 注意：如果你需要支持 WebP，可以将 `Vendor/WebP.framework`(静态库) 加入你的工程。你可以调用 `YYImageWebPAvailable()` 来检查一下 WebP 组件是否被正确安装。
	
##### 2.3 使用
	
加载本地图片：
	
	
		YYImage *image = [YYImage imageNamed:@"wall-e@2x.webp"];
    	YYAnimatedImageView *webpImageView = [[YYAnimatedImageView alloc] initWithFrame:CGRectMake(100, 30, 200, 200)];
		[webpImageView setImage:image];
		// 添加手势处理，可忽略
    	[YYImageExampleHelper addTapControlToAnimatedImageView:webpImageView];
    	[YYImageExampleHelper addPanControlToAnimatedImageView:webpImageView];
    	for (UIGestureRecognizer *g in webpImageView.gestureRecognizers) {
        	g.delegate = self;
    	}
    	[self.view addSubview:webpImageView];	
加载网络图片：

		YYImage *image = [YYImage imageNamed:@"wall-e@2x.webp"];
    	YYAnimatedImageView *webpImageView = 		[[YYAnimatedImageView alloc] initWithFrame:CGRectMake(100, 30, 200, 200)];
    	
    	//  用 SDWebImage  加载即可
		[GIFImageView sd_setImageWithURL:[NSURL URLWithString:@"http://img3.3lian.com/2006/013/08/20051103121441205.gif"] completed:^(UIImage *image, NSError *error, SDImageCacheType cacheType, NSURL *imageURL) {
    		}];
		// 添加手势处理，可忽略
    	[YYImageExampleHelper addTapControlToAnimatedImageView:webpImageView];
    	[YYImageExampleHelper addPanControlToAnimatedImageView:webpImageView];
    	for (UIGestureRecognizer *g in webpImageView.gestureRecognizers) {
        	g.delegate = self;
    	}
    	[self.view addSubview:webpImageView];



#### 	3、 PINRemoteImage 


##### 3.1 安装

该库是 FLAnimatedImage 库的一个补充，
Cocoapods ： pod 'PINRemoteImage' ，如要使用 WebP 图片 再添加 pod' PINRemoteImage/WebP' ,




##### 3.2 使用

下载并设置一张 WebP 图片：    
	
	UIImageView *imageView = [[UIImageView alloc] init];
	[imageView pin_setImageFromURL:[NSURL URLWithString:@"http://pinterest.com/kitten.jpg"]];


#### 	4、 SVGKit
##### 4.1 安装
下载 SVGKit 库，打开 SVGKit-iOS.xcodeproj 编译获取静态库，将静态库拖入工程，并添加依懒库，此时要注意和 SVGKit 配套的 Cococlumberjack 也应一并拖入工程，方可正常使用。暂时还不支持 Cocoapods 导入，不然会走很多弯路。具体导入过程详见 [https://github.com/SVGKit/SVGKit/blob/2.x/README.mdown](https://github.com/SVGKit/SVGKit/blob/2.x/README.mdown)

##### 4.2 使用

		NSString *svgName = @"1237.svg";
    	SVGKImage *svgImage = [SVGKImage imageNamed:svgName];
    	SVGKLayeredImageView *svgView = [[SVGKLayeredImageView alloc] initWithSVGKImage:svgImage];
    	svgView.backgroundColor = [UIColor clearColor];
    	svgView.frame = CGRectMake(10, 450, 0, 0);
    	[self.view addSubview:svgView];


