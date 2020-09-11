# 代码编写

### 1. 基本编写原则
   #### 1.1. 命名要清晰
   - 不要过分追求简洁造成词义不清晰：  
      
      | 正确 | 错误 | 
      |------|------------|
      | insertObject:atIndex  | insertObject:at   |
      | removeObjectAtIndex:  | removeObjectAt:   |
      | removeObject:         | remove:       	|
   - 描述事物时候不要使用缩写单词，该清晰时还是要清晰
   	  
      | 正确 | 错误 | 
      |------|------------|
      | destinationSelection  | destSel   |
      | setBackgroundColor:  | setBkgdColor:   |
      
      通用的缩写：
      
      | 缩写 | 代表的意思 | 
      |------|------------|
      | alloc  | Allocate   |
      | alt  |Alternate   |
      | app  |Application   |
      | calc  |Calculate   |
      | dealloc  |Deallocate   |
      | func  |Function   |
      | horiz  |Horizontal   |
      | info  |Information   |
      | init  |Initialize   |
      | int  |Integer   |
      | max  |Maximum   |
      | min  |Minimum   |
      | msg  |Message   |
      | pboard  |Pasteboard   |
      | rect  |Rectangle   |
      | Rep  |Representation   |
      | temp  |Temporary   |
      | vert  |Vertical   |
 
#### 1.2. 加前缀

   - 类、协议
     ```
     1.最好以两个或者三个大写字母组成的前缀
     2.不能使用系统的前缀，例如：NS,AB,IB，UI等
     ```
   - 私有方法
     ```
     1.私有方法加前缀是为了避免系统的父类也同样存在相同的方法。
     2.前缀可以是公司或者项目名称组成缩写，或者p_
     3.不要用"_",以为系统默认会使用这个来命名私有方法
     ```
   - 分类
     ```
     1.分类的名称也应该加前缀，如：@interface NSString(HN_ADD)
     2.方法也要加，- (void)hn_addNumber;
     ```
    
### 2. 方法命名

#### 2.1. 基本原则
- 方法名以小写字母开头，包含的单词首个字母要大写
- 公共方法不要使用前缀（分类除外）,私有方法可以使用
- 描述某种事件或者动作的方法，以动词开头：

  ```
  - (void)invokeWithTarget:(id)target;
  - (void)selectTabViewItem:(NSTabViewItem *)tabViewItem;
  不要使用do，does,不要在动词前面使用副词或者形容词
  ```
- 如果方法返回某个对象的属性值，要采取以下写法

```
- (NSSize)cellSize;

```
- 所有方法参数前面必须使用关键词

