

WebGIS开源架构

主要内容：

postgis

openlayers

geoserver

开源架构Webgis解决方案开发指南 视频教程链接：

https://blog.csdn.net/weixin_34206806/article/details/106514212



微信公众号代码使用markdown格式

Typora启用源代码格式，复制代码，Ctrl+Alt+M 使用 Markdown Here 渲染



学习网站在此

<https://openlayers.org/>

<https://github.com/openlayers/openlayers/>

<https://github.com/liujiusheng/blog>

<https://github.com/anzhihun/OpenLayers3Primer>

## 一、开发环境搭建

### 1 postgis

#### 1.1 postsql环境配置

postsql 安装

user：postgres

password：mml

postgis 安装 新建数据库postgis_25_sample



#### 1.2 以postgis_25_sample模板新建数据库 

​	架构-public

 * 数据表-spatial_ref_system：空间参考
 * 函数



#### 1.3 数据入库(Import)

##### 	* PostGIS2.0 Shapefile and DBF  loader Exporter

##### 	* Add File

##### 	* Import List

​		Import Options   GBK

​		Schema：模式

​		Table：表名称,自动取为shapefile名称

​		Geo Column：空间字段名称,默认为geom

​		SRID：默认为0，可设为4326   (WGS84)

​		Mode：Create、Append、Delete、Prepare

##### 	* 点击Import

##### 	* public-数据表 刷新

select st_astext("geom")  from public.intersect;



安装jdk8及以上版本



### 2 GeoServer

#### 2.1 进入GeoServer

<http://localhost:8595/geoserver/>

admin

geoserver

#### 2.2 GeoServer界面

Layer Preview：查看图层列表，也可查看系统发布的图层

工作区：可区分不同项目和图层类型

数据存储：用来连接数据库、shapefile文件或tif栅格文件

图层：图层发布界面，用来发布图层

图层组：可把一些图层放在一个图层组里

Styles：预设内部样式

Tile Layers：瓦片图层

#### 2.3 图层发布和浏览

新建工作组

数据存储-新建PostGIS数据源

保存

发布

Layer Preview中查看浏览：openlayers/GeoJSON(WFS)

#### 2.4 解决跨域问题

lib中跨域jar包jetty-servlets.jar添加到GeoServer 2.15.1\webapps\geoserver\WEB-INF\lib下

修改GeoServer 2.15.1\webapps\geoserver\WEB-INF\web.xml文件

在filter平级位置添加：



```
<filter>        
     <filter-name>cross-origin</filter-name>        
     <filter-class>org.mortbay.servlets.CrossOriginFilter</filter-class>        
     <init-param>            
         <param-name>allowedOrigins</param-name>            
         <param-value>*</param-value>        
     </init-param>        
     <init-param>            
		<param-name>allowedMethods</param-name>            
		<param-value>GET,POST</param-value>        
     </init-param>        
     <init-param>           
        <param-name>allowedHeaders</param-name>            
        <param-value>x-requested-with,content-type</param-value>        
	</init-param>    
</filter> 
```



在filter-mapping平级位置添加：

```
<filter-mapping>

	<filter-name>cross-origin</filter-name>

	<url-pattern>/*</url-pattern>

</filter-mapping>
```



### 3 开源tomcat版本+geoserver.war



#### 3.1 安装tomcat8.5.61

server shotdown port：8005

http/1.1 connect port：8080



#### 3.2 geoserver.war

 将geoserver-2.16.3-war下的geoserver.war复制到

C:\Program Files\Apache Software Foundation\Tomcat 8.5\webapps下



#### 3.3 tomcat开启服务

start service，自动在webapps下新建geoserver文件夹(包括数据源data、日志)



#### 3.4 访问geoserver

<http://localhost:8080/geoserver>

