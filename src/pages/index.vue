<script setup lang="ts">
function handleCopyUrl() {
}
const iconList = ref([
  'https://api.iconify.design/ri:macbook-fill.svg?color=%23888888',
  'https://api.iconify.design/fa6-brands:js-square.svg?color=%23888888',
  'https://api.iconify.design/mdi:github-box.svg?color=%23888888',
])
</script>

<template>
  <div>
    <h1 text-size-14>
      fine-icons
    </h1>
    <div container>
      <ul>
        <li
          v-for="icon in iconList" :key="icon"
          flex items-center justify-center gap-4
        >
          <img :src="icon" alt="">
          <div w-60 truncate>
            {{ icon }}
          </div>
          <button @click="handleCopyUrl">
            COPY
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>
