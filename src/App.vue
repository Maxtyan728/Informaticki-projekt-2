<template>
  <v-app>
    <v-app-bar app color="secondary" dark>
      <v-toolbar-title>Movie Review</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn class="mx-2"><router-link to="/">Početna</router-link></v-btn>
      <v-btn><router-link to="contact">Kontakt</router-link></v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <router-view />
      </v-container>
    </v-main>

    <v-footer app color="secondary" dark>
      <v-col class="text-center"><span class="white--text">&copy; 2024 MovieReview</span></v-col>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
.v-main{
  background-color: #D7CCC8;
}
a{
  color: white !important;
  text-decoration: none;
}
</style>
