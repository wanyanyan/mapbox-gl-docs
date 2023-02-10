# Mapbox GL JS

当前版本：`v2.12.0` [更新日志](https://github.com/mapbox/mapbox-gl-js/blob/main/CHANGELOG.md)

- 自定义地图样式
- 快速创建矢量地图
- 兼容其他Mapbox工具

**Mapbox GL JS**是一个使用Mapbox现代化的制图技术来创建网络地图和网络应用的JavaScript库。你可以使用Mapbox GL JS在Web浏览器或者客户端来显示Mapbox地图、添加用户交互以及自定义地图样式。

## 使用案例

Mapbox GL JS的用例包括：

- 地理数据可视化和动画效果
- 在地图上动态查询或过滤要素
- 将你的数据放在地图上
- 在地图上动态展示客户端的数据，或者自定义数据的展现形式
- 3D数据可视化以及动画效果
- 使用程序在地图上添加弹窗或标记

更多实际案例可以查看[使用教程](https://docs.mapbox.com/help/tutorials/?product=Mapbox+GL+JS)，[官方示例](https://docs.mapbox.com/mapbox-gl-js/example/)，以及[用户案例](https://www.mapbox.com/showcase)。

## 关键概念

### Mapbox GL

Mapbox GL中的“GL”是指一个可以使用OpenGL技术在任何兼容的浏览器上渲染二维或三维地图的图形库，不需要借助任何插件。

### 客户端渲染

Mapbox GL JS依赖于客户端渲染，Mapbox地图是将矢量瓦片按照指定的样式规则在客户端动态渲染的，而不是在服务器端渲染的。这就使得我们可以根据用户的交互随意切换地图的样式，或者动态展示后端响应的数据。

### `Map`类

`mapboxgl.Map`类是每一个Mapbox GL JS项目最基本的类，下面的示例代码展示了你要显示一个地图所用的最少的代码。

```js
mapboxgl.accessToken = '<your access token here>';
const map = new mapboxgl.Map({
  container: 'map', // container ID
  style: 'mapbox://styles/mapbox/streets-v12', // style URL
  center: [-74.5, 40], // starting position [lng, lat]
  zoom: 9 // starting zoom
});
```

- **accessToken**： 用来关联你的账户下创建的地图
- **container**：放置地图的HTML标签。上面的示例中使用的是id为`map`的div标签
- **style**：地图样式文件，用来描述地图上所用到的瓦片集，以及这些瓦片集用什么样的符号进行可视化。
- **center**：地图初始化时的位置坐标，格式为[经度，纬度]
- **zoom**：地图初始化时的级别，可以是整数也可以是小数

### 图层

Mapbox地图由一系列图层组成，每个图层都提供了在浏览器渲染指定数据的渲染规则，渲染器使用这些图层将地图绘制到屏幕上。

Mapbox GL JS引擎中的`addLayer`方法可以向地图上添加一个样式图层。这个方法只需要一个唯一的参数，那就是描述这个图层的对象。也可以给它一个`beforeId`的参数，指定一个已经存在的图层ID，将新的图层插入到指定的这个图层前面。如果没指定`beforeId`，渲染器就会将新的图层绘制到地图的最上面。以下部分描述了图层对象所包含的属性。

**异步**

由于Mapbox渲染通常是异步的，因此我们在代码中通常采用事件绑定的方式，在合适的时候添加图层。例如：

```js
map.on('load', () => {
  map.addLayer({
    id: 'terrain-data',
    type: 'line',
    source: {
        type: 'vector',
        url: 'mapbox://mapbox.mapbox-terrain-v2'
    },
    'source-layer': 'contour'
  });
});
```

以上方法通过监听地图的`load`事件，来确保只有当地图的所有资源（包括样式）都加载完成后才会调用`map.addLayer`。

**图层数据源**

当添加图层时，必须指定该图层所使用的数据源。数据源包含一个`type`属性和一个`url`，除了GeoJSON数据源没有`url`以外。一共有6种类型的数据源，每类数据源都有其自己的一些属性：

