<template>
  <v-app>
    <TheAppBar/>
    <TheNavDrawer/>
    <v-main style="height: 10000px">
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
