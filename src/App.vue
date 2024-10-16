<script setup>
import { ref } from 'vue'
import MainHome from './components/Home.vue'
import MainNavbar from './components/Navbar.vue'

const currentComponent = ref(MainHome)
const selectComponent = component => {
  currentComponent.value = component
}
</script>

<template>
  <div id="app">
    <MainNavbar @select-component="selectComponent" />
    <component :is="currentComponent" />
  </div>
</template>

<style scoped></style>
