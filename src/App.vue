<template>
  <Renderer
    ref="renderer"
    :resize="'window'"
    antialias
    shadow
    :pointer="{ intersectRecursive: true }"
  >
    <Camera :position="cameraPos" :lookAt="lookAtPos" />
    <Scene ref="scene" background="#181818">
      <Plane
        :position="{ x: 0, z: 0, y: 0 }"
        :width="10"
        :height="10"
        :rotation="{ x: -Math.PI / 2, y: 0, z: 0 }"
        ><PhysicalMaterial color="#eee" /> </Plane
      >>
      <!-- <PointLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <SpotLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <DirectionalLight
        :position="{ x: 50, z: 50 }"
        cast-shadow
        :intensity="1"
      />
      <!-- <HemisphereLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <RectAreaLight :position="{ x: 50, z: 50 }" cast-shadow :intensity="1" /> -->
      <!-- <AmbientLight cast-shadow :intensity="0.1" /> -->
      <GltfModel
        ref="model"
        src="/mac128.gltf"
        :position="{ x: 0, z: 0 }"
        @click="onClick"
      />
    </Scene>
  </Renderer>
</template>

<script>
/* eslint-disable vue/no-unused-components */
/* eslint-disable no-unused-vars */

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

export default {
  components: {
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
  },
  data() {
    return {
      timeout: null,
      cameraSwitch: false,
      cameraStartPos: { z: -0.2, y: 0.16, x: 0.55 },
      cameraEndPos: { z: 0.0, y: 0.25, x: 0.15 },
      lookAtStartPos: { z: 0, y: 0.17, x: 0 },
      lookAtEndPos: { z: 0, y: 0.2258, x: 0 },
    }
  },
  computed: {
    cameraPos() {
      return this.cameraSwitch ? this.cameraStartPos : this.cameraEndPos
    },
    lookAtPos() {
      return this.cameraSwitch ? this.lookAtStartPos : this.lookAtEndPos
    },
    pointer() {
      return this.$refs.renderer.three.pointer
    },
    test() {
      return this.$refs.scene.scene.children
        .find(({ name }) => name === 'Scene')
        .children.find(({ name }) => name === 'Glass')
    },
  },
  mounted() {
    this.setupPointer()
  },
  methods: {
    positionEqual(pos1, pos2) {
      return pos1.x === pos2.x && pos1.y === pos2.y && pos1.z === pos2.z
    },
    setupPointer() {
      // console.log(this.pointer)
    },
    onClick() {
      clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {
        this.cameraSwitch = !this.cameraSwitch
      }, 0)
    },
  },
}
</script>
