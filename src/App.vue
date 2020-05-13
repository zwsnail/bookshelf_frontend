<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-btn
        href="/"
        text
      >
      <div class="d-flex align-center">
        <v-icon class="mr-2">fa fa-bible</v-icon>
        <span> Bookshelf</span>
          <!-- <i class="large fas fa-bible"></i> -->
          
        </div>  
      </v-btn>
    
      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/zwsnail/bookshelf_backend"
        target="_blank"
        text
      >
        <span class="mr-2">FIND IN github</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <!-- <category/> -->

          <router-view></router-view>
    </v-content>

  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
// import HelloWorld from './components/HelloWorld.vue';
// import category from './views/Category.vue';

export default Vue.extend({
  name: 'App',

  components: {
    // HelloWorld,
    // category,
  },

  data: () => ({
    //
  }),
});
</script>

<style>
.i {
  font-size: 5px;
}
  
</style>
