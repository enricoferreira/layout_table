<template>
  <v-app>
    <!-- <TheAppBar/> -->
    <TheNavDrawer/>
    <v-main style="">
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import TheAppBar from '../src/components/TheAppBar.vue'
import TheNavDrawer from '../src/components/TheNavDrawer.vue'
export default {
  name: 'App',
  components:{
    TheAppBar,
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
</style>