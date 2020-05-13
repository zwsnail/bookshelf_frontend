<template>
    <div>
       <!-- <ApolloQuery :query="query" :                                variables="{ id: selectedCategory }"> -->
       <ApolloQuery :query="require('@/graphql/queries/Book.gql')" :variables="{ id: $route.params.id }">
        <template slot-scope="{ result: { data, loading }, isLoading  }">
          <div v-if="isLoading ">Loading...</div>
            <div v-else class="ma-12 d-inline-flex" > 
              <div>
                <img :src="data.book.image" alt="book cover">
              </div>
              <div class="ml-10">
                <div class="title"><h2>{{ data.book.title }}</h2></div>
                <div class="mt-1"><h5>{{ data.book.author }}</h5></div>
                <div class="mt-7">{{ data.book.description }}</div>
                <div class="ma-5">
                  <v-btn class="ma-2 bt" outlined color="primary">
                    <v-icon dark>mdi-amazon</v-icon>
                     Buy In Amazon
                  </v-btn>
                </div>
                  <div class="mt-10">
                    <a href="#" class="link-margin" @click.prevent="deleteBook()">Delete Book</a>
                    <router-link :to="`/books/${data.book.id}/edit`" href="#" class="link-margin">Edit Book</router-link>
                  </div>
              </div>
            </div>
        </template>
    </ApolloQuery>
  </div>
</template>




<script>
import deleteBook from '@/graphql/mutations/DeleteBook.gql'

export default {
  methods: {
    deleteBook() {
      alert("Are you sure to delete?")
      this.$apollo.mutate({
        mutation: deleteBook,
        variables: {
          id: this.$route.params.id,
        }
      }).then(data => {
        // console.log(data)
        this.$router.push('/')
      })
    }
  }

}
</script>

<style>
.link-margin {
  margin-left: 30px;
}
.v-btn.bt:hover {
  background-color: #ffff7b;
}
.div.title {
  color: #ffff7b;
  font-weight: bolder;
}
</style>