[http://127.0.0.1:8080/geoserver](http://127.0.0.1:8080/)

#### 3.5 修改web.xml文件

打开tomcat下webapps\geoserver\WEB-INF目录下的web.xml文件，添加一下内容，重启tomcat即可。

    <filter>  
        <filter-name>CorsFilter</filter-name>  
        <filter-class>org.apache.catalina.filters.CorsFilter</filter-class>  
    </filter>  
    <filter-mapping>  
        <filter-name>CorsFilter</filter-name>  
        <url-pattern>/*</url-pattern>  
    </filter-mapping>
### 4 QGIS

开源桌面GIS

#### 4.1 语言设置

settings-options->override system locale->user interface translation->简体中文

#### 4.2 数据库连接

右键单击PostGIS->New Connection

Host：localhost

数据库：

basic->用户名，密码：postgres,mml

测试连接

OK

双击public里的shp文件,加载文件

图层里右键单击shp文件可查看属性信息

### 5 VScode

前端开发软件

#### 5.1 汉化

安装扩展Chinese,restart重启应用

新建文件夹，右键单击，通过Code打开

#### 5.2 安装浏览器打开插件

open in browser

### 6 openlayers

v5.3.0

### 7 vs

#### 7.1 vs2019 installer

![img](file:///C:\Users\LENOVO\AppData\Roaming\Tencent\QQ\Temp\8LDO48C$8@[GWU0353$FOVS.png)https://mp.weixin.qq.com/s/zfCEfLTYULoOwKqcmkaMsA

ASP.NET和Web开发，.NET桌面开发，Visual Studio扩展开发 ，.NET Core跨平台开发

输入秘钥VS2019企业版：BF8Y8-GN2QH-T84XB-QVY3B-RC4DF

#### 7.2 .NET Core 3.1 SDK

.NET Core跨平台开发 可应用于linux、ios

C:\Program Files\dotnet

### 8 node.js和yarn

#### 8.1 Node.js 

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。

服务端

cmd  node --version : 查看node.js版本

#### 8.2 Yarn

Yarn是facebook发布的一款取代npm的包管理工具

使用npm安装：npm install -g yarn

查看版本：yarn --version

## 二、走进openlayers

### 1 国内外openlayers开发

mapstore

<https://mapstore.geo-solutions.it/mapstore/>

map.geo.admin

[https://map.geo.admin.ch](https://map.geo.admin.ch/)

超图

<https://iclient.supermap.io/examples/openlayers/>

开发包，经封装



例子：水利模型系统

* 模型基本分析

​	压力分析与预测

​	流速分析与预测

​	流向分析与预测

​	流量分析与预测

​	水龄分析与预测

* 模型场景分析

​	路径分析与预测

​	余氯分析与预测

* 模型编辑校准
* 模型方案管理
* 模型文件管理

管网长度、节点数量、网段数量

节点、管线、流量测点、压力测点、水 厂、水泵、水箱、电子地图、影像地图、离线地图

首页 注记、动态渲染

模拟走向、趋势、热力图

污染测试 测试方案、路径追踪  1~24小时的扩散趋势、每一点的污染程度



### 2 什么是openlayers

openlayers遵循bsd许可的开源框架，是丰富的经过高度测试的javascript库。

作为一个javascript库，给我们带来：

1.客户端

兼容性好，几乎支持所有浏览器，为web服务器提供接口服务

2.开发库

openlayers就是一个地图引擎，可以展示渲染资源



### 3 WebGIS映射程序架构

![1610110366238](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\01\WebGIS映射程序架构.png)

### 4 创建我的第一张地图

创建一张地图， 我们需要以下几个步骤: 

1.下载openlayers开发包

2.创建一-个Html网页， 并弓I入openlayers

3:创建图层对象，引入地图资源，ol.Layer

4.创建一-张地图， 用于添加图层对象，ol.Map

5.创建一个视图， 用于定义地图的显示范围，ol.View  

​	设置view的center或extent以及最小缩放和最大缩放级别:minZoom,maxZoom（0-28，一般0-18层）

6.代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的第一张地图</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        .map{
            width: 100%;  
            height: 100%;  
        }
    </style>
</head>
<body>
    <div class="map" id="map"></div>


    <script src="ol/ol.js"></script>
    <script>
        //瓦片图层对象 创建图层对象，引入地图资源
        var osmLayer = new ol.layer.Tile({
            //openstreet 瓦片图层 墨卡托坐标系
            source:new ol.source.OSM() //匿名对象
        });
        //北京经纬度坐标:116.399669,39.921354
        var beijing = ol.proj.transform([116.399669,39.921354],"EPSG:4326","EPSG:3857");
        //console.log(beijing);
        //创建一个视图， 用于定义地图的显示范围
        var view = new ol.View({
            center:beijing,
            zoom:15
        });
        //创建一张地图， 用于添加图层对象
        var map = new ol.Map({
            //绑定id为map的控件
            target:"map",
            layers:[osmLayer],
            view:view
        });
        
    </script>
</body>
</html>
```









## 三、Openlayers关键概念

openlayers是面向对象的。 

面向对象三大特性：封装、继承、多态

面向对象语言：JAVA、C++、PHP、C#、Javascript、Python、Scala...

本章学习内容：

  openlayers核心组件、事件、可观察属性、调试技术



openlayers核心组件

学习openlayers核心组件之前，了解：

  1.类之间的关系

  2.类之间的继承



### 1 核心组件ol.Map

![D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\ol.Map.png](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\ol.Map.png)

 1个ol.Map

* 0个或1个controls 控件集合

   1个controls 控件集合类有0个或n个ol.control.Control控件类对象

* 0个或1个interactions 交互行为集合

  1个 interactions 交互行为集合有0个或n个ol. interactions.Interaction交互类对象，如滚轮缩放MouseWheelZoom、选择Select

* 0个或1个layers图层集合

  1个layers有0个或n个ol.layer.Base图层类对象

* 0个或1个overlays悬浮覆盖物集合

  1个overlays有0个或n个ol.Overlay类对象

* 0个或n个view视图

  1个地图ol.Map只能绑定一个ol.View视图类对象

  

  openlayers code:

  <https://github.com/openlayers/openlayers>

  

  练习代码

  ```html
  <!DOCTYPE html>
  <html lang="en"> 
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>map和它的小伙伴</title>
      <link rel="stylesheet" href="ol/ol.css">
      <style>
          .map{
              width: 100%;
              height: 100%;
              position: absolute;
          }
          .beijing{
              width: 50px;
              height: 30px;
              background: url("flag.jpg") center center no-repeat;
              background-size: 100% 100%;
          }
      </style>
  </head>
  <body>
      <div class="map" id="map"></div>
      <div class="beijing" id="beijing"></div>
      <script src="ol/ol.js"></script>
      <script>
          //创建一个openstreetmap地图图层 
          var osmLayer = new ol.layer.Tile({
              source:new ol.source.OSM()
          });
          //创建一个地图控件
          var control = new ol.control.FullScreen();
          //创建一个视图
          //墨卡托投影代码3857，经纬度WGS84坐标系代码4326
          var beijing = ol.proj.transform([116.399669,39.921354],"EPSG:4326","EPSG:3857");
          var view = new ol.View({
              center:beijing,
              zoom:5,
              maxZoom:10,
              minZoom:2
          });
          //创建一个交互控件
          var interaction = new ol.interaction.DragRotateAndZoom();
          var interactions = new ol.interaction.defaults().extend([interaction]);
          //console.log(interactions);
          //创建一个悬浮控件
          var overlay = new ol.Overlay({
              position:beijing,
              element:document.getElementById("beijing")
          });
          //创建地图
          var map = new ol.Map({
              target:"map",//id
              layers:[osmLayer],
              view:view,
              controls:[control],
              interactions:interactions,
              overlays:[overlay]
          });
          //console.log(map.getInteractions());
      </script>
  </body>
  </html>
  ```




### 2 Console控制台调试 

Elements

Console

Source  前后端交互

ol-debug.js ：调试版的ol.js，未压缩



引入ol-debug.js

在html中加debugger,进行调试

在Source中的代码可以加断点，进行调试

鼠标悬浮在代码中的对象名上可看对象属性

Console中可以写调试代码：

```html
//查看地图的控件
map.getControls();

//对象赋值为默认控件
controls = new ol.control.defaults();

//或：
//var controls = new ol.control.defaults();
//console.log(controls);

//添加控件到地图
controls.forEach(map.addControl,map);

//再查看一下地图的控件
map.getControls();
```



### 3 openlayers中的超类/父类 super classs 

![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\superclass.png)

​																					继承关系

#### 3.1 ol.Observable所有类的基类

方法

on(type, listener,scope) ：注册监听事件，type枚举所有类型，listener监听(function类型)，监听到事件后就会触发监听方法，scope告诉this是谁

once(type, listener,scope) ：只监听一次

un(type, listener,scope) ：注销监听事件，取消监听

unByKey(key)：key事件返回id,通过id将事件注销掉 (老版本)

练习代码：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>map和它的小伙伴</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        .map {
            width: 100%;
            height: 100%;
            position: absolute;
        }

        .beijing {
            width: 50px;
            height: 30px;
            background: url("flag.jpg") center center no-repeat;
            background-size: 100% 100%;
        }
    </style>
</head>

<body>
    <div class="map" id="map"></div>
    <div class="beijing" id="beijing"></div>
    <!-- <script src="ol/ol.js"></script> -->
    <script src="ol/ol-debug.js"></script>

    <script>
        //创建一个openstreetmap地图图层 
        var osmLayer = new ol.layer.Tile({
            source: new ol.source.OSM()
        });
        //创建一个地图控件
        var control = new ol.control.FullScreen();
        //创建一个视图
        //墨卡托投影代码3857，经纬度WGS84坐标系代码4326
        var beijing = ol.proj.transform([116.399669, 39.921354], "EPSG:4326", "EPSG:3857");
        var view = new ol.View({
            center: beijing,
            zoom: 5,
            maxZoom: 10,
            minZoom: 2
        });
        //创建一个交互控件
        var interaction = new ol.interaction.DragRotateAndZoom();
        var interactions = new ol.interaction.defaults().extend([interaction]);
        //console.log(interactions);
        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position: beijing,
            element: document.getElementById("beijing")
        });
        //创建地图
        var map = new ol.Map({
            target: "map",//id
            layers: [osmLayer],
            view: view,
            controls: [control],
            interactions: interactions,
            overlays: [overlay]
        });

        //注册地图移动事件
        // function onMove() {
        //     console.log(this);
        //     console.log(this + "移动了");
        // }
        // var key = map.on("moveend", onMove);
        //注销事件
        // setTimeout(function(){
        //     console.log("移动事件被我注销了");
        //     map.un("moveend",onMove);
        // },3000);
        //map.un("moveend",onMove);

        //老版本注销事件,较新版本已无效
        //map.unByKey(key);

        var MyClass = function(label){
            this.label = label;
            this.onMoveEnd = function(){
                console.log(this.label+"移动了");
            }
        }
        var obj1 = new MyClass("label1");
        var obj2 = new MyClass("label2");
        map.on("moveend", obj1.onMoveEnd,obj1);
        map.on("moveend", obj2.onMoveEnd,obj2);
       
    </script>
</body>

</html>
```



#### 3.2 类ol.Object

Key-Value Observing(KVO)

可观察属性/键值监测

注意：设置button的层级为2 ：z-index: 2; 

练习代码:

```html
<!DOCTYPE html>
<html lang="en"> 
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>object类和KVO</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        /* 消除间隔 */
        *{
            /* 内边距 */
            padding: 0;
            /* 外边距 */
            margin: 0;
        }
        .map{
            width: 100%;
            height: 100%;
            position: absolute;
        }
        .beijing{
            width: 50px;
            height: 30px;
            background: url("flag.jpg") center center no-repeat;
            background-size: 100% 100%;
        }
        .showLayer{
           position: absolute;
            /* 设置层级为2 */
           z-index: 2; 
        }
    </style>
</head>
<body>
    <div class="map" id="map">
        <input type="button" value="图层属性观察" onclick="showLayer()" class="showLayer">
    </div>
    <div class="beijing" id="beijing"></div>
    <!-- <script src="ol/ol.js"></script> -->
    <script src="ol/ol-debug.js"></script>

    <script>
        //创建一个openstreetmap地图图层 
        var osmLayer = new ol.layer.Tile({
            source:new ol.source.OSM()
        });
        //创建一个地图控件
        var control = new ol.control.FullScreen();
        //创建一个视图
        //墨卡托投影代码3857，经纬度WGS84坐标系代码4326
        var beijing = ol.proj.transform([116.399669,39.921354],"EPSG:4326","EPSG:3857");
        var view = new ol.View({
            center:beijing,
            zoom:5,
            maxZoom:10,
            minZoom:2
        });
        //创建一个交互控件
        var interaction = new ol.interaction.DragRotateAndZoom();
        var interactions = new ol.interaction.defaults().extend([interaction]);
        //console.log(interactions);
        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:beijing,
            element:document.getElementById("beijing")
        });
        //创建地图
        var map = new ol.Map({
            target:"map",//id
            layers:[osmLayer],
            view:view,
            controls:[control],
            interactions:interactions,
            overlays:[overlay]
        });
        //console.log(map.getInteractions());
        
        function showLayer(){
            //console.log(osmLayer.getProperties());

            // if(osmLayer.getVisible()){
            //     osmLayer.setVisible(false);
            // }else{
            //     osmLayer.setVisible(true);
            // }

            //osmLayer.setOpacity(0.5);

            osmLayer.set("####","一个openstreetmap",false);//true不触发属性
        }

        //change:visible
        osmLayer.on("change:visible",function(e){
            var visible = this.getVisible();
            if(visible){
                console.log("图层显示");
            }else{
                console.log("图层隐藏");
            }
        });

        //propertychange
        osmLayer.on("propertychange",function(e){
            console.log("图层某个属性发生改变");
            console.log(e);//ol.Object.Event 属性改变前后的值
        });
    </script>
