<template>
  <div class="sfondo">
    

    <HeaderComp @movieSoarch = "selectMovie"/>

     <div v-if="isLoading" class="load">
        <img src="./assets/img/load-boolflix.png">
      </div>

    <MainComp v-else
              :films ="movie" 
              :jumbo ="movie"
              :tv = "tv" 
              titoloCards='Film' 
              serieCards="Serie Tv" />
    
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
      isLoading: true,

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

       setTimeout(()=>{
         this.isLoading = false;
       },2000)
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
  height: 100vh;
  overflow-x:hidden ;
  padding-bottom: 100px;
  background-image: linear-gradient(to bottom,
 rgb(0, 0, 0),rgb(46, 46, 46));

  &::-webkit-scrollbar {
    width: 10px;  
  }
  &::-webkit-scrollbar-track {
    box-shadow: inset 0 0 5px grey; 
    border-radius: 10px;
  }
  &::-webkit-scrollbar-thumb {
    background: rgb(207, 2, 2); 
    border-radius: 10px;
  }

  .load {
    display: flex;
    justify-content: center;
    margin-top: 250px;
    width: 100%;
     animation: logo 2.2s linear;

    @keyframes logo {

      0%{
        transform: scale(0.5);
      }
      
      25%{
        transform: scale(0.8);
      }

      50%{
        transform: scale(1.1);
      }

      75%{
        transform: scale(1.4);
      }

      100%{
        transform: scale(1.7);
      }
    }
    
   
  }
}
</style>
