<template>
  <div id="app">
    <Sidebar />
    <div class="main" id="main-content">
      <router-view />
    </div>
  </div>
</template>

<script>
import Sidebar from './Sidebar.vue';

export default {
  components: {
    Sidebar
  }
};
</script>

<style>
@import './assets/css/style.css';
</style>
