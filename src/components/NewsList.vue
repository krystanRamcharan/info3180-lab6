<template>
<form @submit.prevent="searchNews" class= "d-flex flex-column justify-content-center">
  <div class="input-group mx-sm-3 mb-2">
    <label class="visually-hidden" for="search">Search</label>
    	<input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here"/>

    	<button class= "btn btn-primary mb-2">Search</button>
    </div>
    <p> You are searching for {{ searchTerm }}</p>
    
	<ul class="news__list">
			<li v-for="article in articles" class="news__item">{{article.title}} 
			<img class="images" :src = "article.urlToImage"/>
			{{article.description}}</li>
		                                                   
	</ul>
	</form>
</template>

<script>
export default {
	data() {
	  return {
	      articles: [],
	      searchTerm:''
	  }
     },
     created() {
     	   let self= this;
           fetch('https://newsapi.org/v2/top-headlines?country=us',
         {

      headers: {
          'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
      }

  })
           .then(function(response){
             return response.json();
           })
           .then(function(data) {
             console.log(data);
             self.articles= data.articles;
           });

        },

        methods:{
          searchNews() {
           let self= this;

           fetch('https://newsapi.org/v2/everything?q=' + self.searchTerm + '&language=en', {
           headers:
           { 
             'Authorization':`Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
             }
           })

           .then(function(response){
            return response.json();
           })
           .then(function(data){
            console.log(data);
            self.articles= data.articles;
           });
          }
        }
           
           
     };
     
     



</script>

<style>
  .news__item{
    display: grid;
    grid-template-columns:repeat(auto-fit, minmax(250px, 1fr));
    grid-gap:0.2rem;
    max-width:80rem;
    margin:5rem auto;
    padding: 0 5rem;
    grid-gap:0.2rem;
    
  }

 .images{
    width:100%;
 	height: 22vw;
 	object-fit:cover;
 	border-radius :0.75rem;

 }


</style>