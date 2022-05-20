<template>
  <div class="sfondo">
    <HeaderComp />

    <MainComp />

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

      apiParams:{
        api_key: '7c69e1dbf94c017daf99d092e85dc183',
        language: 'it_IT',
        query: 'ritorno al futuro',
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
      })
      .catch(err =>{
        console.log(err);
      })
    },
  },

  mounted(){
    this.getApi();
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
