<template>
  <div class="container ir-box d-flex flex-wrapping">

    <div  class="card" 
          v-for="(film, index) in films" :key="`film${index}`">

      <img :src="`https://image.tmdb.org/t/p/w300/${film.poster_path}`">    
      <h4>{{film.original_title}}</h4>     
      <p>
        <strong>Data di uscita:</strong> {{film.release_date}}
      </p>
      <p>
        <strong>Language:</strong> <img :src = toUpper(film)>  
      </p>
      <p class="vote">
        {{film.vote_average}}
      </p>
      <p class="sinos">
        <strong>Sinossi:</strong>
        {{film.overview}}
      </p>
      
      
    </div>
    
    <!-- Card Tv -->
    
    <div  class="card" 
          v-for="(serie, index) in tv" :key="`serie${index}`">

      <img :src="`https://image.tmdb.org/t/p/w300/${serie.poster_path}`">    
      <h4>{{serie.original_name}}</h4>     
      <p>
        <strong>Data di uscita:</strong> {{serie.first_air_date}}
      </p>
      <p>
        <strong>Language:</strong> <img :src = toUpper(serie)>  
      </p>
      <p class="vote">
        {{serie.vote_average}}
      </p>
      <p class="sinos">
        <strong>Sinossi:</strong>
        {{serie.overview}}
      </p>
      
      
    </div>



  </div>
</template>

<script>
export default {
  name:'MainComp',
  props:{
    films: Array,
    tv: Array,
  },

  methods:{

    toUpper(item){
      let iD = item.original_language;
      if(iD === 'en'){
        iD = "gb" 
      }else if( iD === 'ja'){
        iD = "jp"
      }
      let imgSrc = "https://www.countryflagicons.com/SHINY/32/"+ iD.toUpperCase() + ".png";
      return imgSrc;
      
    },


  },
};
</script>

<style lang="scss" scoped>
.ir-box{
  flex-wrap: wrap;
  justify-content: center;
  .card{
    position: relative;
    display: flex;
    flex-wrap: wrap;
    text-align: center;
    width: 300px;
    height: 400px;
    margin: 80px 20px -30px 0px;
    padding: 15px;
    overflow-x: hidden;
    overflow-x: scroll;
    &::-webkit-scrollbar{
      display: none;
    
    }
    
    h4{
      padding-bottom: 10px;
    }
    .sinos{
      position: absolute;
      text-align: left;
      padding-top: 50px;
      margin-top: 150px;
      
    } 
  }
}
</style>