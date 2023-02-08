<template>
  <v-app>
    <TheNavDrawer/>
    <v-main style="">
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import TheNavDrawer from '../src/components/TheNavDrawer.vue'
export default {
  name: 'App',
  components:{
    TheNavDrawer
  },
  data: () => ({
    //
  }),
};
</script>
<style>
  .overflow-auto{
    overflow: hidden;
  }
  .overflow-hidden{
    overflow: hidden;
  }
  html{
    overflow: overlay;
  }
  td, tr, th, table{
    border: none;
    border-spacing: 0ch;
  }
</style>