</body>
</html>
```



#### 3.3 类ol.Collection

![Collection](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\Collection.png)

​                                                                              ol.Collection





在Console中调试：

```html
//1.扩展控件
map.getControls().extend([new ol.control.FullScreen()]);
//2.查看控件集合
map.getControls().getArray();
//3.清空地图控件
map.getControls().clear();
//4.实例化Collection
var collection = new ol.Collection([new ol.control.FullScreen()]);
//5.添加控件
collection.forEach(map.addControl,map);
//6.查看
collection.getArray();
```

练习代码:

```html
<!DOCTYPE html>
<html lang="en"> 
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Collection类</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        .map{
            width: 100%;
            height: 100%;
            position: absolute;
        }
        .beijing{
            width: 50px;
            height: 30px;
            background: url("flag.jpg") center center no-repeat;
            background-size: 100% 100%;
        }
    </style>
</head>
<body>
    <div class="map" id="map"></div>
    <div class="beijing" id="beijing"></div>
    <!-- <script src="ol/ol.js"></script> -->
    <script src="ol/ol-debug.js"></script>

    <script>
        //创建一个openstreetmap地图图层 
        var osmLayer = new ol.layer.Tile({
            source:new ol.source.OSM()
        });
       
        //创建一个视图
        //墨卡托投影代码3857，经纬度WGS84坐标系代码4326
        var beijing = ol.proj.transform([116.399669,39.921354],"EPSG:4326","EPSG:3857");
        var view = new ol.View({
            center:beijing,
            zoom:5,
            maxZoom:10,
            minZoom:2
        });

        //创建一个交互控件
        var interaction = new ol.interaction.DragRotateAndZoom();
        var interactions = new ol.interaction.defaults().extend([interaction]);

        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:beijing,
            element:document.getElementById("beijing")
        });

        //创建地图
        var map = new ol.Map({
            target:"map",//id
            layers:[osmLayer],
            view:view,
            interactions:interactions,
            overlays:[overlay]
        });
     
        //监听地图控件集合长度变化
        map.getControls().on("change:length",function(e){
            console.log(e);
            console.log("地图控件集合长度发生了变化");
        });

        //监听地图控件集合属性变化
        map.getControls().on("propertychange",function(e){
            console.log(e);
            console.log("地图控件集合发生了变化");
        });
    </script>
