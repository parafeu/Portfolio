<template>
  <div>
    <div class="am-background-top"></div>
    <Nuxt />
  </div>
</template>

<style lang="scss">
.am-background-top {
  @apply w-full fixed bg-gradient-to-br from-indigo-100 to-indigo-300;
  z-index: -1;
  height: 75vh;
  border-bottom-left-radius: 100px;
  top: calc(-75vh + 100px);
}
</style>