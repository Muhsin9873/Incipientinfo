<template>
 <div class="header ">
   <div class="row align-self-center ml-2">
     <div class="col title">
       <i class="fa-solid fa-bars"></i>
     </div>
     <div class="col title">
       Dashboard
     </div>
     <div class="col title">
       Users
     </div>
     <router-link to="/" style="color:white"></router-link>
   </div>
   <div class="row align-self-center" >
     <div class="col header-icons">
       <i class="fa-regular fa-bell "></i>
        <span class="badge badge-danger badge-pill">4</span>
     </div>
     <div class="col header-icons">
       <i class="fa-regular fa-envelope"></i>
       <span class="badge badge-warning badge-pill">4</span> 
     </div>
     <div class="col header-icons">
      <i class="fa-regular fa-user"></i>
     </div>
   </div>
 </div>
 
</template>
   
<script>
import Sidebar from './Sidebar.vue'
// import useEmitter from '@/EventBus'
// import { bus } from '../main';


export default {
  name: 'Header',
  components:
    {Sidebar} ,
  data(){
  },
 methods: {
 },

}
</script>
<style scoped>
.header{
  display: flex;   
  height: 70px;
  justify-content: space-between;
  border-bottom: 1px solid brown;
}
.header-icons{
width: 70px;
}
.title{
  color: gray;
  font-size: 20px;
}

</style>
