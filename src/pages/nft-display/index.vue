<script setup lang="ts">
import { onMounted, ref } from 'vue'
import type { MeshPublicInterface, RendererPublicInterface } from 'troisjs'
import { AmbientLight, Box, Camera, Group, LambertMaterial, Plane, PointLight, Renderer, Scene, StandardMaterial, Texture } from 'troisjs'
const rendererC = ref<RendererPublicInterface>()
const meshC = ref<MeshPublicInterface>()
const artwork = ref<InstanceType<typeof Group>>()
const cover = ref('https://static-test.neve.co/user_contracts/3/contracts/ade06ca9-ea88-4e28-8585-6b7bdd6c98ad/series/15/c312a5d1a9c0e3b2f82d65cf49362bdbf03eb287365d26d10da5c99ebdc41f82.jpg')

onMounted(() => {
  const renderer = rendererC.value!

  let directionRight = true
  renderer.onBeforeRender(() => {
    const y = artwork.value?.group.rotation.y || 0
    if (y > Math.PI / 4)
      directionRight = false
    else if (y < -(Math.PI / 4))
      directionRight = true

    artwork.value!.group.rotateY(directionRight ? 0.01 : -0.01)
  })
})

function setimageRatio(tex: Parameters<NonNullable<InstanceType<typeof Texture>['onLoad']>>[0]) {
  artwork.value?.group.scale.set(1.0, tex.image.height / tex.image.width, 1.0)
}
</script>

<template>
  <PhotoFrame>
    <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize alpha>
      <Camera :position="{ z: 5 }" />
      <Scene>
        <AmbientLight color="#808080" />
        <PointLight color="#ffffff" :position="{ y: 50, z: 0 }" />
        <PointLight color="#ffffff" :position="{ y: -50, z: 0 }" />
        <PointLight color="#ffffff" :position="{ y: 0, z: 0 }" />
        <PointLight color="#808080" :position="{ y: 100, z: 200 }" />
        <Group ref="artwork">
          <Box :depth="0.1" :width="1.2" :height="1.2">
            <LambertMaterial />
          </Box>
          <Plane ref="meshC" :position="{ z: 0.051 }">
            <StandardMaterial color="#ffffff">
              <Texture :src="cover" @load="setimageRatio" />
            </StandardMaterial>
          </Plane>
        </Group>
      </Scene>
    </Renderer>
  </PhotoFrame>
</template>

<style socped>
canvas {
  display: block;
}
</style>
