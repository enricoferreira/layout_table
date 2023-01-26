<template>
  <v-app>
    <TheAppBar/>

    <v-main style="height: 10000px">
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import TheAppBar from '../src/components/TheAppBar.vue'
export default {
  name: 'App',
  components:{
    TheAppBar
  },
  data: () => ({
    //
  }),
};
</script>
