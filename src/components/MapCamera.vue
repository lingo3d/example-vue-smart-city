<script setup lang="ts">
import { OrbitCamera, HTML, Find } from "lingo3d-vue"

//global state that determines the selected object
//定义选中物体的全局状态
import objectSelectedState from "../states/objectSelectedState"

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  }
})

//callback that gets called when the user clicks on an object
//当用户点击物体时的回调函数
const handleClick = () => {
  if (objectSelectedState.name === props.name) objectSelectedState.name = ""
  else objectSelectedState.name = props.name
}
</script>

<template>
  <!-- find object by name, highlight outline if selected -->
  <!-- 通过名称来查询物体，选中时轮廓高亮 -->
  <Find
    :name="props.name"
    :id="props.name"
    :outline="objectSelectedState.name === props.name"
    @click="handleClick"
  >
    <!-- HTML tag that follows object -->
    <!-- 跟随物体的HTML标签 -->
    <HTML>
      <div
        class="p-2 backdrop-blur-xl absolute text-white pointer-events-auto cursor-pointer rounded-md overflow-hidden"
        @mousedown="handleClick"
      >
        {{ title }}
      </div>
    </HTML>
  </Find>
  <!-- Camera that activates when object is selected -->
  <!-- 当物体被选中时启动的相机 -->
  <OrbitCamera
    :fov="90"
    :targetId="name"
    :active="objectSelectedState.name === name"
    :transition="0.02"
    :innerZ="50"
    :innerY="-30"
    enableDamping
    :minPolarAngle="120"
    :maxPolarAngle="120"
    autoRotate
  />
</template>