</body>
</html>
```



## 四、走进地图对象Map



学习内容：

什么是Map类

Map类的常用参数

创建自己的代码段：加快自己的开发速度

Map的渲染引擎

Map的事件

Map的可观察属性

Map的主要方法



  Map其实就是整个Openlayers的核心，更大的说，它是整个WebGIS前端的核心。我们需要使用它来管理我们的Layer、Control、Interaction、Overlay、View等这些组件。所以说我们不管做任何事，都需要让他更Map联系起来。Map就是核心。

![D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\ol.Map.png](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\02\ol.Map.png)



### 1 Map的常用参数



![Map的常用参数](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\05\Map的常用参数.png)



练习代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Map的参数</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .map{
            width: 100%;
            height: 100%;
            position: absolute;
        }
        #wjx{
            width: 32px;
            height: 32px;
            background: url("wjx.png") center center no-repeat;
            background-size: 100% 100%;
        }
    </style>
</head>
<body>
    <div class="map" id="map"></div>
    <div id="wjx"></div>
    <script src="ol/ol-debug.js"></script>
    <script>
        //1.加载openstreet图层
        var osmLayer = new ol.layer.Tile({
            source: new ol.source.OSM() 
        });

        //定义地图中心
        var beijing = ol.proj.transform([116.399669,39.921354],"EPSG:4326","EPSG:3857");
        //2.创建视图
        var view = new ol.View({
            center:beijing,
            zoom:10,
            maxZoom:15,
            minZoom:2
        });
        //3.创建地图控件
        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //4.创建交互控件
        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //5.创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:beijing,
            element:document.getElementById("wjx")
        });

        //创建地图
        var map = new ol.Map({
            target:"map",
            layers:[osmLayer],
            view:view,
            overlays:[overlay],
            controls:controls,
            interactions:interactions,
            moveTolerance:100
        });
    </script>
</body>
</html>
```



### 2 VSCode创建自己的代码段

在线HTML代码转换为JavaScript字符串工具：

<http://tools.jb51.net/transcoding/html2js/>

文件-首选项-用户代码片段

输入html  回车

参照所给示例，在花括号里添加自己的代码片段，如：



```html
//地图代码片段
	"gomap": {
		//快捷键
		"prefix": "gomap",
		"body": [
			"<!DOCTYPE html>",
			"<html lang=\"en\">",
			"<head>",
			"    <meta charset=\"UTF-8\">",
			"    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">",
			"    <title>Map的参数</title>",
			"    <link rel=\"stylesheet\" href=\"ol/ol.css\">",
			"    <style>",
			"        *{",
			"            padding: 0;",
			"            margin: 0;",
			"        }",
			"        .map{",
			"            width: 100%;",
			"            height: 100%;",
			"            position: absolute;",
			"        }",
			"        #wjx{",
			"            width: 32px;",
			"            height: 32px;",
			"            background: url(\"wjx.png\") center center no-repeat;",
			"            background-size: 100% 100%;",
			"        }",
			"    </style>",
			"</head>",
			"<body>",
			"    <div class=\"map\" id=\"map\"></div>",
			"    <div id=\"wjx\"></div>",
			"    <script src=\"ol/ol.js\"></script>",
			"    <script>",
			"        //加载openstreet图层",
			"        var osmLayer = new ol.layer.Tile({",
			"            source: new ol.source.OSM() ",
			"        });",
			"        //定义地图中心",
			"        var beijing = ol.proj.transform([116.399669,39.921354],\"EPSG:4326\",\"EPSG:3857\");",
			"        //创建视图",
			"        var view = new ol.View({",
			"            center:beijing,",
			"            zoom:8,",
			"            maxZoom:15,",
			"            minZoom:2",
			"        });",
			"        //创建地图控件",
			"        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);",
			"        //创建交互控件",
			"        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);",
			"        //创建一个悬浮控件",
			"        var overlay = new ol.Overlay({",
			"            position:beijing,",
			"            element:document.getElementById(\"wjx\")",
			"        });",
			"        //创建地图",
			"        var map = new ol.Map({",
			"            target:\"map\",",
			"            layers:[osmLayer],",
			"            view:view,",
			"            overlays:[overlay],",
			"            controls:controls,",
			"            interactions:interactions,",
			"            //moveTolerance:100",
			"        });",
			"    </script>",
			"</body>",
			"</html>"
		],
		"description": "我的地图片段"
	}
```



