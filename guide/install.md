# 安装

在开始使用mapbox-gl-js之前，你需要先申请一个access_token，再将mapbox-gl引擎引入到项目，可以通过CDN的方式引入，也可以使用npm包安装。

## 账户要求

使用Mapbox GL JS之前需要先拥有[access_token](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/)，这个access_token可以关联你账户下的地图，更多信息可以参考[token管理文档](https://docs.mapbox.com/accounts/guides/tokens/)。

## 快速开始

- 使用CDN

在`<head>`标签中引入需要的js文件和css。css文件主要用来正确显示地图上的元素例如弹窗和标注。

```html
<script src='https://api.mapbox.com/mapbox-gl-js/v2.12.0/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/v2.12.0/mapbox-gl.css' rel='stylesheet' />
```

在`<body>`中放入如下代码：

```html
<div id='map' style='width: 400px; height: 300px;'></div>
<script>
mapboxgl.accessToken = 'pk.eyJ1Ijoid2FueWFueWFuIiwiYSI6Im1uNVZnTncifQ.90XY40_yjpItUHO8HnbbpA';
const map = new mapboxgl.Map({
  container: 'map', // container ID
  style: 'mapbox://styles/mapbox/streets-v12', // style URL
  center: [-74.5, 40], // starting position [lng, lat]
  zoom: 9, // starting zoom
});
</script>
```

- 使用包管理工具

用npm安装

```bash
npm install --save mapbox-gl
```

在`<head>`标签中引入需要css文件。css文件主要用来正确显示地图上的元素例如弹窗和标注。

```html
<link href='https://api.mapbox.com/mapbox-gl-js/v2.12.0/mapbox-gl.css' rel='stylesheet' />
```

如果使用了css预处理例如webpack的css-loader，也可以直接在js中引入css：

```js
import 'mapbox-gl/dist/mapbox-gl.css';
```

在js中通过如下代码初始化地图：

```js
import mapboxgl from 'mapbox-gl'; // or "const mapboxgl = require('mapbox-gl');"
 
mapboxgl.accessToken = 'pk.eyJ1Ijoid2FueWFueWFuIiwiYSI6Im1uNVZnTncifQ.90XY40_yjpItUHO8HnbbpA';
const map = new mapboxgl.Map({
  container: 'map', // container ID
  style: 'mapbox://styles/mapbox/streets-v12', // style URL
  center: [-74.5, 40], // starting position [lng, lat]
  zoom: 9, // starting zoom
});
```