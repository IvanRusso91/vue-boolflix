<template>
  <div class="container">

    <div  class="card" 
          v-for="(film, index) in films" :key="`film${index}`">

      <h3> Titolo: {{film.original_title}}</h3>
      <p> Language: {{film.original_language}} </p>
      <p> Sinossi: {{film.overview}}</p>
      <p> Data di uscita: {{film.release_date}}</p>

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

</style>