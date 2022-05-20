<template>
  <div class="container ir-box d-flex flex-wrapping">

    <div  class="card" 
          v-for="(film, index) in films" :key="`film${index}`">
      <h4>{{film.original_title}}</h4>     
      <p>
        <strong>Data di uscita:</strong> {{film.release_date}}
      </p>
      <p>
        <strong>Language:</strong> {{film.original_language}}
      </p>
      <p class="sinos">
        <strong>Sinossi:</strong>
        {{film.overview}}
      </p>
      
      
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
      padding-top: 10px;
      margin-top: 150px;
      
    } 
  }
}


</style>