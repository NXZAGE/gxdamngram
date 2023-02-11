<template>
  <v-app>
    <NavigationBar />

    <v-main class="px-12 py-3">
      <v-container fluid>
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import NavigationBar from "./components/NavigationBar.vue"

export default {
  name: "App",
  components: {
    NavigationBar
  }

};
</script>
