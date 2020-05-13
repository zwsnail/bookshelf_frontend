<template>
  <div>
    <div v-if="message === 'success'">
        <v-alert
        dense
        text
        type="success"
        :value="ture"
        >
        Created a new book!
        </v-alert>
    </div>

    <v-parallax

        src="../assets/hero.svg"
    >
        <v-row
        align="center"
        justify="center"
        >
        <v-col class="text-center animated zoomIn" cols="12" 
        style="background-color: #2076d270; width: 500px"

        >
            <h1 class="display-1 mb-4" style="font-color:#212121">Book recommendation site built with GraphQL</h1>
            <h4 class="subheading">Built with Laravel (Lighthouse GraphQL), Vue.js (vue-apollo) and Vuetify.js</h4>
        </v-col>
        </v-row>
    </v-parallax>


  <div class="home ma-12">
        <div class="side-menu ma-10">  
            <ApolloQuery :query="categoriesQuery">
                <template slot-scope="{ result: { data, loading }, isLoading }">
                <div v-if="isLoading">Loading...</div>
                <div v-else>
                <router-link to="/books/add">
                <v-btn class="mb-1" color="primary">Add Book</v-btn>
                </router-link>  <!-- Apollo Query -->
                    <a href="#" class="ma-5" @click.prevent="getCategory('all')">All Books</a>
                    <a href="#" class="ma-5" @click.prevent="getCategory('featured')">Featured Books</a>
                    <a v-for="category of data.categories" :key="category.id" class="ma-5"
                    @click.prevent="getCategory(category.id)">
                    {{ category.name }}
                    </a>
                </div>
                </template>
            </ApolloQuery>
        </div>

      
        <div v-if="selectedCategory === 'all'">
            <v-container cols="12" >
                <ApolloQuery :query="query">
                    <template slot-scope="{ result: { data, loading }, isLoading  }">
                       <div v-if="isLoading">Loading...</div>
                         <div v-else class="d-flex flex-wrap">
                            <v-row v-for="book of data.books" :key="book.id"
                            class="ma-10"> 
                              <v-col style="width:200px">   
                              <book-listing :book="book"></book-listing>
                              </v-col>
                            </v-row>
                        </div>
                    </template>
                </ApolloQuery>
            </v-container>
        </div>
       

        <div v-else-if="selectedCategory === 'featured'">
          <v-container cols="12" >
            <ApolloQuery :query="query" :variables="{featured: true }">
              <template slot-scope="{ result: { data, loading }, isLoading  }">
                <div v-if="isLoading">Loading...</div>
                    <div v-else class="d-flex flex-wrap">
                        <v-row v-for="book of data.booksByFeatured" :key="book.id">
                          <v-col style="width:200px"> 
                            <book-listing :book="book"></book-listing>
                          </v-col>
                        </v-row>
                    </div>
                </template>
            </ApolloQuery>
           </v-container>
        </div>

            <div v-else>
              <v-container cols="12" >
                <ApolloQuery :query="query" :variables="{ id: selectedCategory }">
                  <template slot-scope="{ result: { data, loading }, isLoading  }">
                    <div v-if="isLoading">Loading...</div>
                      <div v-else class="d-flex flex-wrap">
                        <v-row  v-for="book of data.category.books" :key="book.id">
                          <v-col style="width:200px"> 
                            <book-listing :book="book"></book-listing>
                          </v-col>
                      </v-row>
                    </div>
                  </template>
                </ApolloQuery>
              </v-container>
            </div>
    <!-- home -->
  </div>  

</div>


</template>

<script>
import categoryQuery from '@/graphql/queries/Category.gql'
import categoriesQuery from '@/graphql/queries/Categories.gql'
import booksQuery from '@/graphql/queries/Books.gql'
import booksFeaturedQuery from '@/graphql/queries/BooksFeatured.gql'
import bookListing from '@/components/BookListing.vue'

  export default {
    name: 'home',
    components: {
        bookListing
    },
    data() {
      return {

          categoriesQuery,
          categoryQuery, //  same as categoryQuery: categoryQuery
          booksQuery,
          booksFeaturedQuery,

          categories: [],
          books:[],
          selectedCategory: 'all',
          query: booksQuery, //用来配上面那FeaturedQuery还是all
          message: ''


      }
    },
    created() {


        // this.message = this.$route.params.message

    },
    methods: {
        getCategory(category) {
            if(category === 'all'){
                this.query = booksQuery
            }else if(category === 'featured'){
                this.query = booksFeaturedQuery
            }else{
                this.query = categoryQuery
            }
            //下面是根据id来选
            this.selectedCategory = category

            this.message = this.$route.query.message
            console.log(this.message);
        }
    }
  }
</script>

<style>
 .home {
    padding: 30;
 }
 .display-books {
     display: d-flex flex-wrap;
 }
 .side-menu {
     margin-left: 50;
 }


</style>