<template>
  <div class="sfondo">

    <HeaderComp @movieSoarch = "selectMovie" />

    <MainComp :films ="films"/>

  </div>
</template>

<script>

import HeaderComp from './components/HeaderComp';
import MainComp from './components/MainComp'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp,
  },

   data(){
    return{
      apiUrl:'https://api.themoviedb.org/3/search/movie',
      films:[],

      apiParams:{
        api_key: '7c69e1dbf94c017daf99d092e85dc183',
        language: 'it_IT',
        query: '',
      }
      
    }
  },
  
  methods:{
    getApi(){
      axios.get(this.apiUrl,{
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this.films = res.data.results;
      })
      .catch(err =>{
        console.log(err);
      })
    },

    selectMovie(search){
      this.apiParams.query = search;
      this.getApi();
      console.log(search);
    }
  },

  mounted(){
  
  }
}
 
</script>

<style lang="scss">
@import './assets/style/general';

.sfondo{
  height: 100vh;
  background-image: linear-gradient(to bottom,
 rgb(0, 0, 0),rgb(46, 46, 46));
}

</style>
