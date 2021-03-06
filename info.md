# JustWeEngine - Android游戏框架
An easy open source Android Native Game FrameWork.   
![logo](art/logo.png)  
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-JustWeEngine-green.svg?style=true)](https://android-arsenal.com/details/1/2903)[ ![](https://jitpack.io/v/lfkdsk/JustWeEngine.svg)](https://jitpack.io/#lfkdsk/JustWeEngine)

## 引擎核心类流程图  
![engine](art/engine.jpg)  
## 使用方法  
* 引入Engine作为Library进行使用。
* 引入"/jar"文件夹下的jar包。  
* 使用Gradle构建:  
  * Step 1. Add the JitPack repository to your build file  
  Add it in your root build.gradle at the end of repositories:  
  
  ``` groovy  
  
    	allprojects {
			repositories {
				...
				maven { url "https://jitpack.io" }
			}
		}
   	
  ```
  
  * Step 2. Add the dependency  on
  
  
  ``` groovy
  
      dependencies {
	        compile 'com.github.lfkdsk:JustWeEngine:v1.10'
	  }
		
  ```
* 使用Maven构建:  
  * Step 1. Add the JitPack repository to your build file  
  
  ``` xml
  
    <repositories>
		<repository>
		    <id>jitpack.io</id>
		    <url>https://jitpack.io</url>
		</repository>
	</repositories>
  
  ```
  
  * Step 2. Add the dependency  
  
  ``` xml
  	
    <dependency>
	    <groupId>com.github.lfkdsk</groupId>
	    <artifactId>JustWeEngine</artifactId>
	    <version>v1.10</version>
	</dependency>
	
  ```

## 引擎进入V1.10版本

* 以之开发的微信打飞机游戏Demo：[Demo地址](https://github.com/lfkdsk/EngineDemo)  
* 很多额外控件：[JustWeTools](https://github.com/lfkdsk/JustWeTools)  
* 网络功能的Demo：[JustWe-WebServer](https://github.com/lfkdsk/JustWe-WebServer)  
* StudioVSEclipse([ice1000](https://github.com/ice1000))：[StudioVSEclipse](https://github.com/ice1000/StudioVSEclipse)    

## 快速入门  

* [1.基础功能](#1基础功能)
	* [1.1继承引擎核心类](#11继承引擎核心类)
	* [1.2绘制文字](#12绘制文字)
	* [1.3绘制图片](#13绘制图片)
	* [1.4使用精灵](#14使用精灵)
	* [1.5使用按钮](#15使用按钮)
* [2.动画系统](#2动画系统)
	* [2.1绑定在BaseSub物品及精灵基类上的动画类](#21绑定在basesub物品及精灵基类上的动画类)
	* [2.2绑定在Button上的动画类](#22绑定在button上的动画类)
* [3.物体分组碰撞检测和死亡判定](#3物体分组碰撞检测和死亡判定)
* [4.屏幕扫描模式](#4屏幕扫描模式)
* [5.工具类](#5工具类)
* [6.音频系统](#6音频系统)  
	* [6.1播放短音效](#61播放短音效)
	* [6.2播放音频](#62播放音频)
	* [6.3通过短音效编曲](#63通过短音效编曲)

## 进阶应用
* [7.使用网络](#7使用网络)  
* [8.使用状态机精灵](#8使用状态机精灵)  
* [9.CrashHandler崩溃守护](#9crashhandler崩溃守护)
* [10.使用蓝牙](#10使用蓝牙)
    * [10.1开启、关闭服务](#101开启关闭服务)
    * [10.2扫描设备](#102扫描设备)
    * [10.3发送消息](#103发送消息)  
* [11.SQLite数据库](#11SQLite数据库)
	* [11.1创建表](#111创建表)
    * [11.2增删查改](#112增删查改)  
    
## 拓展功能  
* [允许玩家绘制](#允许玩家绘制)  
* [流程脚本](#流程脚本)

### 1.基础功能
#### 1.1继承引擎核心类： 
   由于框架全部使用SurfaceView进行绘制，不使用诸如Button、Layout等原生控件，所以应该首先新建类继承引擎核心类Engine，负责游戏的流程，注释中已有明确的标明功能。  
   
``` java

	public class Game extends SimpleEngine {
	// 一般在构造函数完成变量的初始化
    public Game() {
    	// 控制debug模式是否开始，debug模式打印日志、帧数、pause次数等信息
        super(true);
        
    }
	
	// 载入一些UI参数和设置屏幕放向，默认背景色，设定屏幕的扫描方式等
    @Override
    public void init() {
    	// 初始化UI默认参数，必须调用该方法，其中有一些用于多机型适配的参数需要初始化
        UIdefaultData.init(this);
    }

	// 通常用于精灵，背景，图片等物体的设置和载入
    @Override
    public void load() {

    }

	// draw 和 update 在线程中进行不断的循环刷新
	// draw 负责绘制 update 负责更新数据和对象信息
    @Override
    public void draw() {

    }

    @Override
    public void update() {

    }
	
	// 将touch 事件传回 功能和所设定的屏幕扫描方式有关
    @Override
    public void touch(MotionEvent event) {

    }
    
	// 将碰撞事件传回 传回精灵和物品的基类 
	// 用于处理碰撞事件 默认使用矩形碰撞
    @Override
    public void collision(BaseSub baseSub) {

    }
    }

```   
  
#### 1.2绘制文字：
    
使用GamePrinter进行文字绘制,除此以外还有多种方法绘制:  
  
``` java

    @Override
    public void draw() {
        Canvas canvas = getCanvas();
        GameTextPrinter printer = new GameTextPrinter(canvas);
        printer.drawText("哈哈哈", 100, 100);
    }
    
```  
效果图：  
![text](art/printer.png)  

#### 1.3绘制图片：
建议图片存放在Asset中：  
``` java  
	GameTexture texture = new GameTexture(this);
	texture.loadFromAsset("pic/logo.jpg")
	texture.draw(canvas, 100, 100);
```  
效果图：    
![pic](art/pic.png)  
另外也可使用`loadFromAssetStripFrame`从一个大的图片中取出对应位置的图片。  

``` java

	/**
     * get bitmap from a big bitmap
     *
     * @param filename
     * @param x
     * @param y
     * @param width
     * @param height
     * @return
     */
    public boolean loadFromAssetStripFrame(String filename,
                                           int x, int y,
                                           int width, int height)
```  
比如可以通过这四个参数把这个小飞机取出来： 
![back](art/back.png)  
![ship](art/ship.png)  
PicUtils中提供了在Bitmap处理中很有用的各种特效和压缩方法，大家可以一试。  

#### 1.4使用精灵：
  使用精灵可以使用BaseSprite也可以继承该类使用，BaseSprite封装了很多方法供各种动画使用，这些功能很多都是需要结合动画系统来使用的，动画系统会在后面介绍。  
##### 新建精灵：
  1.简单初始化:  
  ``` java
  
          sprite = new BaseSprite(this);
          
  ```
  2.初始化连续帧动画：  
  连续帧的初始化需要这样的连续帧图片:  
  ![zombie](art/zombie.png)
  
  ``` java 
  
        GameTexture texture = new GameTexture(this);
        texture.loadFromAsset("pic/zombie.png");
        // 长宽以及列数
        sprite = new BaseSprite(this, 96, 96, 8);
        sprite.setTexture(texture);
        sprite.setPosition(100, 100);
        sprite.setDipScale(100, 100);
        // 帧切换动画是关键
        sprite.addAnimation(new FrameAnimation(0, 63, 1));
        addToSpriteGroup(sprite);
        
  ```
  
  效果图:  
  ![zombiegif](art/zombie.gif)  
  3.使用从大图取出的多帧图片： 
  ``` java  
  
    	// 新建图片资源（此图为上图的大图）
        GameTexture texture = new GameTexture(this);
        texture.loadFromAsset("pic/shoot.png");
        // 初始化设定模式和长宽
  		ship = new BaseSprite(this, 100, 124, FrameType.COMMON);
  		// 设定资源
        ship.setTexture(texture);
        // 从大图中取出两帧
        ship.addRectFrame(0, 100, 100, 124);
        ship.addRectFrame(167, 361, 100, 124);
        ship.addAnimation(new FrameAnimation(0, 1, 1));

  ```
  效果图(两帧图片不断切换):  
  ![ship](art/ship.gif)  

  4.一些重要的其他设定：
    
  ``` java  
  
  	  // 图片资源
  	  ship.setTexture(texture);
  	  // 大图取帧模式
  	  ship.addRectFrame(0, 100, 100, 124);
  	  // 设定位置
  	  ship.setPosition(x, y);
  	  // 设置dp大小
      ship.setDipScale(96, 96);
      // 设定dp位置
	  ship.setDipPosition(x, y);
	  // 设定透明度
	  ship.setAlpha(...);
	  // 只有将精灵添加到SpriteGroup中框架才会自行绘制，否则需要手动调用
	  addToSpriteGroup(ship);
	  ...
	  
  ``` 

#### 1.5使用按钮：  
  使用的按钮可以继承BaseButton进行拓展，也可以直接使用TextureButton和TextButton进行使用。  
  Button设定功能的方式和原生一样，通过设定接口回调的方式进行：
  ``` java  
  
  		button.setOnClickListener(new OnClickListener() {
          @Override
          public void onClick() {
              Log.e("button", "onClick");
          }
        });
        
  ```
  1.TextureButton: 
   
  ``` java  
  
      TextureButton button;
      // 初始化并设定名字
      button = new TextureButton(this, "logo");
	  texture = new GameTexture(this);
      texture.loadFromAsset("pic/logo.jpg");
      // 添加图片资源
      button.setTexture(texture);
      // button的接口回调，不是View的那个接口
      button.setOnClickListener(new OnClickListener() {
          @Override
          public void onClick() {
              Log.e("button", "onClick");
          }
        });
      button.setPosition(200, 300);
      button.setDipScale(100, 150);
      // 添加到ButtonGroup进行绘制和处理
      addToButtonGroup(button);

  ``` 
  效果图:  
  ![texturebutton](art/Texturebutton.png)  
    结合PicUtil中的各种Bitmap处理方法可以很容易的做出各种样式的Button：  
  ![buttons](art/buttons.jpg)  
  
  2.TextButton:  
  
  ``` java  
  	  
      TextButton button;  
      button = new TextButton(this, "logo");
      button.setText("刘丰恺");
      addToButtonGroup(button);
      // 余略见源码
	  ...
	  
  ```
  效果图：  
![button](art/singlebutton.png)  

### 2.动画系统  
  目前的动画系统可以使用已经封装好的继承了BaseAnimation的动画，也可以继承BaseAnim进行自我定义动画类进行使用。  
#### 2.1绑定在BaseSub物品及精灵基类上的动画类  
AnimType中保存了Animation的应用类型。

| Animation     | method        |function|
| ------------- |:-------------:|-------:|
| AliveAnimation|adjustAlive(boolean ori) | 碰撞检测的时候进行判断存活状态 |
| AlphaAnimation|adjustAlpha(int ori)     | 修改物体透明度              |
| CircleMoveAnimation | adjustPosition(Float2 ori)| 沿某一圆心进行圆周运动 |
| FenceAnimation | adjustPosition(Float2 ori)| 使用围栏动画防止出界 |
| FrameAnimation | adjustFrame(int ori) | 逐帧动画 |
| MoveAnimation | adjustPosition(Float2 ori) | 位移动画 |
| SpinAnimation | adjustRotation(float ori) | 旋转动画 |
| ThrobAnimation | adjustScale(Float2 ori) | 跳跃动画 |
| VelocityAnimation | adjustPosition/adjustAlive | 线性加速度计 |
| WrapMoveAnimation | adjustPosition(Float2 ori) | 围栏动画防止出界 |
| ZoomAnimation | adjustScale(Float2 ori) | 放大缩小动画 |
| 待续 | ... | ... |

绑定动画分为两类，ListAnimation和FixedAnimation,ListAnimation将动画存储到固定的一个List中，用于重复更新的动画，
而FixedAnimation存储在Map中，使用名字进行调用，用于点击或者非自动更新的动画。
比如前面精灵类动画的就是添加到ListAnimation。
下面的这种写法就是FixedAnimation，这个动画是小飞机入场，因为只使用了一次，所以使用了FixedAnimation。
``` java

        ship.addfixedAnimation("start",
                new MoveAnimation(UIdefaultData.centerInHorizontalX -   ship.getWidthWithScale() / 2,
                        UIdefaultData.screenHeight - 2 * ship.getHeightWidthScale(), new Float2(10, 10)));
           
```

效果图:  
![fly](art/fly.gif)  

#### 2.2绑定在Button上的动画类  
BaseButtonAnimation是BaseButton的动画类继承了BaseAnim的动画基类，通过提供Button的状态，设定Button的动画。

| Animation        | method           | function  |
| ------------- |:-------------:| -----:|
| ZoomCenterButtonAnim |adjustButtonRect(Rect ori,boolean touchType) | 按钮放缩动画 |
| ColorAnimation|adjustButtonBackGround(int ori,boolean type)| TextButton点击变色 |
| 待续 | ... | ... |

为Button设定放缩动画:  
``` java

	// 设定中心放缩
    button.setZoomCenter(true);
    // 三个参数 初始值／放大值／帧数
    button.setAnimation(new ZoomCenterButtonAnim(10, 30, 3));
	
```
效果图:  
![zoom](art/zoom.gif)    

为Button设定颜色动画:  

``` java

	// 初始颜色 ／ 按下颜色
	button.setAnimation(
       new ColorAnimation(UIdefaultData.colorAccent,
       UIdefaultData.colorPressed));

```
效果图:  
![color](art/button.gif)    

### 3.物体分组碰撞检测和死亡判定
使用设置ID和Name进行物体分组，通过物体分组，框架核心类会对对象进行分类处理。
``` java

	final int SHIP = 0;
	ship.setName("SHIP");
    ship.setIdentifier(SHIP);

```

只要使用了`addToSpriteGroup(sprite)`的精灵对象就会自动进行碰撞检测，而对碰撞检测的结果会从
`collision`中进行发回。
``` java

    @Override
    public void collision(BaseSub baseSub) {
    	// 获取与之碰撞的对象
        BaseSprite other = (BaseSprite) baseSub.getOffender();
        // 获取ID分组处理
        if (baseSub.getIdentifier() == BULLET &&
                other.getIdentifier() == ENEMY) {
            // 设定死亡
            other.setAlive(false);
            // 回收
            removeFromSpriteGroup(other);
            addToRecycleGroup(other);
        }
    }
    
```

其中`getOffender()`获得与之碰撞的对象，通过`getIdentifier()`获取设定的对象分组，实行逻辑判断。
开启Debug模式会看见碰撞线。  
效果图:  
![debug](art/co.png)
### 4.屏幕扫描模式  
屏幕扫描模式是用来优先响应屏幕点击、Button点击、和多点触控而设的，放置在不同情况下都能优化屏幕的刷新。  
``` java

  	// 检测单一移动
  	SINGLE,
  	// 检测Button
    BUTTON,
    // 多点检测
    FULL,
    // 单击＋Button
    SINGLE_BUTTON
  
```
并且通过如下方式进行设置:  

``` java
	
	super.setTouchMode(TouchMode.BUTTON);

``` 


### 5.工具类  
   * `NetUtils` 网络状态工具类
   * `PicUtils` 图片处理工具类
   * `ServiceUtils` 服务工具类
   * `ImageHelper` 图型处理类  
   * `DisplayUtils` 数据转换类
   * `SpUtils` Sp简化工具类（`可存储list和map`）
   * `ValidatorsUtils` 正则表达式处理类  

### 6.音频系统  
#### 6.1播放短音效 
播放短音效，首先初始化`SoundManager`用以加载音效。  
``` java

	// 接收实例和Manager的尺寸
    SoundManager manager = new SoundManager(this, 5);
    // 从assets加载音频 同时加载路径也会作为音效名进行存储
	manager.addSound("mic/open.mid");
	// 通过加载名进行播放
	manager.play("mic/open.mid");
	
	
```

完成以上步骤就可以播放了，当然尽量只向其中放置较短的音效，如背景音乐的长音频，请见播放音频。  

``` java

	public void removeSound(String musicName) // 移除
	public void play(String musicName, float volume) // 播放 ＋ 音量
	public boolean containSoundID(int soundID) // 判断音频是否存在
	public int getSoundID(String soundName)  // 获取ID
	...


```  
#### 6.2播放音频  
播放音频适合例如背景音乐一样的音乐。  

``` java  

	// 传入两个参数 上下文和文件名
	MusicPlayer player = new MusicPlayer(this, "mic/open.mp3");
    player.play();

```  
以上的就能实现播放了，下面还有一些其他的方法。

``` java  

	public void dispose() // 清理
	public void setLooping(boolean isLooping) // 是否循环
	public void setVolume(float volume) // 设定音量
	...
	
```  

#### 6.3通过短音效编曲  
从`SoundManager`中导入多段音频，快速播放达成音效的效果。

``` java 

    SoundManager manager = new SoundManager(this, 5);
    manager.addSound("mic/1.mid");
    manager.addSound("mic/2.mid");
    SoundPlayer player = new SoundPlayer(manager, 500, 16);
    player.addSound("mic/1.mid");
    player.addSound("mic/2.mid");
    ... 

```

使用`player.play();`进行播放。


### 7.使用网络
网络的使用可参考[JustWe-WebServer](https://github.com/lfkdsk/JustWe-WebServer)中的介绍。
按照介绍操作就可以通过：
 
``` java
  
        server.apply("/lfk", new OnWebStringResult() {
            @Override
            public String OnResult() {
                return "=======";
            }
        });

        server.apply("/main", new OnWebFileResult() {
            @Override
            public File returnFile() {
                return new File(WebServerDefault.WebServerFiles+"/"+"welcome.html");
            }
        });
        
```  
        
这样的简单方式绑定路由，而get／post数据可以直接使用http协议的get和post进行。

### 8.使用状态机精灵

``` java

    // 为状态机添加一个任务
    sprite.addState(new StateFinder() {
        @Override
        public boolean isContent(BaseSub baseSub) {
            return Math.abs(zom.s_position.x - baseSub.s_position.x) > 50;
        }
    }, new FrameAnimation(0, 63, 1));

```
  
可以通过上述的addState方法为状态机精灵添加一个任务，只有当第一个参数接口回调的返回值为真的时候，
才会去运行第二个参数提供的指令，如果返回为假则会运行第二项状态的判断。
状态的优先级由加入顺序提供。

效果图:  
![state](art/statesprite.gif)    

### 9.CrashHandler崩溃守护  
CrashHandler用于处理游戏的意外崩溃事件，初始化推荐在Application中进行。
CrashHandler可以自动保存机型和异常日志，以便让开发者找到问题所在。

``` java

    CrashHandler.getInstance().init(this);

```
使用以上语句即可自动保存错误日志。
还可以:

``` java
        
    CrashHandler.getInstance().setRestartActivity(MainActivity.class); // 重启的Activity
    // 添加崩溃回调
    CrashHandler.getInstance().addCrashListener(new AfterCrashListener() {
        @Override
        public void AfterCrash() {  // 设定保存项目
            ...
        }
    });    

```

### 10.使用蓝牙

#### 10.1开启、关闭服务
使用蓝牙需要新建`BlueToothServer`对象，传入上下文和MessageBack接口。

``` java

        blueToothServer = new BlueToothServer(this, new OnMessageBack() {
            @Override
            public void getMessage(String msg) {
                Log.e("L", msg);
            }

            @Override
            public void sendMessage(String msg) {
                Log.e("L", msg);
            }

            @Override
            public void getDevice(ArrayList<String> msg) {
                Log.e("L", msg.size() + "");
            }
        });
		
		// 使用如下语句进行初始化
        blueToothServer.init();

```  
服务初始化之后如未打开蓝牙，系统会自动提示应用要求蓝牙开启。

通过MessageBack接口可以接收到发送、接收、以及扫描设备信息，采取对应操作就可以获得数据。

关闭服务时请使用`blueToothServer.unBindService();`关闭服务。

#### 10.2扫描设备 
使用`blueToothServer.doDiscovery();`进行设备扫描，返回结果在OnMessageBack()接口的
getDevice()方法接收。
使用`blueToothServer.ensureDiscoverable();`允许被扫描。
使用`blueToothServer.getPairedDevices();`返回已配对的设备列表。

#### 10.3发送消息
在配对成功之后就可以使用`blueToothServer.sendMessage(String msg);`发送消息了。
同时，消息的接收也可以从getMessage()接口中获得。  

### 11.SQLite数据库  

SQLite使用了IOC的模式。

#### 11.1创建表

新建的创建表需要继承Node并且写出注解类。  

``` java  
	
	// 表名
	@TableName(tableName = "lfkdsk")
	public class User extends Node {

	// 主键自增 INTEGER型
    @LabelName(autoincrement = true,
            type = LabelName.Type.INTEGER,
            columnName = "name",
            generatedId = true)
    private int name;
	
	// TEXT型 栏名为user_name
    @LabelName(type = LabelName.Type.TEXT,
            columnName = "user_name")
    private String user_name;

	// 自增主键所以只需要提供其他信息
    public User(String user_name) {
        super(user_name);
        this.user_name = user_name;
    }

    public User(int name, String user_name) {
        super(name, user_name);
        this.name = name;
        this.user_name = user_name;
    }

    public int getName() {
        return name;
    }

    public void setName(int name) {
        this.name = name;
    }

    public String getUser_name() {
        return user_name;
    }

    public void setUser_name(String user_name) {
        this.user_name = user_name;
    }
	}

```


``` java  

	// 通过这种方式获取数据库   表名
    private DataBase dataBase = DataBase.initAndOpen("user", User.class);


```

#### 11.2增删查改

``` java  

	// add
	database.insert(User user);
	// find
	database.get(int position);
	// delete
	database.delete(int position);
	// update
	database.update(User user);
	...

```

## 扩展功能

### 允许玩家绘制
可接受用户的绘制输入，并以之生成精灵、背景、或其他对象：[如何使用？](https://github.com/lfkdsk/JustWeTools#paintview画图工具)  

### 流程脚本  

```   
	用以控制人物对话或其他流程的脚本，目前能设定变量，使用简单的表达式，还有分支结构的功能
	，等我好好刷完龙虎书再填坑。
	
```



##有问题反馈
在使用中有任何问题，欢迎反馈给我，可以用以下联系方式跟我交流

* 邮件:lfk_dsk@hotmail.com  
* weibo: [@亦狂亦侠_亦温文](http://www.weibo.com/u/2443510260)  
* 博客:  [刘丰恺](http://www.cnblogs.com/lfk-dsk/)  

## License

    Copyright 2015 [刘丰恺](http://www.cnblogs.com/lfk-dsk/)

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

