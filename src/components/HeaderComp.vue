<template>
  
  <header>
    
    <div class="container-fluid ">
      <div class="row row-cols-12 box-head">

        <div class="col left">
          <img src="../assets/img/boolflix.png" alt="">
        </div>

        <div class="col right">
          <input class="form-control" type="text" placeholder="Cerca...">
        </div>

      </div>
    </div>
      

  </header>
  
</template>

<script>
export default {
  name:'HeaderComp',
  props:{

  },
  
}

</script>

<style lang="scss" scoped>

.box-head{
  padding-top: 20px;
  .left{
    img{
      width: 130px;
      margin-left: 20px;
    }  
  }

  .right{
    display: flex;
    justify-content: end;
    margin-right: 20px;

    input{
      width: 500px;  
    }
  }
}

</style>