<template>
	<ul class="news__list">
		<li v-for="article in articles" class="news__item">{{article.title}}
		                                                   {{article.description
		                                                   {{article.urlToImage}}</li
	</ul>
</template>

<script>
export default {
	data() {
	  return {
	      articles: []
	  }
     },
     created() {
     	   let self= this;
           fetch('https://newsapi.org/v2/top-headlines?country=us',
         {

      headers: {
          'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
      }

  })
           .then(function(response){
             return response.json();
           })
           .then(function(data) {
             console.log(data);
             self.articles= data.articles;
           });

        }
           
           
     };
     
     



</script>

