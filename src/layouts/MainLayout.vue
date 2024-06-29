<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="header">
      <q-toolbar>
        <!-- Logo de la NASA -->
        <img src="/src/img/nasalogo.png" class="logo" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";

defineOptions({
  name: "MainLayout",
});

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>

<style scoped>
.header {
  background-color: #212121;
}

.logo {
  max-height: 60px;
  margin-right: 60px;
}

.toolbar-title {
  flex: 1;
}
</style>
