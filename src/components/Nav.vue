<template>
  <div>
    <v-navigation-drawer fixed v-model="$store.state.drawerRight" right clipped app width="700" style="z-index:999">
      <v-layout wrap row v-if="!$store.state.loading">
        <v-flex x12 class="text-xs-center">
          <Network></Network>
        </v-flex>
      </v-layout>
    </v-navigation-drawer>
    <v-toolbar color="primary" dark fixed app clipped-right>
      <v-toolbar-title class="white--text font-weight-bold">
        Mangal -
        <span class="font-weight-regular">Ecological interactions database</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <!-- <v-btn depressed color="primary" href='#' disabled="true">
          Synthesis
          <v-icon class="pa-2">fas fa-tachometer-alt</v-icon>
        </v-btn> -->
        <v-btn depressed color="primary" href='https://github.com/mangal-wg'>
          Code
          <v-icon class="pa-2">fab fa-github</v-icon>
        </v-btn>
        <v-btn depressed color="primary" href="https://mangal.io/doc/api">
          API Doc
          <v-icon class="pa-2">fas fa-code</v-icon>
        </v-btn>
        <v-btn depressed color="primary" href="https://mangal.io/doc/r">
          R package
          <v-icon class="pa-2">fas fa-cube</v-icon>
        </v-btn>
        <v-btn depressed color="primary" href="https://mangal.io/doc/jl">
          Julia package
          <v-icon class="pa-2">fas fa-cube</v-icon>
        </v-btn>
        <v-toolbar-side-icon @click="changeStatePane"></v-toolbar-side-icon>
      </v-toolbar-items>
    </v-toolbar>
  </div>
</template>

<script>
import Network from './Network'

export default {
  methods: {
    changeStatePane () {
      this.$store.dispatch('openStatePane', !this.$store.state.drawerRight)
    }
  },
  components: {
    Network
  }
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Cardo');
  .v-toolbar__title {
    font-family: Cardo;
    font-size: 16px;
  }
  .v-icon {
    font-size: 14px
  }
</style>
