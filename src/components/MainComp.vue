<template>
<main>

  <div class="container-fluid position-relative jumbo" >
    <img :src="`https://image.tmdb.org/t/p/w1280/${jumbo[counter].backdrop_path}`">
    <div class="text-jumbo">
      <span>{{jumbo[counter].original_title}}</span>
    </div>
  </div>

  <!-- Card film -->

  <div class="box-title">
    <h1 v-if="films.length > 0 ">{{titoloCards}}</h1>
    <hr v-if="films.length > 0 ">
  </div>
  
  <div class="container ir-box d-flex flex-wrapping">

    <div  class="ir-cards flip-card" 
          v-for="(film, index) in films" :key="`film${index}`">

      <div class="flip-card-inner">    
        <div class="flip-card-front">

          <img class ="locandina" v-if="film.poster_path === null" src="../assets/img/no-poster.jpg" >

          <img class="locandina" v-else :src="`https://image.tmdb.org/t/p/w300/${film.poster_path}`">
        </div>

        <div class="flip-card-back">
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
      
      </div>    
    </div>
  </div> 

  <!-- Card Tv -->

  <div class="box-title">
    <h1 v-if="tv.length > 0 ">{{serieCards}}</h1>
    <hr v-if="tv.length > 0 ">
  </div>

  <div class="container ir-box d-flex flex-wrapping">

    <div  class="ir-cards flip-card" 
          v-for="(serie, index) in tv" :key="`serie${index}`">

      <div class="flip-card-inner">    
        <div class="flip-card-front">

           <img class ="locandina" v-if="serie.poster_path === null" src="../assets/img/no-poster.jpg" >

          <img class="locandina" v-else :src="`https://image.tmdb.org/t/p/w300/${serie.poster_path}`">
        </div>

        <div class="flip-card-back">
          <h4>{{serie.original_name}}</h4>     
          <p>
            <strong>Data di uscita:</strong> {{serie.first_air_date}}
          </p>
          <p>
            <strong>Language:</strong> <img :src = toUpper(serie)>  
          </p>
          <p class="vote">
            
            <i v-for="(i, index) in votoPieno(serie)" :key="`d${index}`" class="fa-solid fa-star"></i>

            <i v-for="(i, index) in votoVuoto(serie)" :key="`e${index}`" class="fa-regular fa-star"></i>

          </p>
          <p class="sinos">
            <strong>Sinossi:</strong>
            {{serie.overview}}
          </p>
        </div>  
      
      </div>    
    </div>
  </div> 
  
</main>  
</template>

<script>
export default {
  name:'MainComp',
  data(){
    return{
      counter: 0,
    }
  },

  props:{
    films: Array,
    tv: Array,
    jumbo: Array,
    titoloCards: String,
    serieCards: String,
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
    
    next(){
      this.counter++;
      if(this.counter > this.jumbo.length - 1){
        this.counter = 0;
      }  
    },
  },

  mounted(){
    setInterval(() =>{
      this.next();
    }, 4000)
  }
};
</script>

<style lang="scss" scoped>

.jumbo{
  width: 80%;
  display: flex;
  justify-content: center;
  align-content: center;
  height: 100vh;
  margin-top: 50px;
  overflow: hidden;
  border-radius: 150px;

  overflow: hidden;

  .text-jumbo{
    position:absolute;
    margin-top: 800px;
    font-size: 4rem;
    color: rgb(255, 255, 255);
    border-radius: 20px;
    overflow: hidden; 
    
  }

}

.box-title{
    margin: 30px 0px 0px 0px;

    h1{
      color: white;
      padding: 20px;
      margin-left: 20px;
    }
    hr{
      color: white;
    }
  }

.ir-box{
  flex-wrap: wrap;
  justify-content: center;
  
  .flip-card{
    background-color: transparent;
    width: 300px;
    height: 450px;
    perspective: 1000px;

    &:hover{
      transform: rotateY(180deg);
    }

    .locandina{
      width:300px;
      height: 450px;
    }
    .flip-card-inner{
      position: relative;
      text-align: center;
      transition: transform 0.6s;
      transform-style: preserve-3d;
      background-color: rgb(31, 31, 31);
      
      &:hover{
        transform: rotateY(180deg);
      }
      .flip-card-front{
        position: absolute;
        width: 100%;
        -webkit-backface-visibility: hidden;
        backface-visibility: hidden;
         
        .flip-card-back{
          position: absolute;
          -webkit-backface-visibility: hidden;
          backface-visibility: hidden; 
          transform: rotateY(180deg);
        }
      }
    }
  }
  .ir-cards{
    display: flex;
    text-align: center;
    margin: 80px 20px -60px 0px;
    padding: 15px;
    color: white;
    
     
    h4{
      padding: 10px;
    }

    .vote .fa-solid{
      color: yellow;
    }
    .sinos{
      text-align: left;
      height: 190px;
      overflow-x: hidden;
      padding: 10px;

      &::-webkit-scrollbar {
        width: 5px;  
      }
      &::-webkit-scrollbar-track {
        box-shadow: inset 0 0 5px grey; 
        border-radius: 10px;
      }
      &::-webkit-scrollbar-thumb {
        background: rgb(207, 2, 2); 
        border-radius: 10px;
      }
    } 
  }
}
</style>