### 3 Map的渲染器



#### Canvas

​	canvas是所有现代web浏览器都支持的高性能2D绘图引擎，但它不支持3D渲染，所以说在WebGL普及之前，我们都是用Canvas。

![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\05\canvas.png)



#### WebGL

​	WebGL一个3D引擎，虽然说听起来很厉害，但是现在没有完全普及，它对使用环境有要求，用户的计算机必须有能够支持它的显卡和软件驱动程序。同时浏览器也有要求，IE10版本之前根本不提供WebGL支持，目前基本上只有谷歌Chrome、Safari和Firefox支持。



#### DOM

​	通过HTML的DOM元素绘图，可以支持IE8这些老浏览器。但是基本上如果你不用老浏览器的话，就不会想用上这个技术。



openlayers v5.3.0 API 下

(Observable-Object-)PluggableMap有一个WebGLMap子类



### 4 Map的事件



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\05\Map的事件.png)

```assembly
change (module: o1/ events / Event- Event) 

-通用更改事件。当修订计数器增加时触发。

change:layerGroup (module: ol/ object objectEvent)

change:size (module: o1/ object objectEvent)

change:target (module: ol/ object objectEvent)

change:view (module: o1/ object objectEvent)

click (module: o1/ MapBrowserEvent-MapBrowserEvent) 

-没有拖动的点击。双击将触发其中两个。

dblclick (module: ol/ MapBrowserEvent-MapBrowserEvent) 

-真正的双击，没有拖动。

moveend (module: ol/ MapEvent-MapEvent) 

-移动地图后触发。

movestart (module: ol/ MapEvent-MapEvent) 

-地图开始移动时触发。

pointerdrag (module: o1/ MaprowserEvent-MaprowserEvent) 

-拖动指针时触发。

pointermove (module: o1/ MaprowserEvent-MaprowserEvent) 

-移动指针时触发。请注意，在触摸设备上，这是在平移地图时触发的，因此与mousemove不同。

postcompose (module: ol/ render/ Event-RenderEvent)

postrender (module: o1/ MapEvent-MapEvent) 

-渲染地图框后触发。

precompose  (module: ol/ render/ Event-RenderEvent)

propertychange (module: ol / Object ObjectEvent) 

-更改属性时触发。

rendercomplete (module: ol/ render/ Event-RenderEvent)

-渲染完成时触发，即所有源和平铺已完成前视口的加载，并且所有平铺都已淡入。

singleclick (module: ol / MapBrowserEvent-MapBrowserEvent)

 -真正的单击，没有拖动，也没有双击。请注意，此事件延迟250毫秒， 以确保它不是双击。
```



### 5 Map的可观察属性



| 名称         | 类型                                                         | 可设定 | [ol / Object.ObjectEvent](https://openlayers.org/en/latest/apidoc/module-ol_Object.ObjectEvent.html)类型 | 描述                              |
| ------------ | ------------------------------------------------------------ | ------ | ------------------------------------------------------------ | --------------------------------- |
| `layerGroup` | [模块：ol / layer / Group〜LayerGroup](https://openlayers.org/en/latest/apidoc/module-ol_layer_Group-LayerGroup.html) | 是     | `change:layergroup`                                          | 包含此地图中的图层的图层组。      |
| `size`       | [模组：ol / size〜Size](https://openlayers.org/en/latest/apidoc/module-ol_size.html#~Size) \| 未定义 | 是     | `change:size`                                                | DOM中地图的大小（以像素为单位）。 |
| `target`     | HTMLElement \| 串 \| 未定义                                  | 是     | `change:target`                                              | 渲染地图的元素或元素的ID。        |
| `view`       | [模块：ol / View〜View](https://openlayers.org/en/latest/apidoc/module-ol_View-View.html) | 是     | `change:view`                                                | 控制此地图的视图。                |



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\05\Map的可观察属性英文版.png)



天地图注册登录，控制台申请成为个人开发者

新建应用，获取key(浏览器端)

我的key：513a3fdc4cb956a973d63e59ec688f49



练习代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Map的参数</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .map{
            width: 50%;
            height: 100%;
            position: absolute;
        }
        .map1{
            width: 50%;
            margin-left: 50%;
            height: 100%;
            position: absolute;
        }
        #wjx{
            width: 32px;
            height: 32px;
            background: url("wjx.png") center center no-repeat;
            background-size: 100% 100%;
        }
        .change{
            z-index: 2;
            position: absolute;
        }
    </style>
</head>
<body>
    <input type="button" value="改变地图绑定控件" class="change" onclick="change()"> 
    <div class="map" id="map"></div>
    <div class="map1" id="map1"></div>
    <div id="wjx"></div>
    <script src="ol/ol.js"></script>
    <script>
        //加载openstreet图层 墨卡托投影
        // var osmLayer = new ol.layer.Tile({
        //     source: new ol.source.OSM() 
        // });
        //WGS84投影 天地图
        var tdtmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=vec_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        var zjmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=cva_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        //设置投影
        var projection = new ol.proj.Projection({
            code:"EPSG:4326",
            units:"degrees"
        });
        //创建视图
        var view = new ol.View({
            projection:projection,
            center:[116.40,39.92],
            zoom:8,
            maxZoom:15,
            minZoom:2
        });
        //创建地图控件
        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //创建交互控件
        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:[116.40,39.92],
            element:document.getElementById("wjx")
        });
        //创建地图
        var map = new ol.Map({
            target:"map",
            layers:[tdtmap,zjmap],
            view:view,
            overlays:[overlay],
            controls:controls,
            interactions:interactions,
            //moveTolerance:100
        });

        map.on("movestart",function(e){
            console.log(e);
            console.log("移动开始");
        });
        map.on("moveend",function(e){
            console.log(e);
            console.log("移动结束");
        });

        function change(){
            //获取地图当前绑定的div
            var target = map.getTarget();
            if(target == "map"){
                map.setTarget("map1");
            }else{
                map.setTarget("map");
            }
        }
        map.on("change:target",function(e){
            console.log(e);
            console.log("地图绑定的容器改变");
        });
    </script>
