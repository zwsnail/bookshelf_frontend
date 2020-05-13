<template>
  <div>
    <router-link :to="`/books/${book.id}`"> 
      <v-row justify="center" wrap>
        <img :src="book.image" alt="cover image" class="center">
      </v-row>
    </router-link>


    <router-link :to="`/books/${book.id}`" class="text-center">
          <v-row justify="center">
      <div>{{ book.title }}</div>
            </v-row>
    </router-link>
          <v-row justify="center">
    <div class="text-center">{{ book.author }}</div>
          </v-row>
  </div>
</template>

<script>
export default {
  props: ['book']
}
</script>
<style>
.booklist {
  width: 400;
}
  
</style>