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
  onMounted(()=>{
  
        const viewer = new Cesium.Viewer('cesiumContainer', {
        // geocoder: false,
        // homeButton: false,
        // sceneModePicker: false,
        // baseLayerPicker: false,
        // navigationHelpButton: false,
        // animation: false,
        // infoBox: false,
        // selectionIndicator: false,
        // timeline: false,
        // fullscreenButton: false,
        // vrButton: false,
        // enableLighting: true,
        // shadows: true,
        // imageryProvider: new Cesium.UrlTemplateImageryProvider({
        //     url: "https://webst02.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}",
        // }),
    })
    viewer.camera.flyTo({
        destination: new Cesium.Cartesian3.fromDegrees(113.7, 34.36, 20000.0),
        duration: 3
    })
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
