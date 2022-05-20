<template>
  <div class="container ir-box d-flex flex-wrapping">

    <div  class="card" 
          v-for="(film, index) in films" :key="`film${index}`">

      <h4>{{film.original_title}}</h4>
      <p> Data di uscita: {{film.release_date}}</p>
      <p> Language: {{film.original_language}} </p>
      <p class="sinos"> Sinossi: {{film.overview}}</p>

    </div>
    
    

  </div>
</template>

<script>
export default {
  name:'MainComp',

  props:{
    films: Array,
  }
}
</script>

<style lang="scss" scoped>

.ir-box{
  flex-wrap: wrap;
  justify-content: center;
  .card{
    display: flex;
    flex-wrap: wrap;
    text-align: center;
    width: 300px;
    height: 500px;
    margin: 80px 20px -30px 0px;
    padding: 10px;

    .sinos{
      text-align: left;
    
    }

  }

}


</style>