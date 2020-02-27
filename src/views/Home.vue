<template>
  <div id="main_Home"> 
    <h1>Popular Movies</h1>
<br><br>
      <div id="card_container">
          <section class="card" v-bind:key="movie.id" v-for="movie in moviesCollection">

            <img :src="`http://image.tmdb.org/t/p/w500/${movie.poster_path}`">
            <h3 class="movie_title" v-if="movie.title.length<30">{{movie.title}}</h3>
            <h3 class="movie_title" v-else>{{movie.title.slice(0,30)+' ...'}} </h3>
            <p>Popularity: {{movie.popularity}}</p>
            <p>Release date: {{movie.release_date}}</p>
            <router-link :to="`/movieDetails/${movie.id}`" class="btn">More Info</router-link>

          </section>
      </div>

    <br><br>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";
export default {
  data() {
    return {
      moviesCollection: []
    };
  },
  methods: {

  },
  created: function(){
    var vm = this;
    axios.get("https://api.themoviedb.org/3/discover/movie?api_key=642cd3357bcf98c5781401017fdac7d1")
    .then(function(response) {
      console.log(response.data.results);
      vm.moviesCollection = response.data.results;
    });
  }
};
</script>

<style lang="scss" scoped>

#main_Home {
  padding: 20px;
}

.card {
  transition: all .2s linear;
  width: 100%;
  height: 550px;
  
  padding-bottom: 10px;
  margin-bottom: 10px;
  box-sizing: border-box;
  border-radius: 10px;
  box-shadow: 10px 10px 25px #2f2f2f;

  img {
    width: 90%;
    padding: 20px;
    padding-bottom: 0;
    height: 350px;
    box-sizing: border-box;
  }

  .btn {
    text-decoration: none;
    color: #42b983;
    background: #222;
    padding: 10px 17px;
    font-weight: bold;
    display: block;
    margin-top: 45px;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;

    transition: background-color .2s linear;
  }

  .btn:hover {
    background-color: #444;
  }
}

.btn {
  text-decoration: none;
  color: #42b983;
  background: #222;
  padding: 10px 17px;
  font-weight: bold;
  margin-top: 45px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;

  transition: background-color .2s linear;
}

.card:hover {
  box-shadow: none;
  transform: translateX(10px);
}

@media screen and (min-width: 550px) {
  
  #card_container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
  }
  
  .card {
    width: 20%;
    min-width: 300px;
    margin-bottom: 20px;
    margin-right: 15px; 
  }
}

</style>
