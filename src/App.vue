<script setup>
  import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <div class="main-page">
    <header class="header-block">
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
    </header>

    <main class="content-block"></main>
  </div>
</template>

<style scoped lang="scss">
  .main-page {
    padding: 50px;
    .header-block {
      margin-bottom: 26px;
      .logo {
        padding: 4px;
      }
    }

    .content-block {
      padding: 24px 20px;
      background-color: var(--main-bg);
      filter: drop-shadow(0px 0px 10px rgba(0, 0, 0, 0.1));
      border-radius: 10px;
    }
  }
</style>