| 正确 | 错误 | 
|------|------------|
| - (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag;  | - (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;  |

- 参数名称和参数关键词要一对一

| 正确 | 错误 | 
|------|------------|
| - (id)viewWithTag:(NSInteger)aTag;  | - (id)taggedView:(int)aTag;  |

- 当一个方法是对另一个方法的增加具体功能的参数时，要在旧的方法后面增加参数。

```
- (id)initWithFrame:(CGRect)frameRect;
- (id)initWithFrame:(NSRect)frameRect mode:(int)aMode cellClass:(Class)factoryId numberOfRows:(int)rowsHigh numberOfColumns:(int)colsWide;

```

- 方法中使用***and***关键词

```
1.不要使用and来连接参数
2.当方法描述两个独立的动作是可以使用and，如：
- (BOOL)openFile:(NSString *)fullPath withApplication:(NSString *)appName andDeactivate:(BOOL)flag;
```

#### 2.2. 访问器方法

- 名词属性
```
- (NSString *)title;
- (void)setTitle:(NSString *)aTitle;
```
- 形容词属性
```
- (BOOL)isAdjective;
- (void)setAdjective:(BOOL)flag;
```
- 动词属性
```
- (BOOL)showsAlpha;
- (void)setShowsAlpha:(BOOL)flag;
```

- 不要使用 do / does ,可以使用can,should,will,did...

```
- (void)setCanHide:(BOOL)flag;
- (BOOL)canHide;

- (void)setShouldCloseDocument:(BOOL)flag;
- (BOOL)shouldCloseDocument;
```

- 当间接返回多个值是才使用***get***,如：
```
///使用了inout,
- (void)getLineDash:(float *)pattern count:(int *)count phase:(float *)phase;
```


#### 2.3. 委托方法

- 方法的命名以调用代理方法的类名称开头，如：
```
- (BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(int)row;
```
- 使用did表示已经发生，will表示将要发生，should表示调用带有did,will的方法

```
- (void)browserDidScroll:(NSBrowser *)sender;
- (NSUndoManager *)windowWillReturnUndoManager:(NSWindow *)window;
- (BOOL)windowShouldClose:(id)sender;
```

#### 2.4. 表示集合的方法

- 通常都要提供成组的方法

```
- (void)addLayoutManager:(NSLayoutManager *)obj;
- (void)removeLayoutManager:(NSLayoutManager *)obj;
- (NSArray *)layoutManagers;
```

#### 2.5. 方法的参数

- 通常第一个参数的首个字母大写，其他参数以小写开头，其它的包含单词首个字母要大写,如：
```
- (void)scrollToRowAtIndexPath:(NSIndexPath *)indexPath atScrollPosition:(UITableViewScrollPosition)scrollPosition animated:(BOOL)animated;

```
- 不要使用几个字母的参数，或者缩写，保证参数清晰易懂

#### 2.6. 私有方法

- 使用"公司缩写(如：AY)"或者"项目缩写(如:HN)"或者"p_"前缀避免系统的父类使用了相同的方法
- 不要使用 "_"前缀，系统默认已经使用这个了

#### 2.6. 公有方法
- 分类的方法需要加前缀，避免方法覆盖和重复

#### 2.7. 构造方法
- 初始化方法必须有一个总方法能够包含所有初始化方法的实现功能。
- 便利初始化方法通过调用总初始化的方法实现功能

如：
```
- (instancetype)initWithSessionConfiguration:(NSURLSessionConfiguration *)configuration {
    return [self initWithBaseURL:nil sessionConfiguration:configuration];
}

- (instancetype)initWithBaseURL:(NSURL *)url
           sessionConfiguration:(NSURLSessionConfiguration *)configuration
{
}
```
- 使用NS_DESIGNATED_INITIALIZER，指定初始化方法
```
- (instancetype)initWithBaseURL:(NSURL *)url
           sessionConfiguration:(NSURLSessionConfiguration *)configuration NS_DESIGNATED_INITIALIZER;
```
#### 2.8. initialize 和load 方法

 - load方法是在runtime初始化之后的，所以一般做runtime的操作，例如MethodSwizzing,
 - initialize方法要注意不要在分类上重写，因为分类会覆盖原类的方法，这个方法一般用来初始化变量，另外要注意子类重新这个方法，父类的initialize会调两次，要做好判断

#### 2.9. 多线程方法使用
 - GCD使用队列最好自己创建,这样会有队列名称，方便调试
```
dispatch_queue_create(<#const char * _Nullable label#>, <#dispatch_queue_attr_t  _Nullable attr#>)
```
- GCD block要注意野指针问题


### 3. C 函数

- c 函数的命名与OC的命名有很多相似的地方

	- 它们以用于类的相同前缀开始
	- 单词前缀后的第一个字母要大写
	- 大多数函数名以动词开头，用来描述函数的作用

	如：
	```
	NSHighlightRect
	NSDeallocateObject
	```
    
- 如果函数返回其第一个参数的属性，则省略谓词。
 ```
 unsigned int NSEventMaskFromType(NSEventType type)
 float NSHeight(NSRect aRect)
 ```
- 如果该值是通过引用返回的，则使用“Get”。
 ```
 const char *NSGetSizeAndAlignment(const char *typePtr, unsigned int *sizep, unsigned int *alignp)
 ```
- 如果返回的值是布尔值，则函数应该以变形动词开始
 ```
 BOOL NSDecimalIsNotANumber(const NSDecimal *decimal)
 ```

### 4. 变量和数据类型

- 驼峰命名
  ```
  @property (assign) BOOL showsAlpha;
  ```
- 实例变量,要写下划线
  ```
  @interface Class ()
  {
  	BOOL _showsAlpha;
  }
  @end
  ```
- 属性
  ```
  ///字符串使用copy
  @property (nonatomic, copy) NSString *friendId
  
  ///头文件使用,readonly,实现文件使用readwrite
  @interface Class: NSObject
  @property (nonatomic, strong, readonly) NSArray *novelArray;
  @end
  ...
  @interface Class()
  @property (nonatomic, strong, readwrite) NSArray *novelArray;
  @end
  
  ///weak的使用
  @property (nonatomic, weak) id<Delegate>delegate; ///代理
  @property (nonatomic, weak) id object; ///弱引用一个对象
  
  ///懒加载
  - (NSArray *)array {
  	if (!_array) {
    	_array = alloc（）
    }
    return _array
  }
  
  ///getter
  @property (assign, getter=isShowsAlpha) BOOL showsAlpha;
  
  ///类属性
  @property (class, assign) BOOL showsAlpha;

  ///分类的关联属性
  + (SSCustomAlertView *)alertView {
  	 return objc_getAssociatedObject(self, @selector(setAlertView:));
  }
  + (void)setAlertView:(SSCustomAlertView *)alertView {
    objc_setAssociatedObject(self, _cmd, alertView, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
  }
  
  ```
  
 - 枚举
  ```
      枚举的命名必须跟随类的名称来命名区分
      两种枚举：
      ///普通枚举
      typedef NS_ENUM(NSInteger, UIViewAnimationTransition) {
        UIViewAnimationTransitionNone,
        UIViewAnimationTransitionFlipFromLeft,
        UIViewAnimationTransitionFlipFromRight,
        UIViewAnimationTransitionCurlUp,
        UIViewAnimationTransitionCurlDown,
    };
    ///位运算，可以判断多种符合的枚举，（UIViewAutoresizingFlexibleLeftMargin｜UIViewAutoresizingFlexibleRightMargin）
    typedef NS_OPTIONS(NSUInteger, UIViewAutoresizing) {
        UIViewAutoresizingNone                 = 0,
        UIViewAutoresizingFlexibleLeftMargin   = 1 << 0,
        UIViewAutoresizingFlexibleWidth        = 1 << 1,
        UIViewAutoresizingFlexibleRightMargin  = 1 << 2,
        UIViewAutoresizingFlexibleTopMargin    = 1 << 3,
        UIViewAutoresizingFlexibleHeight       = 1 << 4,
        UIViewAutoresizingFlexibleBottomMargin = 1 << 5
    };
  ```
 - 全局变量，静态变量
 
   如果是常量的话需以k开头定义
   ```
   ///全局常量头文件定义，实现文件实现
   UIKIT_EXTERN NSString *const kHNVesionString;
   NSString *const kHNVesionString = @"2.0.9";
   
   ///局部静态变量
   static NSString *const kHNVesionString = @"2.0.9";
   
   ```
 - 数组
 
 ```
 遍历使用enumerateObjectsUsingBlock,因为自带autoreleasepool
 [array enumerateObjectsUsingBlock:^(id  _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
 }];
 ```
 
  
### 5. 内存管理
 
  - 循环引用

      A对象和B对象直接或者间接强引用都会造成循环引用，由于RAC内存管理的机制造成内存不能释放，通过其中一方弱引用对方打破循环引用

      ```
      1. block循环引用
      [RACObserve(self, hasRechargedOperation)subscribeNext:^(id  _Nullable x) {
          self.hn_navigationController.hn_disableInteractivePopGestureRecognizer = ![x boolValue];
      }];
      上面代码因为 self间接强引用了RAC的block,然后block会捕获self，强引用了self对象，所以会造成循环引用
      通过以下代码解除循环引用：
      @weakify(self);
      [RACObserve(self, hasRechargedOperation)subscribeNext:^(id  _Nullable x) {
          @strongify(self);
          self.hn_navigationController.hn_disableInteractivePopGestureRecognizer = ![x boolValue];
      }];

      2. 委托循环引用解决
       @property (nonatomic, weak) id<Delegate>delegate; ///代理
       
      3. NSTimer、 NSDisplayLink造成的循环引用，通过持有weak间接对象或者userinfo传入block来打破循环引用 

      ```
  - 野指针

    在使用异步方法回调时，要注意回调里面对象是否释放，然后访问已经释放的对象会 BAD_ACCESS.

    ```
    例如GCD的异步回调block，可以通过@weakify(self)和@strongify(self)解决这个问题
    ```
  - 多次创建对象

   在短时间内创建多个对象会造成对象不能及时释放，内存暴涨 ,使用一下方法解决：

   ```
   @autoreleasepool {
      <#statements#>
   }
   ```
  - 监听内存警告，实时释放旧的内存。
  
  ```
     ///VC
     - (void)didReceiveMemoryWarning {
           //clear
     }

  ```
  - 控制单例的使用量
  
### 5. 单例的使用

 - 单例的类不要给继承，因为单例始终只能初始化一个对象，不符合继承可扩展的思想
 - 使用单例要注意多线程的问题，当出现线程资源竞争的问题，需要使用锁
 - 单例需要注意是否持有内存消耗比较高的IO操作对象，要注意释放
  
  
### 6. 编程思想

 - [六大设计原则](https://juejin.im/post/6844903673672237063)
 - 设计类的时候，需要考虑以后的扩展性，还有类之前的耦合情况。
 - 通过协议、组合、封装等解耦
 - 使用类族实现工厂方法，例如UIButton初始化的方法，根据不同类型返回的是不同子类的实例对象
 
### 7. LLDB的调试
- [LLDB](https://objccn.io/issue-19-2/)

### 8. 工具
  - 接口调试： [Postman](https://www.postman.com)
  - 代码映射： [JSONExport](https://github.com/Ahmed-Ali/JSONExport)
  - 终端： [iTerm2](https://www.iterm2.com)
 
 
### 9. 团队协作

 - 修改或者删除代码，需要理清逻辑，不明白先向同事问清楚
 - 引用第三方库需要思考下要不要二次封装，以便后期换库
 - 编写分类方法时要注意覆盖原来类的方法
 - 代码编写太难理解的地方需要加注释
 - 合并代码发生冲突，不明白的情况需要向同事问清楚
 - 测试过的代码，如果重构修改逻辑，需要重新测试，评估影响情况
 - 最好每天都有codereview
 - 发现同事代码有问题需要告知同事一声
 - 能沟通最好当面沟通解决问题
 
### 10. git 

#### 分支管理
- master分支，版本发布，打tag，代码只能从其他分支合并过来，不能修改
- dev分支，保持开发的最新代码，当发布测试完成这里可以考虑打tag
- feature分支,从dev分支出来的开发新功能的分支，以feature/XXX格式命名，功能开发完合并到dev
- test分支，测试分支，feature开发完合并到dev，再合并到test分支进行测试，测试的bug在test修改完再合并回dev,feature,测试完成可以上线再合并到master
- hotfix,线上问题修复，以master分支出来的分支，修复测试完成合并到master,dev

#### commit标识

常用的
- [fix] -> 表示bug修复
- [feat] -> 新功能
- [refactor] -> 代码重构
- [docs] -> 调整代码格式
- [import] -> 导入库






 
 
  
   


