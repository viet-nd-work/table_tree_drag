<script setup>
import ProjectCard from "./components/ProjectCard.vue";
import { projects } from "./data";
</script>

<template>
  <div class="mpj_list_content flex">
    <div class="ctable-content-body">
      <project-card
        v-for="(item, index) in projects"
        :key="index"
        :data="item"
      />
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
