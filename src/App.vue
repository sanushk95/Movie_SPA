<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      results: []
    }
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

    // var xhttp = new XMLHttpRequest();
    // xhttp.onreadystatechange = function() {
    //   if(this.status == 200 && this.readyState == 4)
    //   {
    //     console.log("Connected!!!!");
    //     var res = JSON.parse(this.responseText);
    //     console.log(res);
    //   }
    // }
    // xhttp.open("get","https://api.themoviedb.org/3/discover/movie?api_key=642cd3357bcf98c5781401017fdac7d1");
    // xhttp.send();
  }
};
</script>

<style lang="scss">
* {
  ::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #777777;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #333;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #333;
}
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  scroll-behavior: smooth;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

body {
  background-color: #121212;
  color: #ccc;
}

h1 {
  color: #42b983;
}

</style>

