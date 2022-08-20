<template>
    <div class="home ">
    <div class="d-flex">
      <div>
        <sidebar />
      </div>
      <div class="header-container" style="width:90%">
         <Header />        
         <div class="edit-user">
            <div class="container">
                <div class="modal-body">
                    <form   autocomplete="off">
                        <div class="mb-3">
                            <label for="InputName" class="form-label">Name </label>
                            <input type="text" v-model="editUser.name" class="form-control" placeholder="User Name" id="InputName">
                        </div>
                        <div class="mb-3">
                            <label for="InputName" class="form-label">Surname </label>
                            <input type="text" v-model="editUser.surname"  class="form-control" placeholder="User Surname" id="InputName">
                        </div>
                        <div class="mb-3">
                            <label for="InputEmail1" class="form-label">Email </label>
                            <input type="email" v-model="editUser.email" class="form-control outline" placeholder="User Email"  id="InputEmail1">
                        </div>
                        <div class="mb-3">
                            <label for="InputPhone" class="form-label">Phone Number</label>
                            <input type="number" v-model="editUser.number"  class="form-control" placeholder="User Phone Number" id="InputPhone">
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary " @click="editUserData(editUser.id)">Edit User</button>
                </div>
            </div>
         </div>
      </div>
    </div>    
  </div>
</template>
<script>
import Header from '@/components/Header.vue'
import Sidebar from '../components/Sidebar.vue';
import axios from "axios";
export default{
    name:'Edit',
    components: 
    {Header,Sidebar},
    data(){
        return{
            userData:[],
            editUser:{
                name:'',
                surname:'',
                number:'',
                email:''
            }
        }
    },
    mounted(){
        this.getUserData(this.$route.params.id)
    },
    methods:{
        async getUserData(id){
           const res = await axios.patch(`http://localhost:3000/users/${id}`, {
              bought: true,
             });
             this.editUser=res.data
        },
        async editUserData(id){
            await axios.patch(`${`http://localhost:3000/users`}/${id}`,this.editUser);
            this.$router.push("/")
        }
    }
}
</script>
<style scoped>
  .edit-user{
    background-color: rgba(128, 128, 128, 0.223);
  height: 90vh;
  border: 1px;
  }
</style>