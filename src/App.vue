<script setup lang="ts">
import { World, OrbitCamera, Model } from "lingo3d-vue"
import MapCamera from "./components/MapCamera.vue"

//global state that determines the selected object
//定义选中物体的全局状态
import objectSelected from "./states/objectSelectedState"
</script>

<template>
  <World defaultLight="env.hdr" color="rgb(0, 0, 25)">

    <!-- default camera, active when no object is selected -->
    <!-- 默认相机，没有选中任何物体时启动 -->
    <OrbitCamera
      :fov="90"
      :active="objectSelected.name === ''"
      :transition="0.02"
      :innerZ="223.68"
      enableZoom
      enableDamping
      autoRotate
      :minPolarAngle="100"
    />

    <!-- map model -->
    <!-- 地图模型 -->
    <Model
      :metalnessFactor="0.5"
      :roughnessFactor="0.5"
      pbr
      :y="46.67"
      :width="552.32"
      :depth="572.75"
      src="shanghai.glb"
    >
      <!-- three zoomable cameras that focus on selected objects -->
      <!-- 三个可缩放，并且可以聚焦到选中物体的相机 -->
      <MapCamera name="01-shanghaizhongxindasha" title="Shanghai Tower" />
      <MapCamera
        name="02-huanqiujinrongzhongxin_huanqiujinrongzhongxin_0"
        title="Shanghai World Financial Center"
      />
      <MapCamera name="03-jinmaodasha_jjinmaodasha_0" title="Jin Mao Tower" />
      <MapCamera
        name="04-dongfangmingzhu_dongfangmingzhu_0"
        title="Oriental Pearl Tower"
      />
    </Model>
  </World>
</template>
