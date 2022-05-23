<template>
  <div class="sfondo">

    <HeaderComp @movieSoarch = "selectMovie"/>
  
    <MainComp :films ="films" :tv = "tv"/>

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
      apiUrlMovie:'https://api.themoviedb.org/3/search/movie',
      apiUrlTv:'https://api.themoviedb.org/3/search/tv',
      tv: [],
      films:[],

      apiParams:{
        api_key: '7c69e1dbf94c017daf99d092e85dc183',
        language: 'it_IT',
        query: '',
      }
      
    }
  },
  
  methods:{

    // ----- film -----

    getApiMovie(){
      axios.get(this.apiUrlMovie,{
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
      this.getApiMovie();
      this.getApiTv()
      console.log(search);
    },

    // ------ Serie Tv -------
    
    getApiTv(){
      axios.get(this.apiUrlTv,{
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this.tv = res.data.results;
      })
      .catch(err =>{
        console.log(err);
      })
    },


  },
  mounted(){
  
  }
}
 
</script>

<style lang="scss">
@import './assets/style/general';
.sfondo{
  height: 400vh;
  background-image: linear-gradient(to bottom,
 rgb(0, 0, 0),rgb(46, 46, 46));
}
</style>
