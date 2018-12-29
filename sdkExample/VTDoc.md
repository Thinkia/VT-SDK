## 拓视觉 sdk 文档

### 准备工作
1. 在工程中引用 VT.js 文件和 vt.css 文件。

### 初始化
#### 方法：
1. VT.initContext({divContainer})：return null
+ divContainer : div元素,用于承载三维渲染的容器。
```javascript
// 首先初始化三维渲染的上下文环境
VT.initContext({divContainer:document.getElementById('app')});
```

### 加载模型数据
#### 方法：
1.  VT.loadModels({filePath})：return null
+ filePath : 模型数据的路径。
```javascript
// 加载模型文件
VT.loadModels({filePath:'https://cdn1.visualtouring.com/V_VT/changsha/2018-09-15/hicollector/e7a1982d40a1da0bd80439d870196db8'});
```

### 模式切换
+ 全景模式：单击模型任意位置。或者调用方法`VT.modePano();`
+ 3d模式：调用方法`VT.mode3D()`。
+ 平面模式：调用方法`VT.modePlan()`。

### 标签功能

#### 常量

1. VT.LINE_TYPE : 枚举类型，目前支持 `VT.LINE_TYPE.default(实线)` 和 `VT.LINE_TYPE.dash(虚线)` 两种枚举。
2. VT.LABEL_TYPE : 枚举类型，目前支持 `VT.LABEL_TYPE.image(图片类型)` 和 `VT.LABEL_TYPE.text(文字类型)`
#### 方法
##### 1. VT.getLabelBasicInfo() : return LabelBasicInfo 
   
+ LabelBasicInfo : 标签基本信息对象。
```markdown
{
   success (boolean) : boolean类型状态值，用于判断是否成功获取信息。
   basicInfo: {
     position (vec3) : 三维向量，标签的三维坐标 ,
     normal (vec3) : 三维向量，标签位置的平面法向量 ,
     floorInfo (string) : 楼层信息 
   },
   msg (string) : 提示信息
}
```
**获取创建标签的必要信息（坐标，法向量，楼层信息）** 

##### 2. VT.createLabel( LabelInfo ) : return  Label
+ LabelInfo : 标签信息对象。
```markdown
{
    position (vec3) : 三维向量，标签的三维坐标 , 
    normal (vec3) : 三维向量，标签位置的平面法向量 , 
    floorNo (string) : 楼层信息 , 
    labelImg (string) : 图片资源路径 , 
    labelText (string) : 文字类型标签的内容 ,
    labelType (enum) : 枚举变量(VT.LABEL_TYPE)，标签类型（默认图片类型）。
    offset (float) : 标签偏移量 , 
    lineType (enum) : 枚举变量(VT.LINE_TYPE)，线段类型（默认实线）。
    lineColor (string) : 支持 css 中常用的颜色字符串，如 '#ff0000' , 
    lineAlpha (float) : 线段透明度（0.0~1.0） , 
    lineWidth (float) : 线段宽度 ,
    title (string) : 标签标题 , 
    content (string) : 标签内容 , 
    resUrl (string) : 标签资源链接 , 
    linkUrl (string) : 标签跳转链接
}
```
+ Label : 一个标签对象实例，通过该实例可设置标签的点击事件回调。
```javascript
// 创建标签并获取实例
var label = VT.createLabel(LabelInfo);
// 设置点击事件回调
label.setClickEvent( function(event) {
  console.log(event)
} );
```

##### 3. VT.labelEditStatus (boolean) ： return null 
```javascript
// 开启标签编辑模式，编辑模式下可看到隐藏的标签
VT.labelEditStatus(true);
```
**设置 true 为编辑模式（开），可看见已隐藏的标签。false 为编辑模式（关），被隐藏的标签不可见。**


### 测距功能
+ 测距功能开启后右键点击模型任意两点即可测量显示两点的直线距离; 

### 测距功能
+ 函数：VT.distance({});
+ 说明：测距开关默认关闭，调用则开启；在开启的状态下再次调用则关闭开关；


### 户型图功能
+ 函数：VT.showSvg({})
+ 参数: 1.若不传参数则默认户型图的容器id为'svg',容器默认display属性为none;
        2.若要使用自定义容器id为 a 则使用VT.showSvg({divID='a'});
+ 说明：该函数需要在全景状态中调用，根据当前位置所在楼层初始化对应楼层的户型图并显示居中显示在户型图容器中;

### VR模式
+ 函数：VT.useVR()，默认关闭
+ 说明：该函数需要在全景状态中调用,移动端才能看到效果;将手机放到VR眼镜盒子，开启VR模式，淡紫色视口小环对准全景中显示的大虚拟球，淡紫色视口小环外边框读条完毕后即可移动到对应位置;

### 标尺模式
+ 函数：VT.showRule(); 默认关闭
+ 说明：该函数为内置属性,点击开启即可看到房间的长宽高三维属性; 

### 相机操作
+ 函数：VT.cameraHandle({
           _direction:'top',
           _degree:5
         });
+ 说明：1._direction可传参'top''left''right' 'bottom' 分别对应上左右下;
        2._degree：转动的角度;
        
 ### 前进模式
        
+ 函数：VT.findBestPoint();

+ 说明：在全景下使用,根据当前朝向和点位信息,自动找到最合适的点位并前进移动;

### 区域编辑数据
+ VT.getAreaEditObj()          返回json字符串对象                    用于保存
+ VT.setAreaEditObj(jsonObj)     jsonObj   为保存的字符串对象   用于设置区域编辑数据

### 场景数据

+ VT.getSceneInfo()   返回json字符串场景数据                   用于保存
+ VT.setSceneInfo(sceneInfo )    sceneInfo 为保存的json字符串   用于设置场景数据