</body>
</html>
```



### 6 Map的主要方法



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\05\Map的主要方法.png)



将加载显示天地图的代码模板添加到用户代码片段里，方便开发使用



练习代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>地图的渲染</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .map{
            width: 100%;
            height: 100%;
            position: absolute;
        }
        #wjx{
            width: 32px;
            height: 32px;
            background: url("wjx.png") center center no-repeat;
            background-size: 100% 100%;
        }
        .onMove{
            z-index: 2;
            position: absolute;
        }
    </style>
</head>
<body>
    <input type="button" value="移动地图" class="onMove" onclick="onMove()">
    <div class="map" id="map"></div>
    <div id="wjx"></div>
    <script src="ol/ol.js"></script>
    <script>
        //WGS84投影 天地图CSGS2000
        var tdtmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=vec_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        var zjmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=cva_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        //设置投影
        var projection = new ol.proj.Projection({
            code:"EPSG:4326",
            units:"degrees"
        });
        //创建视图
        var view = new ol.View({
            projection:projection,
            center:[116.40,39.92],
            zoom:8,
            maxZoom:15,
            minZoom:2
        });
        //创建地图控件
        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //创建交互控件
        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:[116.40,39.92],
            element:document.getElementById("wjx")
        });
        //创建地图
        var map = new ol.Map({
            target:"map",
            view:view,
            layers:[tdtmap,zjmap],
            //overlays:[overlay],
            controls:controls,
            interactions:interactions,
            //moveTolerance:100
        });
      
        function onMove(){
            var mapdom = document.getElementById("map");
            mapdom.style.width = 500 + "px";
            //强制更新地图大小，不加地图会变形
            map.updateSize();

            // var view = map.getView();
            // var center = view.getCenter();
            // center[0] -= 0.1;
            // view.setCenter(center);
            // //地图渲染后才能移动
            //map.render();//加载数据完再渲染
            // //map.renderSync();//立即渲染
        }


        map.on("click",function(e){
            console.log(e);
            var coord = e.coordinate;
            var pixel = e.pixel;
            console.log(coord);
            //四个转换方法
            //getCoordinateFromPixel(pixel)
            console.log(map.getCoordinateFromPixel(pixel));
            //getEventCoordinate(event))
            console.log(map.getEventCoordinate(e.pointerEvent));
            console.log(pixel);
            //getCoordinateFromPixel(pixel)
            console.log(map.getPixelFromCoordinate(coord));
            //getEventPixel(event))
            console.log(map.getEventPixel(e.pointerEvent));
            //遍历点击像素位置存在的要素
            map.forEachFeatureAtPixel(pixel,function(e){
                console.log(e);
            });
            //遍历点击像素位置存在的矢量图层，瓦片图层遍历不了，会报错
            map.forEachLayerAtPixel(pixel,function(e){
                console.log(e);
            });
        });

        //创建矢量图层
        var vectorSource = new ol.source.Vector();
        var vectorLayer = new ol.layer.Vector({
            source:vectorSource,
            style:new ol.style.Style({
                //图片样式
                image:new ol.style.Icon({
                    size:[64,64],
                    src:"wjx.png"
                })
            })
        });
        //Get the element that serves as the map viewport
        //获取dom元素
        console.log(map.getViewport());
        //创建图层要素
        var feature = new ol.Feature({
            //几何体 点要素
            geometry:new ol.geom.Point([116.40,39.92])
        });
        //添加要素
        vectorSource.addFeature(feature);
        //把图层添加到地图中
        map.addLayer(vectorLayer);
    </script>
</body>
</html>
```





## 五、地图视图管理View

学习内容：

坐标系统及投影简介

View对象的主要组成部分

View对象的主要参数

View对象的可观察属性

View对象的方法

示例：视图联动



### 1 坐标系统及投影简介



参考文献：

[1]汤国安.地理信息系统教程[M].北京：高等教育出版社，2007.



#### 1.1 坐标系统



地理空间坐标系统

a.球面坐标系统

天文地理坐标系

大地地理坐标系

空间直角坐标系

b.平面坐标系统(投影坐标系统)

高斯平面直角坐标系

地方独立平面直角坐标系

...



大地(地理)坐标系:

以地球椭球为依据

大地本初子午面：球心、英国伦敦格林尼治天文台所在面

大地经度(L)、大地纬度(B)



参心大地坐标系：

​	以参考椭球中心为坐标原点。

地心大地坐标系：

​	地球椭球中心与地球质心重合，椭球短轴与地球自转轴重合。



北京54与西安80是参心大地坐标系，单位是经纬度。

北京54坐标原点在前苏联的普尔科沃。西安80坐标原点在陕西省泾阳县永乐镇。

WGS84与国家2000(CSGS2000)是地心大地坐标系，单位是经纬度。WGS84投影代号:EPSG4326。

WGS84坐标：美国国防部研制确定的，GPS定位得到的坐标就是该坐标系。2000国家大地坐标系：国产地心坐标系，与国际接轨，目前全国全面推广使用。

openstreetmap 的瓦片图层是墨卡托直角坐标系，单位是m。墨卡托投影默认代号:EPSG3857



#### 1.2 投影



高斯-克吕格投影：

​	横轴等角切圆柱投影.

​	在同一条经线上长度变形随纬度降低而增大，赤道处最大.

​	在同一纬线上长度变形随经差的增大而增大，且增大速度较快.

​	在纬度30°以下6°带边缘区长度变形值超过了1/1000.

​	适合幅员广大的国家和地区，我国基本比例尺数学基础.



