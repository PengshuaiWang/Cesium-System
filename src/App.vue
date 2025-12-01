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
  );
 */
  onMounted(()=>{
  
        const viewer = new Cesium.Viewer('cesiumContainer'
        , {
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
        shadows: true,
        imageryProvider :false
/*         imageryProvider:new Cesium.WebMapServiceImageryProvider({
          url:"http://t0.tianditu.gov.cn/img_w/wmts",
          SERVICE:"WMTS",
          REQUEST:"GetTile",
          VERSION:"1.0.0",
          layers:"img",
          STYLE: "default",
          FORMAT:"tiles",
          tk:"edd6461ff68afd21e432a78123ec0b08",
          TILEMATRIXSET:"w"
      })   */
    
/*         imageryProvider: new Cesium.UrlTemplateImageryProvider({
            url: "https://webst02.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}",
        }), */
    }
  )
       viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
          url:"https://t2.tianditu.gov.cn/img_w/wmts?SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=img&STYLE=default&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&TILEMATRIX=14&tk=edd6461ff68afd21e432a78123ec0b08",
          layer:"tdtBasicLayer",
          style: "default",
          format:"image/jpeg", 
          tileMatrixSetID:"GoogleMapsCompatible"
       }))
/*     viewer.camera.flyTo({
        destination: new Cesium.Cartesian3.fromDegrees(113.7, 34.36, 20000.0),
        duration: 3
    }) */
    viewer.bottomContainer.style.display = 'none';
    // viewer.cesiumWidget.creditContainer.style.display="none";// 修改样式
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
