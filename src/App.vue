<template>
  <Renderer ref="renderer" :resize="'window'" antialias shadow>
    <Camera
      :position="{ z: -0.2, y: 0.16, x: 0.55 }"
      :lookAt="{ z: 0, y: 0.17, x: 0 }"
    />
    <Scene ref="scene" background="#181818">
      <Plane
        :position="{ x: 0, z: 0, y: 0 }"
        :width="10"
        :height="10"
        recieve-shadow
        :rotation="{ x: -Math.PI / 2, y: 0, z: 0 }"
        ><PhysicalMaterial color="#eee" />
      </Plane>>
      <!-- <PointLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <SpotLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <DirectionalLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" />
      <!-- <HemisphereLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <RectAreaLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <AmbientLight cast-shadow :intensity="0.1" /> -->
      <GltfModel
        src="/mac128.gltf"
        @load="onModelLoaded"
        @progress="onProgress"
        @error="onError"
        :position="{ x: 0, z: 0 }"
        cast-shadow
        recieve-shadow
      />
    </Scene>
  </Renderer>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

import {
  GltfModel,
  Box,
  Camera,
  LambertMaterial,
  PointLight,
  AmbientLight,
  SpotLight,
  DirectionalLight,
  HemisphereLight,
  RectAreaLight,
  Renderer,
  Scene,
  SphereGeometry,
  PhongMaterial,
  PhysicalMaterial,
  InstancedMesh,
  Plane,
} from 'troisjs'

const scene = ref(null)

function onModelLoaded(object) {
  console.log('model loaded')
}
function onLoad(object) {
  console.log(object)
}
function onProgress(object) {
  // console.log(object)
}
function onError(err) {
  console.log(err)
}

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>
