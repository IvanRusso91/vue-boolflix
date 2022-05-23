<template>
  <div class="container ir-box d-flex flex-wrapping">

    <div  class="card" 
          v-for="(film, index) in films" :key="`film${index}`">

      <!-- <img :src="`https://image.tmdb.org/t/p/w300/${film.poster_path}`">     -->
      <h4>{{film.original_title}}</h4>     
      <p>
        <strong>Data di uscita:</strong> {{film.release_date}}
      </p>
      <p>
        <strong>Language:</strong> <img :src = toUpper(film)>  
      </p>
      <p class="vote">
        
        <i v-for="(i, index) in votoPieno(film)" :key="`a${index}`" class="fa-solid fa-star"></i>

        <i v-for="(i, index) in votoVuoto(film)" :key="`c${index}`" class="fa-regular fa-star"></i>
      </p>
      <p class="sinos">
        <strong>Sinossi:</strong>
        {{film.overview}}
      </p>
      
      
    </div>
    
    <!-- Card Tv -->
    
    <div  class="card" 
          v-for="(serie, index) in tv" :key="`serie${index}`">

      <!-- <img :src="`https://image.tmdb.org/t/p/w300/${serie.poster_path}`">     -->
      <h4>{{serie.original_name}}</h4>     
      <p>
        <strong>Data di uscita:</strong> {{serie.first_air_date}}
      </p>
      <p>
        <strong>Language:</strong> <img :src = toUpper(serie)>  
      </p>
      <p  class="vote">

        <i v-for="(i, index) in votoPieno(serie)" :key="`i${index}`" class="fa-solid fa-star"></i>

        <i v-for="(i, index) in votoVuoto(serie)" :key="`b${index}`" class="fa-regular fa-star"></i>

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
      }else if( iD === 'ko'){
        iD = 'kr'
      }else if( iD === 'ur'){
        iD = 'pk'
      }
      let imgSrc = "https://www.countryflagicons.com/SHINY/32/"+ iD.toUpperCase() + ".png";
      return imgSrc;
      
    },

    votoPieno( item ){
      let grade = item.vote_average;
      grade= Math.round(grade / 2) ;
      let stellePiene = [...Array(grade).keys()].map(i => i + 1);
      return stellePiene;
    },

    votoVuoto( item ){
      let grade = item.vote_average;
      grade= Math.round(grade / 2) ;
      let stelleVuota = [...Array( 5 - grade ).keys()].map(i => i + 1);
      return stelleVuota;
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