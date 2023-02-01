# Map

`Map`对象用来在你的页面上创建底图实例，地图实例会暴露出一些方法和属性，用来通过程序来对地图进行操作，同时也会触发一些事件用来进行用户交互。

创建地图实例需要指定一个地图容器`container`以及一些其他必要的选项。Mapbox GL JS根据你提供的这些选项在页面上初始化地图，并返回这个地图的实例。

`Map`类继承自[Evented](/api/evented.md)

```js
new Map class(options: Object)
```

## 参数

**options** `(Object)`

|  属性名   | 描述  |
|  ----  | ----  |
| **options.accessToken** `string` <br>默认值：`null` | 如果指定了这个属性，地图会替换在`mapboxgl.accessToken`中设置的Token |
| **options.antialias** `boolean` <br>默认值：`false`  | 如果设置为`true`，会使用[MSAA antialiasing](https://en.wikipedia.org/wiki/Multisample_anti-aliasing)来创建gl上下文，对自定义图层抗锯齿会很有用。默认情况下该属性值为`false`，以提高渲染性能 |
| **options.attributionControl** `boolean` <br>默认值：`true`  | 如果设置为`true`，将会在地图上创建一个[AttributionControl](/api/markers?id=AttributionControl)控件 |
| **options.bearing** `number` <br>默认值：`0`  | 地图初始的旋转角度，从北方向开始，逆时针进行计算，单位为度。如果在地图构造函数的选项中没有指定`bearing`，Mapbox GL JS将会去地图的样式文件中查找，如果样式文件也没有指定，那么将会设置为默认值`0` |
| **options.bearingSnap** `number` <br>默认值：`7`  | 捕获阈值，单位为度，地图旋转角度小于这个阈值的时候，地图将会自动重置到北方向。 |
| **options.bounds** `LngLatBoundsLike` <br>默认值：`null`  | 地图初始化时显示的经纬度范围，如果设置了`bounds`，将会忽略`center`和`zoom`选项 |
| **options.boxZoom** `boolean` <br>默认值：`true`  | 如果设置为`true`，"box zoom"交互将会被启用（详情查看[BoxZoomHandle](/api/handlers?id=BoxZoomHandle)） |
| **options.center** `LngLatLike` <br>默认值：`[0, 0]`  | 地图初始化时中心点的经纬度。如果没有指定`center`, Mapbox GL JS将会去地图的样式文件中查找，如果样式文件也没有指定，那么将会设置为默认值`[0, 0]`。注意数组的第一个元素是经度，第二个元素是纬度 |
| **options.clickTolerance** `number` <br>默认值：`3`  | 鼠标点击的阈值，单位为像素 |
| **options.collectResourceTiming** `boolean` <br>默认值：`false`  | 如果设置为`true`，将会使用Resource Timing API来收集GeoJSON和矢量瓦片Web Worker（这些信息通常无法在主进程中获取到）发出的请求信息。这些信息将会随`data`事件，通过`resourceTiming`属性返回。 |
| **options.container** `(HTMLElement | string)` | 渲染地图的容器，可以是一个HTML元素，也可以是HTML元素的id。这个HTML元素不能包含子元素 |
| **options.cooperativeGestures** `boolean` | 如果设置为`true`，通过滚轮对地图进行缩放时需要同时按下`ctrl`键或者`⌘`键，触摸平移的时候需要使用两根手指，而触摸倾斜需要使用三根手指 |
| **options.crossSourceCollisions** `boolean` <br>默认值：`true` | 如果设置为`true`，来自多个数据源的符号在碰撞检测时也会发生碰撞。如果设置成`false`，那么每个数据源中的符号在碰撞检测时相互独立互不影响 |
| **options.customAttribution** `(string \| Array<string>)` <br>默认值：`null` | 在[AttributionControl](/api/markers?id=AttributionControl)控件中显示的字符串或者字符串列表，仅在`options.attributionControl`为`true`时有效 |
| **options.doubleClickZoom** `boolean` <br>默认值：`true` | 如果设置为`true`，"双击缩放"交互将会被启用（详情查看[DoubleClickZoomHandler](/api/handlers?id=DoubleClickZoomHandler)） |
| **options.dragPan** `(boolean \| Object)` <br>默认值：`true` | 如果设置为`true`，"拖拽平移"交互将会被启用，如果设置为一个对象，该对象将会被赋给[DragPanHandler](/api/handlers?id=DragPanHandler)的`enable`属性 |
| **options.dragRotate** `boolean` <br>默认值：`true` | 如果设置为`true`，"拖拽旋转"交互将会被启用（详情查看[DragRotateHandler](/api/handlers?id=DragRotateHandler)） |
| **options.fadeDuration** `number` <br>默认值：`300` | 标注碰撞时，标注符号渐显/渐隐动画的时间，单位为“毫秒”。这个选项会影响所有的`symbol`图层。这个选项不会影响地图渲染时或者栅格瓦片消隐时的动画 |
| **options.failIfMajorPerformanceCaveat** `boolean` <br>默认值：`false` | 如果设置为`true`，当Mapbox GL JS的性能比预想的差很多的时候（硬件加速无法启用，只能使用软件渲染），地图将会创建失败 |
| **options.fitBoundsOptions** `object?` | 当上面指定了地图的初始`bounds`，通过该选项给[Map#fitBounds](./?id=fitBounds)函数传递必要的参数 |
| **options.hash** `(boolean | string)` <br>默认值：`false` | 如果设置为`true`，地图的位置信息（级别、中心经度、中心纬度、旋转角度、倾斜角度）将会被同步到当前页面的URL中，例如`http://path/to/my/page.html#2.59/39.26/53.07/-24.1/60`。 |
| **options.interactive** `boolean` <br>默认值：`true` | 如果设置为`false`，所有的鼠标、触摸和键盘事件都会被禁用，所以地图将无法响应任何交互 |
| **options.keyboard** `boolean` <br>默认值：`true` | 如果设置为`true`，将会启用快捷键操作（详情查看[KeyboardHandler](/api/handlers?id=KeyboardHandler)） |
| **options.language** `string` <br>默认值：`null` | 指定地图数据和UI组件所使用的语言。只有Mapbox矢量瓦片数据源可以设置语言，默认情况下GL JS不设置语言，而是由矢量瓦片的TileJSON来决定使用的语言。有效的语言字符串必须是一个[BCP-47 language code](https://en.wikipedia.org/wiki/IETF_language_tag#List_of_subtags)。不支持的BCP-47代码不会有任何翻译，无效的代码会触发一个可恢复的错误。如果一个标注没有当前语言的翻译，将会显示该标准原本的语言。如果该选项设置为`auto`，GL JS将会从用户浏览器中的`window.navigator.language`选择用户偏好语言，如果`locale`属性没有被指定，该语言也会被用作UI的本地化。 |
| **options.locale** `Object` <br>默认值：`null` | 地图UI组件显示语言的本地化补丁，例如控件中显示的提示信息。`locale`对象通过控件的id进行关联和翻译；可以从[src/ui/default_locale.js](https://github.com/mapbox/mapbox-gl-js/blob/main/src/ui/default_locale.js)查看所有支持的控件示例，这个对象既可以指定所有的UI字符串的翻译，也可以指定一部分。 |
| **options.localFontFamily** `string` <br>默认值：`false` | 定义一个CSS字体用来覆盖所生成的字形文件，地图样式中设置的字体将会被忽略，除非设置了`font-weight`。如果设置了该选项，`localIdeographFontFamily`中的设置将会被覆盖 |
| **options.localIdeographFontFamily** `string` <br>默认值：`sans-serif` | 定义一个CSS字体用来覆盖'CJK Unified Ideographs', 'Hiragana', 'Katakana', 'Hangul Syllables' 和 'CJK Symbols and Punctuation'范围内的字形文件。地图样式中设置的这些字形将会被忽略，除非设置了`font-weight`。如果设为`false`，则只能使用样式文件中的字体设置，在[Mapbox Studio]()中，该选项默认设置为`false`。设置该选项的主要目的是避免字体服务器带宽紧张。关于该选项，可以查看示例[使用本地字体](/example/local_font)。 |
| **options.logoPosition** `string` <br>默认值：`bottom-left` | 地图上Mapbox Logo的位置，可取值`top-left`, `top-right`, `bottom-left`, `bottom-right`。 |
| **options.maxBounds** `LngLatBoundsLike` <br>默认值：`null` | 地图可显示的最大范围 |
| **options.maxPitch** `number` <br>默认值：`85` | 地图可倾斜的最大角度 |
| **options.maxTileCacheSize** `number` <br>默认值：`null` | 对于每个数据源的瓦片缓存中，保存的最大的瓦片数量。如果没指定，将会根据当前视图动态设置 |
| **options.maxZoom** `number` <br>默认值：`22` | 地图缩放的最大级别 |
| **options.minPitch** `number` <br>默认值：`0` | 地图可倾斜的最小角度 |
| **options.minTileCacheSize** `number` <br>默认值：`null` | 对于每个数据源的瓦片缓存中，保存的最小的瓦片数量。如果没指定，将会根据当前视图动态设置 |
| **options.minZoom** `number` <br>默认值：`0` | 地图缩放的最小级别 |
| **options.optimizeForTerrain** `boolean` <br>默认值：`true` | 对于地形来说，如果设置为`true`，地图渲染将会优先考虑性能，该操作可能会导致图层的渲染顺序发生改变以获得最优性能（在地形之上的图层会优先渲染，包括`fill`、`line`、`background`、`hillshade`和`raster`。反之如果设为`false`，地图将会始终按照既定的图层顺序渲染 |
| **options.pitch** `number` <br>默认值：`0` | 地图初始化时的倾斜角度，以屏幕所在面为基准面，单位为度。如果在地图构造函数的选项中没有指定`pitch`，Mapbox GL JS将会去地图的样式文件中查找，如果样式文件也没有指定，那么将会设置为默认值`0` |
| **options.pitchWithRotate** `boolean` <br>默认值：`true` | 如果设置为`false`，“拖拽旋转”交互中的倾斜操作将会被禁用 |
| **options.preserveDrawingBuffer** `boolean` <br>默认值：`false` | 如果设置为`true`，地图的`canvas`画布可以用接口`map.getCanvas().toDataURL()`导出为PNG图片。默认为`false`以优化性能。 |
| **options.projection** `ProjectionSpecification` <br>默认值：`mercator` | 地图的投影坐标系，支持以下几种投影：<br> <ul><li>Albers，等积圆锥投影，名称为`albers`</li><li>Equal Earth，等积伪圆柱投影，名称为`equalEarth`</li><li>Equirectangular，圆柱投影，名称为`equirectangular`</li><li>三维球，名称为`globe`</li><li>Lambert Conformal Conic，兰勃特等角投影，名称为`lambertConformalConic`</li><li>Mercator，墨卡托投影，名称为`mercator`</li><li>Natural Earth，伪圆柱投影，名称为`naturalEarth`</li><li>Winkel Tripel，温克尔三重投影，名称为`winkelTripel`</li></ul>圆锥投影例如Albers和Lambert有`center`和`parallels`两个属性项，可以让开发者去定义拥有最小变形的区域；可以从示例中去查看如何配置这些属性。 |
| **options.refreshExpiredTiles** `boolean` <br>默认值：`true` | 如果设置为`false`，当地图瓦片超过HTTP请求头`cacheControl` / `expires`中设置的日期时，地图不会去重新请求新的瓦片 |
| **options.renderWorldCopies** `boolean` <br>默认值：`true` | 如果设置为`true`，当地图可视范围超过[-180, 180]时，将会并排循环显示世界地图。如果设置为`false`：<ul><li>当地图缩小的很小的级别，一整个世界地图无法填满地图容器时，超过[-180, 180]的区域将会显示为空白。</li><li>有部分位于-180/180临界线上的要素会被分割成两部分（一部分在地图的左边缘，另一部分在右边缘）</li></ul> |
| **options.scrollZoom** `(boolean \| Object)` <br>默认值：`true` | 如果设置为`true`，"滚动缩放"交互将会被启用。如果是一个`Object`，它会被作为参数传递给[ScrollZoomHandler](/api/handles?id=ScrollZoomHandler)的`enable`函数 |
| **options.style** `(Object \| string)` | 地图的样式文件，必须是一个符和[Mapbox样式规范](/api/style)的JSON对象，或者是能获得该JSON对象的URL。可以设置为`null`，之后手动添加一个style样式。<br>如果想要从Mapbox API去加载一个样式，可以使用`mapbox://styles/:owner/:style`这种格式的URL，其中`:owner`是你的Mapbox账户名称，`:style`是样式id。你也可以使用Mapbox官方对外提供的[服务](https://docs.mapbox.com/api/maps/styles/#mapbox-styles): <ul><li>`mapbox://styles/mapbox/streets-v11`</li><li>`mapbox://styles/mapbox/outdoors-v11`</li><li>`mapbox://styles/mapbox/light-v10`</li><li>`mapbox://styles/mapbox/dark-v10`</li><li>`mapbox://styles/mapbox/satellite-v9`</li><li>`mapbox://styles/mapbox/satellite-streets-v11`</li><li>`mapbox://styles/mapbox/navigation-day-v1`</li><li>`mapbox://styles/mapbox/navigation-night-v1`</li></ul> 如果在你的URL后面加上`?optimize=true`，例如`mapbox://styles/mapbox/streets-v11?optimize=true`，Mapbox可以对其提供的矢量瓦片集进行风格优化，想了解更多相关内容，可以查看[Mapbox API文档](https://www.mapbox.com/api-documentation/maps/#retrieve-tiles) |
| **options.testMode** `boolean` <br>默认值：`true` | 当accessToken无效时，不会显式地抛出错误，对与使用库写单元测试时会很有用 |
| **options.touchPitch** `(boolean \| Object)` <br>默认值：`true` | 如果设置为`true`，"拖拽倾斜"交互将会被启用。如果是一个`Object`，它会被作为参数传递给[TouchZoomRotateHandler](/api/handles?id=TouchZoomRotateHandler)的`enable`函数 |
| **options.trackResize** `boolean` <br>默认值：`true` | 如果设为`true`，当浏览器窗口大小改变时，地图会自动重新设置大小 |
| **options.transformRequest** `RequestTransformFunction` <br>默认值：`null` | 地图请求外部URL之前需要执行的回调。这个回调可以用来对URL进行修改、设置请求头或者对跨域请求添加凭证等。这个回调函数需要返回一个[RequestParameters](https://docs.mapbox.com/mapbox-gl-js/api/properties/#requestparameters)对象，包含`url`属性，或者必要的`headers`和`credentials`属性 |
| **options.worldview** `string?` | 设置地图的worldview，主要用来确定有争议的边界线如何渲染。默认情况下GL JS不会设置worldview，因此Mapbox瓦片的worldview由矢量瓦片的TileJSON来决定。有效的wordview代码参考[ISO alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes)，如果设置了无效的代码，将会回溯到TileJSON中的worldview。 |
| **options.zoom** `number` <br>默认值：`0` | 初始化时的地图级别。如果在地图构造函数的选项中没有指定`zoom`，Mapbox GL JS将会去地图的样式文件中查找，如果样式文件也没有指定，那么将会设置为默认值`0` |

## 示例

```js
const map = new mapboxgl.Map({
  container: 'map', // container ID
  center: [-122.420679, 37.772537], // starting position [lng, lat]
  zoom: 13, // starting zoom
  style: 'mapbox://styles/mapbox/streets-v11', // style URL or style object
  hash: true, // sync `center`, `zoom`, `pitch`, and `bearing` with URL
  // Use `transformRequest` to modify requests that begin with `http://myHost`.
  transformRequest: (url, resourceType) => {
    if (resourceType === 'Source' && url.startsWith('http://myHost')) {
      return {
        url: url.replace('http', 'https'),
        headers: {'my-custom-header': true},
        credentials: 'include'  // Include cookies for cross-origin requests
      };
    }
  }
});
```

## 实例成员

### 交互处理程序

- scrollZoom

地图的[ScrollZoomHandler](/api/handlers?id=ScrollZoomHandler)，实现了使用滚轮或者触控板进行地图缩放的操作。可以在[ScrollZoomHandler](/api/handlers?id=ScrollZoomHandler)部分查看更多详情和示例。

- boxZoom

地图的[BoxZoomHandler](/api/handlers?id=BoxZoomHandler)，按住Shift键时可以使用拖拽手势将地图缩放到对应位置。可以在[BoxZoomHandler](/api/handlers?id=BoxZoomHandler)部分查看更多详情和示例。

- dragRotate

地图的[DragRotateHandler](/api/handlers?id=DragRotateHandler)，可以使用Control键或者鼠标右键拖拽地图实现地图旋转。可以在[DragRotateHandler](/api/handlers?id=DragRotateHandler)部分查看更多详情和示例。

- dragPan

地图的[DragPanHandler](/api/handlers?id=DragPanHandler)，可以使用触摸手势或者鼠标对地图进行拖拽平移。可以在[DragPanHandler](/api/handlers?id=DragPanHandler)部分查看更多详情和示例。

- keyboard

地图的[KeyboardHandler](/api/handlers?id=KeyboardHandler)，可以使用快捷键对地图进行平移、缩放或者旋转等操作。可以在[KeyboardHandler](/api/handlers?id=KeyboardHandler)部分查看更多详情和示例。

- doubleClickZoom

地图的[DoubleClickZoomHandler](/api/handlers?id=DoubleClickZoomHandler)，允许用户通过鼠标双击对地图进行放大。可以在[DoubleClickZoomHandler](/api/handlers?id=DoubleClickZoomHandler)部分查看更多详情和示例。

- touchZoomRotate

地图的[TouchZoomRotateHandler](/api/handlers?id=TouchZoomRotateHandler)，允许用户通过触摸手势对地图进行缩放或旋转。可以在[TouchZoomRotateHandler](/api/handlers?id=TouchZoomRotateHandler)部分查看更多详情和示例。

- touchPitch

地图的[TouchPitchHandler](/api/handlers?id=TouchPitchHandler)，允许用户通过触摸手势对地图进行倾斜操作。可以在[TouchPitchHandler](/api/handlers?id=TouchPitchHandler)部分查看更多详情和示例。

### 控件

#### addControl(control, position?)

调用`control.onAdd(this)`向地图上添加一个[IControl](/api/markers?id=IControl)控件。

**参数**

*control* `IControl` 需要添加到地图上的[IControl](/api/markers?id=IControl)控件。

*position* `string?` 控件在地图上的位置，可取值`'top-left'` , `'top-right'` , `'bottom-left'` , 和 `'bottom-right'` 。 默认值 `'top-right'`

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Add zoom and rotation controls to the map.
map.addControl(new mapboxgl.NavigationControl());
```

**相关资料**

[示例: 在地图上显示导航控件](https://www.mapbox.com/mapbox-gl-js/example/navigation/)

----------

#### removeControl(control)

从地图上移除控件

**参数**

*control* `IControl` 需要移除的[IControl](/api/markers?id=IControl)控件。

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Define a new navigation control.
const navigation = new mapboxgl.NavigationControl();
// Add zoom and rotation controls to the map.
map.addControl(navigation);
// Remove zoom and rotation controls from the map.
map.removeControl(navigation);
```

----------

#### hasControl(control)

检查地图上是否存在某个控件

**参数**

*control* `IControl` 需要检查的[IControl](/api/markers?id=IControl)控件。

**返回值**

`boolean`: 存在则返回`true`，否则返回`false`

**示例**

```js
// Define a new navigation control.
const navigation = new mapboxgl.NavigationControl();
// Add zoom and rotation controls to the map.
map.addControl(navigation);
// Check that the navigation control exists on the map.
const added = map.hasControl(navigation);
// added === true
```

----------

#### getContainer()

获取地图容器的HTML元素

**返回值**

`HTMLElement`: 地图的容器

**示例**

```js
const container = map.getContainer();
```

----------

#### getCanvasContainer()

返回包含地图`<canvas>`画布的那个HTML元素。

如果你需要添加一些非WebGL绘制的内容到地图上，你应该把这些内容放在这个HTML元素里面。

地图上的一些交互事件例如平移缩放等，也绑定在这个元素上，它的子元素上的事件例如`<canvas>`也会冒泡到该元素上，但是添加到地图上的控件不会冒泡到该元素。

**返回值**

`HTMLElement`: 包含地图`<canvas>`画布的HTML元素

**示例**

```js
const canvasContainer = map.getCanvasContainer();
```

**相关资料**

[示例: 创建一个可拖拽的点](https://www.mapbox.com/mapbox-gl-js/example/drag-a-point/)

[示例: 高亮显示一个矩形包围盒内部的要素](https://www.mapbox.com/mapbox-gl-js/example/using-box-queryrenderedfeatures/)

----------

#### getCanvas()

返回地图的`<canvas>`元素。

**返回值**

`HTMLCanvasElement`: 地图的`<canvas>`元素

**示例**

```js
const canvas = map.getCanvas();
```

**相关资料**

[示例: 测量距离](https://www.mapbox.com/mapbox-gl-js/example/measure/)

[示例: 鼠标悬浮时显示一个弹窗](https://www.mapbox.com/mapbox-gl-js/example/popup-on-hover/)

[示例: 点击一个符号时，将符号居中](https://www.mapbox.com/mapbox-gl-js/example/center-on-symbol/)

### 地图操作

#### resize(eventData)

根据地图容器的大小对地图大小进行重置。

检查地图的容器大小是否发生变化，发生变化时对地图进行更新。这个方法必须在地图的容器大小由程序改变以后触发，或者初始化时，地图的容器由CSS进行了隐藏，显示地图时触发。

**参数**

*eventData* `Object | null` 给那些因地图大小重置而触发的事件传递额外的参数，例如`movestart`, `move`, `resize`和`moveend`。这对于区分事件的来源（例如这个事件是由于程序触发还是因用户交互触发）很有用。

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Resize the map when the map container is shown
// after being initially hidden with CSS.
const mapDiv = document.getElementById('map');
if (mapDiv.style.visibility === true) map.resize();
```

-----------

#### getBounds()

返回地图的经纬度范围。当地图的倾斜角度或者旋转角度不为0的时候，地图的可视范围并不是一个矩形，返回的结果是包含可视区域的最小矩形。如果地图上设置了内边距，返回的结果是包含内部的范围，不包含边距。

这个函数不支持“三维球(globe)”投影

**返回值**

`LngLatBounds`: 地图的经纬度范围，是一个[LngLatBounds](/api/geography?id=LngLatBounds)对象

**示例**

```js
const bounds = map.getBounds();
```

-----------

#### getMaxBounds()

返回地图显示的最大经纬度范围，如果没有设置，则返回`null`

**返回值**

`Map`: 地图实例

**示例**

```js
const maxBounds = map.getMaxBounds();
```

-----------

#### setMaxBounds(bounds)

设置或者取消地图的最大经纬度范围。

设置该范围以后，地图的缩放和平移操作将会被限制在该范围内。如果想要平移和缩放到该范围以外的区域显示，那么地图将会尝试显示一个与目标位置尽可能接近的位置和级别，但是仍然会将地图限制在该范围以内。

对于`墨卡托(mercator)`坐标系，地图的视图会被限制在该范围，但是对于其他坐标系例如`globe`，则只限制地图的中心点。

**参数**

*bounds* `((LngLatBoundsLike | null | undefined))` 设置的最大经纬度范围，如果设置了`null`或`undefined`，则会清除原来设置的经纬度范围

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Define bounds that conform to the `LngLatBoundsLike` object.
const bounds = [
  [-74.04728, 40.68392], // [west, south]
  [-73.91058, 40.87764]  // [east, north]
];
// Set the map's max bounds.
map.setMaxBounds(bounds);
```

-----------

#### setMinZoom(minZoom)

设置或者取消地图的最小级别。如果当前地图的级别小于设置的最小级别，地图将会被缩放到设置的最小级别。

并不是设置了最小级别地图就一定能缩小到这个级别。也会有其他因素例如地图的高度会影响到地图的缩放。例如地图的高度是512px时，及时设置了最小级别为0，地图也不可能缩放到第0级。

**参数**

*minZoom* `((number | null | undefined))` 设置的小级别（-2到24），如果设置了`null`或`undefined`，则会清除原来设置的最小级别，将最小级别重置为-2

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setMinZoom(12.25);
```

-----------

#### getMinZoom()

返回地图的最小级别

**返回值**

`number`: 返回`minZoom`

**示例**

```js
const minZoom = map.getMinZoom();
```

-----------

#### setMaxZoom(maxZoom)

设置或者取消地图的最大级别。如果当前地图的级别大于设置的最大级别，地图将会被缩放到设置的最大级别。

**参数**

*maxZoom* `((number | null | undefined))` 设置的最大级别，如果设置了`null`或`undefined`，则会清除原来设置的最大级别，将最大级别重置为22

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setMaxZoom(18.75);
```

-----------

#### getMaxZoom()

返回地图的最大级别

**返回值**

`number`: 返回`maxZoom`

**示例**

```js
const maxZoom = map.getMaxZoom();
```

-----------

#### setMinPitch(minPitch)

设置或者取消地图的最小倾斜角度。如果当前地图的倾斜角度小于设置的倾斜角度，地图将会倾斜到设置的最小角度。

**参数**

*minPitch* `((number | null | undefined))` 设置的最小倾斜角度（0-85），如果设置了`null`或`undefined`，则会清除原来设置的最小倾斜角度，将最小倾斜角度重置为0

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setMinPitch(5);
```

-----------

#### getMinPitch()

返回地图的最小倾斜角度

**返回值**

`number`: 返回`minPitch`

**示例**

```js
const minPitch = map.getMinPitch();
```

-----------

#### setMaxPitch(maxPitch)

设置或者取消地图的最大倾斜角度。如果当前地图的倾斜角度大于设置的倾斜角度，地图将会倾斜到设置的最大角度。

**参数**

*maxPitch* `((number | null | undefined))` 设置的最大倾斜角度，如果设置了`null`或`undefined`，则会清除原来设置的最大倾斜角度，将最大倾斜角度重置为85

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setMaxPitch(70);
```

-----------

#### getMaxPitch()

返回地图的最大倾斜角度

**返回值**

`number`: 返回`maxPitch`

**示例**

```js
const maxPitch = map.getMaxPitch();
```

-----------

#### getRenderWorldCopies()

返回`renderWorldCopies`的属性值。如果值为`true`，当地图可视范围超过[-180, 180]时，将会并排循环显示世界地图。如果值为`false`：
- 当地图缩小的很小的级别，一整个世界地图无法填满地图容器时，超过[-180, 180]的区域将会显示为空白
- 有部分位于-180/180临界线上的要素会被分割成两部分（一部分在地图的左边缘，另一部分在右边缘）

**返回值**

`boolean`: 返回`renderWorldCopies`的值

**示例**

```js
const worldCopiesRendered = map.getRenderWorldCopies();
```

**相关资料**

[示例: Render world copies](https://docs.mapbox.com/mapbox-gl-js/example/render-world-copies/)

-----------

#### setRenderWorldCopies(renderWorldCopies)

设置`renderWorldCopies`的属性值。

**参数**

*renderWorldCopies* `boolean` 如果值为`true`，当地图可视范围超过[-180, 180]时，将会并排循环显示世界地图。如果值为`false`：
- 当地图缩小的很小的级别，一整个世界地图无法填满地图容器时，超过[-180, 180]的区域将会显示为空白
- 有部分位于-180/180临界线上的要素会被分割成两部分（一部分在地图的左边缘，另一部分在右边缘）

`undefined`被当作`true`处理，而`null`被当作`false`处理。

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setRenderWorldCopies(true);
```

**相关资料**

[示例: Render world copies](https://docs.mapbox.com/mapbox-gl-js/example/render-world-copies/)

### 坐标转换

-----------

#### getProjection()

返回当前地图的投影信息

**返回值**

`ProjectionSpecification`: 一个描述当前地图投影信息的[projection](/style/projection.md)对象

**示例**

```js
const projection = map.getProjection();
```

-----------

#### setProjection(projection)

设置地图投影，如果参数是`null`或`undefined`，地图会重置为墨卡托投影

**参数**

*projection* `((ProjectionSpecification | string | null | undefined))` 地图的投影信息，可以是一个[projection](/style/projection.md)对象或投影的名称

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setProjection('albers');
map.setProjection({
  name: 'albers',
  center: [35, 55],
  parallels: [20, 60]
});
```

**相关资料**

[示例: 使用其他的投影坐标系来显示网络地图](https://docs.mapbox.com/mapbox-gl-js/example/map-projection/)

[示例: 在地图中使用不同的投影](https://docs.mapbox.com/mapbox-gl-js/example/projections/)

-----------

#### project(lnglat)

给定一个经纬度坐标，返回这个点相对地图容器(`container`)的像素坐标，用[Point](/api/geography?id=Point)对象表示。

当地图处于倾斜状态，而给定的`lnglat`完全在相机后面，那么不存在该点的像素坐标。这种情况下，返回的[Point](/api/geography?id=Point)对象中的`x`和`y`属性会设置为`Number.MAX_VALUE`。

**参数**

*lnglat* `LngLatLike` 经纬度坐标

**返回值**

`Point`: 相对地图`container`的像素坐标

**示例**

```js
const coordinate = [-122.420679, 37.772537];
const point = map.project(coordinate);
```

-----------

#### unproject(point)

给定一个点的像素坐标，返回这个点的经纬度，用[LngLat](/api/geography?id=LngLat)对象表示。如果地图上显示有地平线，而给定的点位于地平线以上，则返回位于地平线上并且离给定的点最近的那个点的经纬度。

**参数**

*point* `PointLike` 像素坐标

**返回值**

`LngLat`: 该点对应的经纬度坐标

**示例**

```js
map.on('click', (e) => {
  // When the map is clicked, get the geographic coordinate.
  const coordinate = map.unproject(e.point);
});
```

### 地图状态

-----------

#### isMoving()

如果地图正在平移、缩放、旋转或倾斜，则返回`true`

**返回值**

`boolean`: 地图是否正在移动中

**示例**

```js
const isMoving = map.isMoving();
```

-----------

#### isZooming()

如果地图正在缩放，则返回`true`

**返回值**

`boolean`: 地图是否正在缩放中

**示例**

```js
const isZooming = map.isZooming();
```

-----------

#### isRotating()

如果地图正在旋转，则返回`true`

**返回值**

`boolean`: 地图是否正在旋转中

**示例**

```js
const isRotating = map.isRotating();
```

### 事件处理

#### on(type, layerIds, listener)

给指定的事件类型添加一个监听函数，如果指定了`layerIds`，则只在指定的图层上面监听

**参数**

*type* `string` 需要监听的事件类型，只有部分事件可以指定在某个图层上监听，具体如下表所示：

|  事件   | 是否支持`layerId`  |
|  ----  | ----  |
| mousedown | 是 |
| mouseup | 是 |
| mouseover | 是 |
| mouseout | 是 |
| mousemove | 是 |
| mouseenter | 是（必须指定layerId） |
| mouseleave | 是（必须指定layerId） |
| preclick |  |
| click | 是 |
| dblclick | 是 |
| contextmenu | 是 |
| touchstart | 是 |
| touchend | 是 |
| touchcancel | 是 |
| wheel |  |
| resize |  |
| remove |  |
| touchmove |  |
| movestart |  |
| move |  |
| moveend |  |
| dragstart |  |
| drag |  |
| dragend |  |
| zoomstart |  |
| zoom |  |
| zoomend |  |
| rotatestart |  |
| rotate |  |
| rotateend |  |
| pitchstart |  |
| pitch |  |
| pitchend |  |
| boxzoomstart |  |
| boxzoomend |  |
| boxzoomcancel |  |
| webglcontextlost |  |
| webglcontextrestored |  |
| load |  |
| render |  |
| idle |  |
| error |  |
| data |  |
| styledata |  |
| sourcedata |  |
| dataloading |  |
| styledataloading |  |
| sourcedataloading |  |
| styleimagemissing |  |

*layerIds* `((string | Array<string>))` 可选。 样式中的图层id列表。

如果指定了`layerId`，那么事件只会在指定的图层可见的要素上触发，并且返回的事件参数上面会带有`features`属性，包含匹配到的所有要素列表。如果没有指定`layersIds`，事件可能在地图上的任何地方触发，事件参数中也不会有`features`属性。注意并不是所有的事件类型都能指定`layerIds`。

*listener* `Function` 事件触发后需要执行的监听函数

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Set an event listener that will fire
// when the map has finished loading.
map.on('load', () => {
  // Add a new layer.
  map.addLayer({
    id: 'points-of-interest',
    source: {
      type: 'vector',
      url: 'mapbox://mapbox.mapbox-streets-v8'
    },
    'source-layer': 'poi_label',
    type: 'circle',
    paint: {
      // Mapbox Style Specification paint properties
    },
    layout: {
      // Mapbox Style Specification layout properties
    }
  });
});
```

```js
// Set an event listener that will fire
// when a feature on the countries layer of the map is clicked.
map.on('click', 'countries', (e) => {
  new mapboxgl.Popup()
    .setLngLat(e.lngLat)
    .setHTML(`Country name: ${e.features[0].properties.name}`)
    .addTo(map);
});
```

```js
// Set an event listener that will fire
// when a feature on the countries or background layers of the map is clicked.
map.on('click', ['countries', 'background'], (e) => {
  new mapboxgl.Popup()
    .setLngLat(e.lngLat)
    .setHTML(`Country name: ${e.features[0].properties.name}`)
    .addTo(map);
});
```

**相关资料**

[示例: 在地图上添加三维地形](https://docs.mapbox.com/mapbox-gl-js/example/add-terrain/)

[示例: 点击一个符号时，将符号居中](https://docs.mapbox.com/mapbox-gl-js/example/center-on-symbol/)

[示例: 创建一个可拖拽的标签](https://docs.mapbox.com/mapbox-gl-js/example/drag-a-point/)

[示例: 创建鼠标悬浮高亮效果](https://docs.mapbox.com/mapbox-gl-js/example/hover-styles/)

[示例: 点击地图显示一个弹窗](https://docs.mapbox.com/mapbox-gl-js/example/popup-on-click/)

----------
#### once(type, layerIds, listener)

给指定的事件类型添加一个一次性的监听函数，如果指定了`layerIds`，则只在指定的图层上面监听

**参数**

*type* `string` 需要监听的事件类型，支持以下事件类型：`'mousedown'` , `'mouseup'` , `'preclick'` , `'click'` , `'dblclick'` , `'mousemove'` , `'mouseenter'` , `'mouseleave'` , `'mouseover'` , `'mouseout'` , `'contextmenu'` , `'touchstart'` , `'touchend'` , 或者 `'touchcancel'`。

`mouseenter`和`mouseover`在鼠标从地图外面或者图层外面移动到指定要素上时触发。

*layerIds* `((string | Array<string>))` 可选。 样式中的图层id列表。`mouseleave`和`mouseout`在鼠标从指定的要素移出去时触发。

如果指定了`layerId`，那么事件只会在指定的图层可见的要素上触发，并且返回的事件参数上面会带有`features`属性，包含匹配到的所有要素列表。如果没有指定`layersIds`，事件可能在地图上的任何地方触发，事件参数中也不会有`features`属性。注意并不是所有的事件类型都能指定`layerIds`。

*listener* `Function` 事件触发后需要执行的监听函数

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Log the coordinates of a user's first map touch.
map.once('touchstart', (e) => {
  console.log(`The first map touch was at: ${e.lnglat}`);
});
```

```js
// Log the coordinates of a user's first map touch
// on a specific layer.
map.once('touchstart', 'my-point-layer', (e) => {
  console.log(`The first map touch on the point layer was at: ${e.lnglat}`);
});
```

```js
// Log the coordinates of a user's first map touch
// on specific layers.
map.once('touchstart', ['my-point-layer', 'my-point-layer-2'], (e) => {
  console.log(`The first map touch on the point layer was at: ${e.lnglat}`);
});
```

**相关资料**

[示例: 创建一个可拖拽的点](https://docs.mapbox.com/mapbox-gl-js/example/drag-a-point/)

[示例: 在三维地形上绕点飞行](https://docs.mapbox.com/mapbox-gl-js/example/free-camera-point/)

[示例: 创建地图飞行动画，并在侧边显示详情](https://docs.mapbox.com/mapbox-gl-js/example/playback-locations/)

----------
#### off(type, layerIds, listener)

将地图上用[Map#on](/api/map?id=ontype-layerids-listener)添加的事件监听函数全部移除，也可以选择只移除指定图层上的事件

**参数**

*type* `string` 需要移除监听的事件类型

*layerIds* `((string | Array<string>))` 可选。 之前添加监听时指定的图层列表

*listener* `Function` 需要移除的监听函数

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
// Create a function to print coordinates while a mouse is moving.
function onMove(e) {
  console.log(`The mouse is moving: ${e.lngLat}`);
}
// Create a function to unbind the `mousemove` event.
function onUp(e) {
  console.log(`The final coordinates are: ${e.lngLat}`);
  map.off('mousemove', onMove);
}
// When a click occurs, bind both functions to mouse events.
map.on('mousedown', (e) => {
  map.on('mousemove', onMove);
  map.once('mouseup', onUp);
});
```

**相关资料**

[示例: 创建一个可拖拽的点](https://docs.mapbox.com/mapbox-gl-js/example/drag-a-point/)

### 要素查询

#### queryRenderedFeatures(geometry?, options?)

返回满足查询条件的[GeoJSON要素](http://geojson.org/)列表

**参数**

*geometry* `((PointLike | Array<PointLike>)?)` 需要查询的几何范围，单位为像素。可以是一个单独的点，也可以是一个由左下角点和右上角点构成的包围盒。如果不指定该参数，则会认为要查询的是整个地图视图。只有在地图视图内的范围才有效。

*options* `(Object?)` 查询参数，具体参数项如下：

| 名称 | 描述 |
| ---- | ---- |
| **options.filter** `Array?` | 过滤条件，对查询结果按指定的条件进行过滤 |
| **options.layers** `Array<string>?` | 需要查询的图层id列表，只有指定的图层要素才会被返回，如果这个属性为`undefined`，则所有的符合条件的图层都会被查询到 |
| **options.validate** `boolean` <br> 默认值：`true` | 检查`options.filter`是否符合Mapbox样式规范。禁用格式检查可以用来进行性能优化，但前提是你在调用该函数之前已经检查过该参数的有效性 |


**返回值**

`Array<Object>`: 满足查询条件的[GeoJSON要素](http://geojson.org/)列表

返回的要素中的`properties`属性是该要素数据源中的属性值。对于GeoJSON数据源来说，只支持字符串和数值类型的属性值。`null`、`Array`和`Object`不支持。

返回的每个每个要素在最上层都有`layer`、`source`和`sourceLayer`属性。其中`layer`属性表示查询到的这个要素是样式(style)中的哪个图层渲染的。`layer`属性中的布局属性和绘图属性的值是根据当前级别和要素重新计算的。

只会返回当前渲染在地图上的要素，以下几种要素不会被查询到：

- 图层中的`visibility`属性值为`none`的要素

- 图层中设置的可见级别的范围不包含当前地图的级别

- 由于文本或图标碰撞被隐藏的符号要素

除此以外的所有其他要素都可以被查询到，包括那些因绘图属性设置原因而在地图上不可见的要素，例如图层的透明度或者颜色值的alpha通道设置为0。

位于地图上层的要素在返回的数组中会越靠前，同一个要素被多次渲染（低级别时跨越中央子午线的要素），只会返回一条结果。



**示例**

```js
// Find all features at a point
const features = map.queryRenderedFeatures(
  [20, 35],
  {layers: ['my-layer-name']}
);
```

```js
// Find all features within a static bounding box
const features = map.queryRenderedFeatures(
  [[10, 20], [30, 50]],
  {layers: ['my-layer-name']}
);
```

```js
// Find all features within a bounding box around a point
const width = 10;
const height = 20;
const features = map.queryRenderedFeatures([
  [point.x - width / 2, point.y - height / 2],
  [point.x + width / 2, point.y + height / 2]
], {layers: ['my-layer-name']});
```

```js
// Query all rendered features from a single layer
const features = map.queryRenderedFeatures({layers: ['my-layer-name']});
```

**相关资料**

[示例: 查询鼠标指针处的要素](https://www.mapbox.com/mapbox-gl-js/example/queryrenderedfeatures/)

[示例: 高亮指定包围盒内的要素](https://www.mapbox.com/mapbox-gl-js/example/using-box-queryrenderedfeatures/)

[示例: 查询地图视图范围内的所有要素](https://www.mapbox.com/mapbox-gl-js/example/filter-features-within-map-view/)

#### querySourceFeatures(sourceId, parameters?)

返回指定的矢量瓦片或GeoJSON数据源种满足查询条件的[GeoJSON要素](http://geojson.org/)列表

**参数**

*sourceId* `(string)` 矢量瓦片或者GeoJSON数据源的ID。

*parameters* `(Object?)` 查询参数，具体参数项如下：

| 名称 | 描述 |
| ---- | ---- |
| **parameters.filter** `Array?` | 过滤条件，对查询结果按指定的条件进行过滤 |
| **parameters.sourceLayer** `Array<string>?` | 需要查询的数据图层名称。只对矢量瓦片数据源有效，GeoJSON数据源忽略该参数 |
| **parameters.validate** `boolean` <br> 默认值：`true` | 检查`options.filter`是否符合Mapbox样式规范。禁用格式检查可以用来进行性能优化，但前提是你在调用该函数之前已经检查过该参数的有效性 |


**返回值**

`Array<Object>`: 满足查询条件的[GeoJSON要素](http://geojson.org/)列表

与[Map#queryRenderedFeatures](/api/map?id=queryrenderedfeaturesgeometry-options)不同的是，该函数会返回所有符合条件的要素列表，无论该要素是否渲染。查询范围包含所有已经加载的矢量瓦片和GeoJSON数据源，但是不包括当前视图范围以外的数据。

由于查询的要素来自与矢量瓦片或者GeoJSON数据源，因此在瓦片边界的地方可能会出现要素被切割或者重复的要素，因此在查询结果中可能有部分要素重复出现。



**示例**

```js
// Find all features in one source layer in a vector source
const features = map.querySourceFeatures('your-source-id', {
  sourceLayer: 'your-source-layer'
});
```

**相关资料**

[示例: 高亮与当前选中的数据相似的要素](https://www.mapbox.com/mapbox-gl-js/example/query-similar-features/)

### 样式相关

#### setStyle(style, options?)

更新地图的样式。

如果已经设置过地图样式，再次调用该函数并且`diff`参数设置为`true`时，地图会将新的样式与旧的样式就行比较，并找出变化的部分，只对变化的部分进行更新。但是sprite和glyph发生变化时无法进行差异化更新，只能进行整体更新，会将原来的地图样式移除后再重新设置新的地图样式。

**参数**

*style* `((Object | string | null))` 一个描述地图样式的JSON对象或者该JSON对象的url地址。

*options* `(Object?)` 选项参数，具体参数项如下：

| 名称 | 描述 |
| ---- | ---- |
| **options.diff** `boolean` <br> 默认值：`true` | 如果设为`false`，则进行全量更新，会将原来的地图样式移除，再设置新的地图样式 |
| **options.localIdeographFontFamily** `string` <br> 默认值：`sans-serif` | 定义一个CSS字体用来覆盖'CJK Unified Ideographs', 'Hiragana', 'Katakana', 'Hangul Syllables' 和 'CJK Symbols and Punctuation'范围内的字形文件。地图样式中设置的这些字形将会被忽略，除非设置了`font-weight`。如果设为`false`，则只能使用样式文件中的字体设置。 |

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.setStyle("mapbox://styles/mapbox/streets-v11");
```

**相关资料**

[示例: 更改地图的样式](https://www.mapbox.com/mapbox-gl-js/example/setstyle/)

#### getStyle()

获取地图的样式

**返回值**

`Object`: 地图样式的JSON对象。

**示例**

```js
map.on('load', () => {
  const styleJson = map.getStyle();
});
```

#### isStyleLoaded()

检查地图的样式是否已经被完整的加载

**返回值**

`boolean`: 地图样式是否已被完整加载。

**示例**

```js
const styleLoadStatus = map.isStyleLoaded();
```

### 数据源

#### addSource(id, source)

向地图样式中添加一个新的数据源。

**参数**

*id* `(string)` 需要添加的数据源的ID，不能与已有的数据源冲突。

*source* `(Object?)` 要添加的数据源，参考样式规范中的[数据源定义](/style/sources.md)

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.addSource('my-data', {
  type: 'vector',
  url: 'mapbox://myusername.tilesetid'
});
```

```js
map.addSource('my-data', {
  "type": "geojson",
  "data": {
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [-77.0323, 38.9131]
  },
  "properties": {
    "title": "Mapbox DC",
    "marker-symbol": "monument"
  }
  }
});
```

**相关资料**

[示例: 矢量瓦片数据源：显示和隐藏图层](https://docs.mapbox.com/mapbox-gl-js/example/toggle-layers/)

[示例: GeoJSON数据源：添加实时数据](https://docs.mapbox.com/mapbox-gl-js/example/live-geojson/)

[示例: 栅格数据源：添加山影](https://docs.mapbox.com/mapbox-gl-js/example/hillshade/)

#### isSourceLoaded(id)

检查指定的数据源是否已经加载，如果指定id的数据源已经没有需要请求的数据，则返回`true`，否则返回`false`

**参数**

*id* `(string)` 需要检查的数据源ID。

**返回值**

`boolean`: 指定的数据源是否已经加载

**示例**

```js
const sourceLoaded = map.isSourceLoaded('bathymetry-data');
```

#### areTilesLoaded()

当前视图内所有数据源的所有瓦片是否已经加载完成。

**返回值**

`boolean`: 视图内的所有瓦片是否都已经请求完成

**示例**

```js
const tilesLoaded = map.areTilesLoaded();
```

#### removeSource(id)

从当前地图样式中移除指定id的数据源。

**参数**

*id* `(string)` 需要移除的数据源ID。

**返回值**

`Map`: 返回地图实例本身用来链式调用

**示例**

```js
map.removeSource('bathymetry-data');
```

#### getSource(id)

获取指定id的数据源。该方法通常用来获取数据源示例来更新地图样式中的数据源。例如设置GeoJSON数据源的`data`，或者更新图片数据源的`url`和`coordinates`。

**参数**

*id* `(string)` 需要获取的数据源ID。

**返回值**

`Object?`: 指定id的数据源示例，如果不存在则返回undefined。具体的结构根据数据源的类型不同会有所不同。

**示例**

```js
const sourceObject = map.getSource('points');
```

**相关资料**

[示例: 创建一个可拖拽的点](https://docs.mapbox.com/mapbox-gl-js/example/drag-a-point/)

[示例: 为点要素创建一个动画效果](https://docs.mapbox.com/mapbox-gl-js/example/animate-point-along-line/)

[示例: 添加实时数据](https://docs.mapbox.com/mapbox-gl-js/example/live-geojson/)

### 图片

#### addImage(id, image, options)

向地图样式中添加一个图片，这个图片可以像地图样式sprite中的图标一样使用，通过图片的id用于`icon-iamge`,`background-pattern`, `fill-pattern`或者`line-pattern`。如果地图的雪碧图中没有足够的空间添加图片，则会报错。

**参数**

*id* `(string)` 图片的id

*image* `((HTMLImageElement | ImageBitmap | ImageData | {width: number, height: number, data: (Uint8Array | Uint8ClampedArray)} | StyleImageInterface))` 需要添加的图片，可以是`HTMLImageElement`, `ImageData`, `ImageBitmap`或者一个包含`width`, `height`和`data`属性的对象。

*options* `((Object | null))` 选项参数，默认值`{}`，具体参数如下：

| 名称 | 描述 |
| ---- | ---- |
| **options.content** `[number, number, number, number]` | `[x1, y1, x2, y2]` 如果设置了`icon-text-fit`，该属性定义了图片中可以被`text-field`中的内容覆盖的部分 |
| **options.pixelRatio** `number` <br> 默认值：`1` | 图片的像素与屏幕的像素比 |
| **options.sdf** `boolean` <br> 默认值：`false` | 图片是否解析为sdf图片 |
| **options.stretchX** `Array<[number, number]>` | 图片是否解析为sdf图片 |
| **options.stretchY** `Array<[number, number]>` | 图片是否解析为sdf图片 |

**返回值**

`Object?`: 指定id的数据源示例，如果不存在则返回undefined。具体的结构根据数据源的类型不同会有所不同。

**示例**

```js
const sourceObject = map.getSource('points');
```

**相关资料**

[示例: 创建一个可拖拽的点](https://docs.mapbox.com/mapbox-gl-js/example/drag-a-point/)

[示例: 为点要素创建一个动画效果](https://docs.mapbox.com/mapbox-gl-js/example/animate-point-along-line/)

[示例: 添加实时数据](https://docs.mapbox.com/mapbox-gl-js/example/live-geojson/)
