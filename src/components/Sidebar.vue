<template>
  <div class="container-wrap">
    <div class="wrapper-heading">
      <h4 class="mt-2">Vue Practical</h4>
    </div>
    <div class="mt-2">
      <div class="wrapper-title">
         Dashboard
      </div>
      <router-link to="/" style="color:white"><div  class="wrapper-title">
         Users
      </div></router-link>
    </div>
  </div>
</template>
   
<script>
export default {
  name: 'sidebar',
  data(){
    return{
    }
  },
 methods: {
    ChangeT(e){
    this.layout=e
  }
 },
  created(){ 
    
  } 
}
</script>
<style scoped>
  .container-wrap {
    height: 100vh;
    width: 250px;
    background-color:rgba(31, 31, 57, 0.766);
    color: white;
    justify-content: center;
  }
 .wrapper-heading{
    display: flex;
    justify-content: center;
 }
.wrapper-title{
    font-size: 25px;
    border: 1px solid rgba(128, 128, 128, 0.364);
    height: 50px;
    background-color: rgba(31, 31, 57, 0.359);
}
</style>
