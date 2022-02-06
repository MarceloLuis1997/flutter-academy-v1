<template>
  <v-app dark>
    <v-app-bar
      fixed
      app
    >
      <v-btn
        text
        depressed
        to="/"
      >
        My Home
      </v-btn>
      <v-btn
        text
        depressed
        to="/"
      >
        All Courses
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container class="app-container">
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {

}
</script>

<style>
.app-container {
  max-width: 95% !important;
}
</style>
