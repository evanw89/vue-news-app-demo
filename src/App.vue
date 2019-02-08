<template>
  <div id="app" class="container-fluid">
    <h1>{{ customContent }}</h1>
    <div class="row">
      
      <app-search v-on:newsChanged="getNews"></app-search>

    </div>
    <div class="row">
      <app-article
        v-for="newsArticle in articles"
        v-bind:data="newsArticle"></app-article>
    </div>
  </div>

</template>

<!-- ____________________________________________ -->

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Article from './components/Article.vue';
import Search from './components/Search.vue';

export default {
  data: function() {
    return {
      articles: [],
      customContent: 'Hello world',
      searchQ: 'politics'
    }
  },
  methods: {
    getNews: function(query) {
      var that = this;
      var url = 'https://newsapi.org/v2/everything?' +
          // 'country=us&' +
          'q=' + query + '&' +
          'apiKey=eb85487dcf1d45d5aa52c973e59ad105';
      var req = new Request(url);
    
      fetch(req)
        .then(function(response) {
            return response.json();
        })
        .then(function(data) {
          console.log(data);
          that.articles = data.articles;
        })

       this.searchQ = '';
    }
  },
  components: {
    'app-article': Article,
    'app-search': Search
  },
  mounted: function() {

    this.getNews(this.searchQ);

  }
}
</script>

<!-- ____________________________________________ -->

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
