<template>
  <div class="sfondo">

    <HeaderComp @movieSoarch = "selectMovie"/>
  
    
    <MainComp :films ="movie" :tv = "tv" titoloCards='Film' serieCards="Serie Tv" />
    
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
      apiUrl:'https://api.themoviedb.org/3/search/',
      tv: [],
      movie:[],

      apiParams:{
        api_key: '7c69e1dbf94c017daf99d092e85dc183',
        language: 'it_IT',
        query: 'matrix',
      }
      
    }
  },
  
  methods:{

    // ----- film -----

    getApi(item = ''){
      let endPoint = 'https://api.themoviedb.org/3/movie/popular';
      if(item !== ''){
        endPoint = this.apiUrl + item;
      }else{
        item = 'movie';
      }
      console.log(endPoint);
      axios.get(endPoint,{
        params: this.apiParams
      })
      .then(res => {
        this[item]= res.data.results;
        console.log(res.data);
      })
      .catch(err =>{
        console.log(err);
      })
    },

    selectMovie(search){
      this.apiParams.query = search;
      this.getApi('movie');
      this.getApi('tv');
      console.log(search);
    },

  },

    mounted(){
      this.getApi()     
    },
};
 
</script>

<style lang="scss">
@import './assets/style/general';
.sfondo{
  height: 400vh;
  background-image: linear-gradient(to bottom,
 rgb(0, 0, 0),rgb(46, 46, 46));
}
</style>
