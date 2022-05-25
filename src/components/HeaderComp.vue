<template>
  
  <header>
    
    <div class="container-fluid ">
      <div class="row row-cols-12 box-head">

        <div class="col left">
          <img src="../assets/img/boolflix.png" alt="">
          <div class="ir-menu d-flex">
            <nav>
              <ul>
                <li>
                  <a href=""><i class="fa-solid fa-house"></i>Home</a>
                </li>
                <li>
                  <a @click="movieSelect()"  href="movie"><i class="fa-solid fa-clapperboard"></i>Films</a>
                </li>
                <li>
                  <a @click="tvSelect()" href="tv"><i class="fa-solid fa-couch"></i>Serie Tv</a>
                </li>
              </ul>
            </nav>
          </div>
        </div>
        

        <div class="col right">

          <input  v-model.trim= "search"
                  @keyup.enter= "movieSoarch"
                  class="form-control" 
                  type="text" 
                  placeholder="Cerca..." >

          <div class="utente">
            <img src="../assets/img/avatar.png" alt="avatar">
          </div>
        </div>

      </div>
    </div>
      

  </header>
  
</template>

<script>
export default {
  name:'HeaderComp',
  data(){
    return{
      search:'',
      filterType:'',
    }
  },
  methods:{
    movieSoarch(){
      this.$emit('movieSoarch', this.search);
      this.search='';
    },

    // movieSelect(){
    //   this.filterType= 'movie';
    //   this.$emit('selectMovie', this.filterType)
    // },

    //  tvSelect(){
    //   this.filterType= 'tv';
    //   this.$emit('selectTv', this.filterType)
    // },
  },
};
</script>

<style lang="scss" scoped>
.box-head{
  padding-top: 20px;
  .left{
    padding-top: 10px;
    img{
      width: 130px;
      margin-left: 20px;
    }
    .ir-menu{
      margin-left: 150px;
      margin-top: -45px;
      nav{
        ul{
          list-style: none;
          li{
            font-size: 1.2rem;
            display: inline-block;
            margin-left: 50px;
            
            a{
              text-decoration: none;
              display: flex;
              text-align: center;
              flex-direction: column;
              color: rgb(207, 2, 2);
              &:hover{
                transition: 0.5s;
                color: white;
              }
            }
          }
        }  
      }
    
    }
    
  }
  .right{
    input{
      width: 800px; 
      margin-top: 10px; 
    }
    .utente{
      width: 40px;
      border-radius: 5px;
      overflow: hidden;
      margin-left: 820px;
      margin-top: -40px;

      img{
        width: 100%;
        cursor: pointer;
      }
    }
  }
}
</style>