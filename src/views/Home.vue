<template>
  <div class="home ">
    <div class="d-flex">
      <div>
        <sidebar />
      </div>
      <div class="header-container" style="width:90%">
         <Header />        
        <div class="user-wrapper">
          <div class="container">
             <div class="user-create-wrapper ">
               <div class="title">
                  Users
               </div>
               <div>
                 <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#createUserModal">Create User</button>
               </div>
             </div>
             <hr style="width:103%;margin-left:-15px">
             <div style="height:500px">
              <table  style="color:black" class="table table-striped table-hover">
                    <thead>
                        <tr >
                            <th></th>
                            <th >Name </th>
                            <th>Surname</th>  
                            <th>Email</th>   
                            <th>Phone Number</th>
                            <th>Action</th>                                          
                        </tr>
                    </thead>
                    <tbody v-if="tasks.length!=0">
                        <tr :key="task.id" v-for="task in tasks" >
                            <td></td>
                            <td>{{task.name}}</td>
                            <td>{{task.surname}}</td>
                            <td>{{task.email}}</td>
                            <td>{{task.number}}</td>
                            <td>
                             <button type="button" @click="editUserFun(task.id)" class="btn btn-primary">Edit</button>
                              <button type="button" class="btn btn-primary ml-2"  data-toggle="modal" data-target="#deleteModal" @click="deleteIdFun(task.id)">Delete</button>
                            </td>
                        </tr>
                    </tbody>
               </table>
             </div>
          </div>
        </div>
      </div>
    </div>
    <!--Create user Modal-->
    <div class="modal fade" data-bs-backdrop="static" data-bs-keyboard="false" id="createUserModal" tabindex="-1"
        aria-labelledby="ModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="ModalLabel">Create User</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form   autocomplete="off">
                        <div class="mb-3">
                            <label for="InputName" class="form-label">Name </label>
                            <input type="text"  class="form-control" v-model="userData.name" placeholder="User Name" id="InputName">
                        </div>
                        <div class="mb-3">
                            <label for="InputName" class="form-label">Surname </label>
                            <input type="text" v-model="userData.surname" class="form-control" placeholder="User Surname" id="InputName">
                        </div>
                        <div class="mb-3">
                            <label for="InputEmail1" class="form-label">Email </label>
                            <input type="email" v-model="userData.email" class="form-control outline" placeholder="User Email"  id="InputEmail1">
                        </div>
                        <div class="mb-3">
                            <label for="InputPhone" class="form-label">Phone Number</label>
                            <input type="number" v-model="userData.number" class="form-control" placeholder="User Phone Number" id="InputPhone">
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary " @click="submited()" data-bs-dismiss="modal">Add Details</button>
                </div>
            </div>
        </div>
    </div>
  </div>

  <!--Delete user modal-->
  <div class="modal fade" id="deleteModal" tabindex="-1" role="dialog" aria-labelledby="deleteModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="delteModalLabel">Alert</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        Do You Want to delete
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">No</button>
        <button type="button" class="btn btn-primary" @click="deleteUser(deleteId)" >Yes</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>

import Header from '@/components/Header.vue'
import Sidebar from '../components/Sidebar.vue';
import axios from "axios";
export default {
  name: 'Home',
  components: 
    {Header,Sidebar},

  data(){
    return{
      tasks:[],
      deleteId:'',
      userData:{
          name:'',
          surname:'',
          number:'',
          email:''
      }
    }
  },
   async created() {
    try {
      const res = await axios.get(`http://localhost:3000/users`);
      this.tasks = res.data;
      console.log("users",this.tasks);
    } catch (error) {
      console.log(error);
    }
  },
  methods:{

   async submited(){
      console.log("name",this.userData);
      const res = await axios.post(`http://localhost:3000/users`,this.userData);
      window.location.reload()
    },

    async deleteUser(id){
      axios.delete(`http://localhost:3000/users/${id}`)
      window.location.reload()
    },
    editUserFun(id){
      this.$router.push("/edit/"+id)
    },
    deleteIdFun(id){
      this.deleteId=id
    }
  }
  
}
</script>
<style>
.user-wrapper{
  background-color: rgba(128, 128, 128, 0.223);
  height: 90vh;
  border: 1px;
}
.title{
  color: gray;
  font-size: 20px;
}
.container{
  background-color: white;
  border: 1px solid rgba(46, 45, 45, 0.608);
}
.user-create-wrapper{
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 60px;
  /* border: 1px solid red;  */
}
</style>