横轴墨卡托投影(UTM)：

​	横轴等角割圆柱投影.	

​	圆柱面在84°N和84°S处与椭球体相割.

​	在6°带内最大长度变形不超过0.04%.

​	国际较通用，主要用于全球经度自84°N~80°S之间地区的制图.



### 2 视图对象View



#### 2.1 初步了解View

center

resolution

rotation

projection



#### 2.2 View的基本参数

| **参数**          | **类型**                                                     | **默认值**  |
| ----------------- | ------------------------------------------------------------ | ----------- |
| center            | [module:ol/coordinate~Coordinate](https://openlayers.org/en/latest/apidoc/module-ol_coordinate.html) |             |
| constrainRotation | boolean \| number                                            | TRUE        |
| enableRotation    | boolean                                                      | TRUE        |
| extent            | [module:ol/extent~Extent](https://openlayers.org/en/latest/apidoc/module-ol_extent.html) |             |
| maxResolution     | number                                                       |             |
| minResolution     | number                                                       |             |
| maxZoom           | number                                                       | 28          |
| minZoom           | number                                                       | 0           |
| projection        | [module:ol/proj~ProjectionLike](https://openlayers.org/en/latest/apidoc/module-ol_proj.html) | 'EPSG:3857' |
| resolution        | number                                                       |             |
| resolutions       | Array.<number>                                               |             |
| rotation          | number                                                       | 0           |
| zoom              | number                                                       |             |
| zoomFactor        | number                                                       | 2           |



| 描述                                                         |
| ------------------------------------------------------------ |
| center：视图的初始中心。使用projection选项指定中心的坐标系。如果未设置图层源，则不会获取图层源，但可以稍后设置中心#setCenter。 |
| constrainRotation：旋转约束。 false意味着没有约束。true意味着没有约束，但在零附近捕捉零。数字将旋转约束为该数量的值。例如，4将旋转约束为0度，90度，180度和270度。 |
| enableRotation：启用旋转。默认为true。如果设置旋转约束为false，将会设置旋转的值为0。如果enableRotation设置为false，constrainRotation选项没有任何作用。 |
| extent：限制中心的程度，换句话说，中心不能设置在这个范围之外。 |
| maxResolution：用于确定分辨率约束的最大分辨率。它与minResolution（或maxZoom）和zoomFactor。一起使用。如果未指定，则以投影的有效范围适合256x256像素图块的方式计算。如果投影是Spherical   Mercator（默认值），则maxResolution默认为40075016.68557849 / 256 =   156543.03392804097。 |
| minResolution：用于确定分辨率约束的最小分辨率。它与maxResolution（或minZoom）和zoomFactor。一起使用。如果未指定，则假设29个缩放级别（系数为2）进行计算。如果投影是Spherical   Mercator（默认值），则minResolution默认为40075016.68557849 / 256 / Math.pow(2, 28) = 0.0005831682455839253。 |
| maxZoom：用于确定分辨率约束的最大缩放级别。它与minZoom（或maxResolution）和zoomFactor。一起使用。请注意，如果minResolution还提供了，则优先于maxZoom。 |
| minZoom：用于确定分辨率约束的最小缩放级别。它与maxZoom（或minResolution）和zoomFactor。一起使用。请注意，如果maxResolution还提供了，则优先于minZoom。 |
| projection：投影。默认为球形墨卡托。                         |
| resolution：视图的初始分辨率。单位是projection每像素的单位（例如，每像素米）。设置此选项的另一种方法是设置zoom。如果既未zoom定义也未定义，则不会获取图层源，但可以稍后使用#setZoom或设置它们#setResolution。 |
| resolutions：决定解决方案约束的决议。如果设置了，maxResolution，minResolution，minZoom，maxZoom，和zoomFactor选项都将被忽略。 |
| rotation：以弧度为单位的视图的初始旋转（顺时针正向旋转，0表示向北）。 |
| zoom：仅在resolution未定义时使用。用于计算视图初始分辨率的缩放级别。使用该#constrainResolution方法确定初始分辨率。 |
| zoomFactor：用于确定分辨率约束的缩放系数。                   |



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\06\View的主要参数.png)



原表格见openlayers官网:

<https://openlayers.org/en/latest/apidoc/module-ol_View-View.html>

new View(opt_options)



#### 2.3 View的可观察属性



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\06\View的可观察属性.png)



#### 2.4 View的主要方法



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\06\View的主要方法.png)

v5.3.0的ol/View有rotate方法，在v6.5.0中，ol/View没有rotate方法。



练习代码：



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>View视图管理</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .map{
            width: 100%;
            height: 100%;
            position: absolute;
        }
        #wjx{
            width: 32px;
            height: 32px;
            background: url("wjx.png") center center no-repeat;
            background-size: 100% 100%;
        }
    </style>
</head>
<body>
    <div class="map" id="map"></div>
    <div id="wjx"></div>
    <script src="ol/ol-debug.js"></script>
    <script>
        //WGS84投影 天地图CSGS2000
        var tdtmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=vec_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        var zjmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=cva_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        //设置投影
        var projection = new ol.proj.Projection({
            code:"EPSG:4326",
            units:"degrees"
        });
        //创建视图
        var view = new ol.View({
            projection:projection,
            //center必须要设
            center:[104.06, 30.66],
            //地图显示范围，移动地图移不出此范围
            //extent:[103.95, 30.60,104.20, 30.74],
            //zoom:8,
            //精细化控制视图分辨率大小
            resolution:0.00025,
            //旋转约束,设为4时,可旋转4个角度:0°,90°,180°,270°
            constrainRotation:4,
            //enableRotation:false,
            //rotation:1.57,
            //maxResolution:0.0015,
            //minResolution:0.00015,
            // maxZoom:15,
            // minZoom:2
        });
        //创建地图控件
        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //创建交互控件
        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //创建一个悬浮控件
        var overlay = new ol.Overlay({
            position:[116.40,39.92],
            element:document.getElementById("wjx")
        });
        //创建地图
        var map = new ol.Map({
            target:"map",
            view:view,
            layers:[tdtmap,zjmap],
            overlays:[overlay],
            controls:controls,
            interactions:interactions,
            //moveTolerance:100
        });
      
        view.on("change:resolution",function(e){
            console.log(e);
        });

        map.on("click",function(e){
            var coord = e.coordinate;
            // console.log(e);
            console.log(coord);
        });

        view.rotate(1.57,[104.06, 30.66]);
    </script>
