
<template>

  <Header />
  <div id="app">
     <h4>Get the latest news live around the globe</h4>
     <FilterModal v-on:getfilters ="FetchResults($event)" />
    
  
      <div class="container">
      <br/>
     <Search v-on:changemessage="SearchKeyword($event)" />
     <div style="height:70px;"> </div>
  
 <div class="container"> 
  <div class="row" v-if="articles.length">
   
     <div v-for="article in articles" v-bind:key="article.id" class="card col-xs-12 col-lg-6  mb-4 p-0">
    
       <img class="card-img-top" :src="article.urlToImage"> 
   
     
      <div class="card-body">
       <h5 class="card-title" >{{article.title}}</h5>
       <p  class="card-text">{{article.description}}</p>
     
       <a :href= article.url class="btn btn-primary"  target = "_blank">Read More..</a>
      </div>
     </div>
   
  </div>
  
 </div>

  </div>
  
  <img v-if="!articles.length" id="home-image" src=".\assets\news.jpg"> 
  </div>
</template>

<script>

import axios from "axios";
import Header from "./components/Header.vue"
import Search from "./components/Search.vue"
import FilterModal from "./components/FilterModal.vue"

export default {
  name: 'App',
  components: {
      Header,
      Search,
      FilterModal
     
  },

  
  
  data() {
    return {
     
     //This array will store the fetched news articles we get back from axios
      articles: {},
      //Api_key from newsapi.org
      api_key: "e931d40e21624f788a3e964b5d8676e1",
      country: "",
      category: "",
      base_url: "http://newsapi.org/v2/top-headlines",
       //We will use this url for keyword-searching
      keyword_url: "http://newsapi.org/v2/everything?",
      keyword: "",
      
    
    }
  },
  
  

  methods: {
    
    SearchKeyword: function($event) {
      this.keyword = $event;
      axios({
          method: 'get',
          url: this.keyword_url + 'q=' + this.keyword + '&apiKey=' + this.api_key
          
        })
        .then((response) => {
            
           // console.log(response);
            this.articles = response.data.articles;
          
         }, (error) => {
            console.log(error);
        });
    },

    FetchResults: function($event) {
      this.country = $event.country;
      this.category = $event.category;
      axios({
          method: 'get',
          url: this.base_url + '?country=' + this.country + '&category=' + this.category +  '&apikey=' + this.api_key,
          
        })
        .then((response) => {
            
           // console.log(response);
            this.articles = response.data.articles;
          
         }, (error) => {
            console.log(error);
        }); 
    }
     
  }
}
</script>

<style>
  #app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   text-align: center;
   color: #2c3e50;
   margin-top: 60px;
  }

  .card-img-top {
    height: 300px;
  }
  .card-title {
    min-height: 80px;
  }
  .card-text {
    min-height: 100px;
  }
   
  #home-image {
    width:800px;
    height: 300px;
  }


</style>
