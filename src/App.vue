<template>
  <div id="cesiumContainer" ref="cesiumContainer"></div>
</template>

<script setup>
  import * as Cesium from 'cesium';
  import "./Widgets/widgets.css";
  import { onMounted } from 'vue';
  window.CESIUM_BASE_URL= "/";
  Cesium.Ion.defaultAccessToken="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI2ZmJkMzFlOC0yODY3LTQxNjgtOTBjNC04NzExODQ1MDYyOTEiLCJpZCI6MzY0MzY3LCJpYXQiOjE3NjQyMjM1OTV9.jVGCqw7Ued3esQx0HKFds7DOyucN0n_VwfW4oRP-iQs";
  // const Cartesian = Cesium.Cartesian3.fromDegrees(0, 0, 500.0)
/*   Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
    113.30,//西经度
    34.36, //南纬度
    113.7, 
    34.59
  ); */


 var subdomains=['0','1','2','3','4','5','6','7'];
  onMounted(()=>{
  
        const viewer = new Cesium.Viewer('cesiumContainer', {
          geocoder: false, //是否显示搜索框
          homeButton: false, //HOME按钮
          sceneModePicker: false,//控制显示器查看模式（俯视、斜视）
          baseLayerPicker: false,//是否显示图层显示器
          navigationHelpButton: false,//是否显示帮助按钮
          animation: false, //是否播放动画
          infoBox: false,
          selectionIndicator: false,
          timeline: false,//是否显示时间轴
          fullscreenButton: false, //是否显示全屏按钮
          vrButton: false,
          enableLighting: true,
          shadows: false,
          baseLayer:new Cesium.ImageryLayer(new Cesium.WebMapTileServiceImageryProvider({
            url:"https://t{s}.tianditu.gov.cn/img_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=img&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=edd6461ff68afd21e432a78123ec0b08",
            subdomains: subdomains,
            layer: "tdtImgLayer",
            style: "default",
            maximumLevel:18,
            format: "image/jpeg",
            tileMatrixSetID: "GoogleMapsCompatible",//使用谷歌的瓦片切片方式
          
        })  )
    }
  )
       viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
          url:"http://t{s}.tianditu.com/cia_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=cia&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=edd6461ff68afd21e432a78123ec0b08",
          subdomains:subdomains,
          layer: "tdtAnnoLayer",
          style: "default",
          format: "image/jpeg",
          tileMatrixSetID: "GoogleMapsCompatible",
       }))
      viewer.camera.setView({
          destination: new Cesium.Cartesian3.fromDegrees(113.40, 34.79, 5000.0),
          duration: 3
      })
    viewer.bottomContainer.style.display = 'none';
    
    // viewer.cesiumWidget.creditContainer.style.display="none";
  });
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
  #cesiumContainer{
    width: 100vw;
    height: 100vh;
  }
</style>