</body>
</html>
```



#### 2.5 View的视图联动



两个地图可以共用视图View，但不同共用Control和Interaction



![View的视图联动](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\06\View的视图联动.png)



练习代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>map</title>
    <link rel="stylesheet" href="ol/ol.css">
    <style>
        *{
            padding: 0;
            margin: 0;
        }
        .map{
            width: 50%;
            height: 100%;
            position: absolute;
        }
        .map1{
            width: 50%;
            height: 100%;
            position: absolute;
            margin-left: 50%;
        }
    </style>
</head>
<body>
    <div class="map" id="map"></div>
    <div class="map1" id="map1"></div>
    <script src="ol/ol-debug.js"></script>
    <script>
        //WGS84投影 天地图CSGS2000
        var tdtmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=vec_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        var zjmap = new ol.layer.Tile({
            source:new ol.source.XYZ({
                url:"http://t4.tianditu.com/DataServer?T=cva_w&x={x}&y={y}&l={z}&tk=513a3fdc4cb956a973d63e59ec688f49"
            })
        });
        //设置投影
        var projection = new ol.proj.Projection({
            code:"EPSG:4326",
            units:"degrees"
        });
        //创建视图
        var view = new ol.View({
            projection:projection,
            center:[116.40,39.92],
            zoom:10,
            maxZoom:15,
            minZoom:2
        });
        //创建地图控件
        var controls = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //创建交互控件
        var interactions = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //创建地图控件
        var controls1 = new ol.control.defaults().extend([new ol.control.FullScreen()]);
        //创建交互控件
        var interactions1 = new ol.interaction.defaults().extend([new ol.interaction.DragRotateAndZoom()]);
        //创建地图
        var map = new ol.Map({
            target:"map",
            view:view,
            layers:[tdtmap,zjmap],
            controls:controls,
            interactions:interactions,
            //moveTolerance:100
        });
        
        var map1 = new ol.Map({
            target:"map1",
            view:view,
            layers:[tdtmap,zjmap],
            controls:controls1,
            interactions:interactions1,
            //moveTolerance:100
        });
    </script>
</body>
</html>
```



## 六、走进图层

学习内容：

GIS数据类型

Layer对象的架构

Source对象的架构

各种栅格图层的加载演示

栅格切片的发布



### 1 图层的基本概念



#### 1.1 空间数据



栅格数据

栅格数据是由按照行和列排列组织的一些像元集合，每一个像元都包含了信息值，可以是航片，卫星影像，数字图片等等。

矢量数据

矢量数据结构是对矢量数据模型进行数据的组织。通过记录实体坐标及其关系，尽可能精确地表现点、线、多边形等地理实体，坐标空间设为连续，允许任意位置、长度和面积的精确定义。矢量数据结构直接以几何空间坐标为基础，记录取样点坐标。

![矢量数据vs栅格数据](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\矢量数据vs栅格数据.png)





#### 1.2 Layer的架构



![Layer的架构](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\Layer的架构.png)





Openlayers v6.5.0 API中Layer下类的继承关系：

![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\ol.layer.Layer1.png)





layer文件夹下的文件

<https://github.com/openlayers/openlayers/tree/main/src/ol/layer>



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\layer文件夹下的文件.png)



#### 1.3 Layer的Source架构



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\Source架构2.png)





#### 1.4 OGC标准



OGC

OGC 全称是开放地理空间信息联盟(Open Geospatial Consortium),是一个非盈利的国际标准组织，它制定了数据和服务的一系列标准，GIS厂商按照这个标准进行开发可保证空间数据的互操作。





![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\OGC标准.png)





网络覆盖服务 (WCS)

提供的是包含了地理位置信息或属性的空间栅格图层                                                                            1.GetCapabilities（获取服务的元信息）

2.DescribeCoverage（获取Coverage的描述信息）

3.GetCoverage（获取Coverage）



网络地图服务 (WMS)

能够根据用户的请求返回相应的地图（包括PNG，GIF，JPEG等栅格形式或者是SVG和WEB CGM等矢量形式）

1.GetCapabilities（获取服务中的要素类及支持的操作）

2.GetMap（获取地图）

3.GetFeatureInfo（根据地图上的像素点获取更详细的要素信息，类似 Identify 功能） 



网络要素服务(WFS) 

即Web要素服务，支持对地理要素的插入，更新，删除，检索和发现服务                                                1.GetCapabilities（获取服务中的要素类及支持的操作）

2.DescribeFeatureType（描述要素类的信息）

3.GetFeature（获取要素）

4.GetGmlObject（通过 XLink 获取 GML 对象）

5.Transaction（创建、更新、删除数据的事务操作）

6.LockFeature（在事务过程中锁定要素）



网络地图切片服务(WMTS) 

切片服务



#### 1.5 瓦片的结构



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\瓦片的结构.png)





### 2 栅格图层加载方式



![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\ol.layer.XYZ.png)

一个关于OpenLayers 3使用的入门教程：

<https://github.com/anzhihun/OpenLayers3Primer/>



图层加载有关内容：

<https://github.com/anzhihun/OpenLayers3Primer/tree/master/ch05/05-02.md>



OSM图层加载：



```
var osmLayer = new ol.layer.Tile({
            source: new ol.source.OSM({
                url: 'http://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png'
            }) 
        });
```



报错：

![](D:\Core\最近学习\WebGIS\开源架构Webgis解决方案开发指南（2019年新课）\notes\img\07\OSM报错.png)



而把ol.source.OSM改为ol.source.XYZ时成功

```HTML
var osmLayer = new ol.layer.Tile({
            source: new ol.source.XYZ({
                url: 'http://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png'
            }) 
        });
```

