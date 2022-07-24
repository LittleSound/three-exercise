<script setup lang="ts">
import works from '~/works'
</script>

<template>
  <div space="y-6">
    <div space="y-2">
      <div i-carbon:3d-cursor text-4xl inline-block />
      <p>
        <a rel="noreferrer" href="https://github.com/LittleSound/three-exercise" target="_blank">
          3D Exercise
        </a>
      </p>
    </div>
    <div px-4>
      <div class="grid gap-x-4 gap-y-1 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3" max-w-600px mx-auto>
        <RouterLink v-for="(item, index) of works" :key="item.name" :to="item.to" class="link block mr-4 hover:text-blue">
          <pre class="mr-2 opacity-50 inline text-base">{{ String(index + 1).padStart(3, '0') }}</pre>
          <span>{{ item.name }}</span>
        </RouterLink>
      </div>
    </div>
  </div>
</template>
