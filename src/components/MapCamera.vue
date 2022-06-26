<script setup lang="ts">
import { OrbitCamera, HTML, Find } from "lingo3d-vue";
import objectSelectedState from "../states/objectSelectedState";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  info: {
    type: String,
    required: true,
  },
});

const handleClick = () => {
  if (objectSelectedState.name === props.name) {
    objectSelectedState.name = "";
  } else {
    objectSelectedState.name = props.name;
  }
};
</script>

<template>
  <Find
    :name="props.name"
    :id="props.name"
    :outline="objectSelectedState.name === props.name"
    @click="handleClick"
  >
    <HTML>
      <div
        className="p-2 backdrop-blur-xl absolute text-white pointer-events-auto cursor-pointer rounded-md overflow-hidden"
        @click="handleClick"
      >
        {{ title }}
      </div>
    </HTML>
  </Find>
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
