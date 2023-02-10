<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-row align="center" justify="start">
        <!-- Ссылки для роутера -->
        <v-col class="col-1">
          <v-btn depressed to="/"> Home </v-btn>
        </v-col>
        <v-col class="col-1">
          <v-btn depressed to="/about"> About </v-btn>
        </v-col>
      </v-row>
    </v-app-bar>

    <v-main>
      <!-- Сюда подставятся views исходя из роута -->
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),

  mounted() {
    this.axios.get("url").then((data) => {
      console.log(data);
    });
  },
};
</script>
