<template>
  <div id="explore">
        <h1 class="text-center">📚 Istraži bestseller knjige</h1>

        <div v-if="responseData">
            <!-- search -->
            <v-text-field @keyup="search" v-model="searchInput" label="Pretraži..." solo class="mt-6">
                <v-btn slot="append" icon color="red darken-4">
                    <v-icon
                    @click="search">
                    mdi-magnify
                    </v-icon>
                </v-btn>
            </v-text-field>

            <!-- filter input -->
            <v-row>
                <v-col
                cols="4"
                >
                <h4 class="ml-1 mt-5">Filter:</h4>
                </v-col>
                <v-col
                cols="8"
                >
                <v-select
                    :items="publishers"
                    label="Izdavač"
                    required
                ></v-select>
                </v-col>
            </v-row>

            <!-- error if search yields no results -->
        <v-alert
            v-if="errorMessage"
            color="red darken-4"
            type="success"
            >{{errorMessage}}</v-alert>

            <!-- books data -->
        <v-row>
            <v-col
            v-for="(book, i) in data"
            :key="i"
            cols="12"
            sm="6"
            md="4"
                class="d-flex flex-column"
            >
            <v-card elevation="10" rounded="lg" class="d-flex flex-column flex">
                <div>
                    <v-card-title>{{book.book_details[0].title}}</v-card-title>
                
                    <v-card-subtitle>
                        <v-icon class="mr-1">mdi-account-edit</v-icon>
                        {{book.book_details[0].author}}
                    </v-card-subtitle>

                    <v-card-text>{{book.book_details[0].description}}</v-card-text>
                </div>

                <div class="mx-4 d-flex align-end flex">
                    <a :href="book.amazon_product_url" target="_blank" rel="noopener noreferrer" class="text-decoration-none mb-4">
                        <v-btn
                        color="red darken-4"
                        outlined
                        text>
                            Kupi
                        </v-btn>
                    </a>
                </div>
            </v-card>
            </v-col>
        </v-row>

            <!-- pagination nav -->
        <nav role="navigation" v-if="!searchInput" class="my-3 d-flex flex-row justify-center">
            <v-btn class="mx-2" color="red darken-4" @click="changePage" :disabled="currentPage == 1" outlined text icon>&lt;</v-btn>
            <v-btn class="mx-2" color="red darken-4" @click="changePage" :disabled="currentPage == 2" outlined text icon>&gt;</v-btn>
        </nav>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

export default {
    name: 'Explore',

    data(){
        return {
            responseData: undefined,
            data: undefined,
            searchInput: "",
            errorMessage: "",
            currentPage: 1,
            publishers: [],
        }
    },

    methods: {
        search(){
            if(this.searchInput.length > 1){
                let searchedArray = []

                let booksData = this.responseData.results;
                booksData.forEach(element => {
                    if(element.book_details[0].title.toLowerCase().indexOf(this.searchInput.toLowerCase()) > -1){
                        searchedArray.push(element)
                    }
                });

                this.data = searchedArray;
            }else if(this.searchInput.length < 1){
                this.data = this.responseData.results
            }else {
                return
            }
            
            if(!this.data.length){
                this.errorMessage = "Nijedna knjiga nije pronađena. Pokušajte ponovno."
            }else {
                this.errorMessage = "";
            }
        },

        changePage(){
            if(this.currentPage == 1){
                this.data = this.responseData.results.slice(12,24)
                this.currentPage = 2
            } else {
                this.data = this.responseData.results.slice(0,12)
                this.currentPage = 1
            }
        }
    },

    mounted(){
        const API_BASEURL = "https://api.nytimes.com/svc/books/v3/lists.json";
        const API_KEY = "wAuNis251JjiZ017dDi7GtzS80VdL3G5";
        this.axios.get(API_BASEURL, {
            params: {
                "api-key": API_KEY,
                "list": "paperback-nonfiction"
            }
        })
        .then((response) => {
            this.responseData = response.data
            this.data = this.responseData.results.slice(0,12);

            let emptyArray = [];
            this.data.forEach(element => {
                emptyArray.push(element.book_details[0].publisher)
            })
            this.publishers = emptyArray
        })
        .catch((error) => {
            console.log(error);
        })
    }
}
</script>

<style>

</style>