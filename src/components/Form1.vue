<template>
    <div id="content">
        <div id="card" class="card shadow-lg mr-auto ml-auto mt-12" width="400px">
        <div class="card-title">
            <h1 class="text-center mt-3">Login</h1>
        </div>
        <div class="card-body">
            <form @submit.prevent="submit">
            <div class="form-group">
              <label class="text-lg">Email</label>
              <input 
              @blur="$v.email.$touch()"
              v-model="email" class="form-control" type="email" placeholder="Enter your email">
              <div v-if="$v.email.$error">
                <p class="p-1 text-danger" v-if="!$v.email.email"><i class="fas fa-exclamation-circle"></i>Please enter a valid email</p>
                <p class="p-1 text-danger" v-if="!$v.email.required"><i class="fas fa-exclamation-circle"></i>Email is required</p>
              </div>         
            </div>
            <div class="form-group">
              <label class="text-lg">Password</label>
              <div class="d-flex">
              <input
              @blur="$v.password.$touch()"
              v-model="password"
              class="form-control" :type="showPassword ? 'text' : 'password'"
              placeholder="Enter your password">
              <button class="" @click="showPassword = !showPassword"><i :class="showPassword ? 'fas fa-eye': 'fas fa-low-vision appearance-none'"> </i></button>
              </div>
              <div v-if="$v.password.$error">
                <p class="p-1 text-danger" v-if="!$v.password.alphaNum">Password must contain Numbers,small and capital letters.</p>
                <p class="p-1 text-danger" v-if="!$v.password.required">Password is required!!</p>
              </div>
            </div>
            <div class="form-group">
              <label class="text-lg">Pick time</label><br>
              <select class="form-control" v-model="times" id="">
                <option  v-for="time in times" :key="time" value="">{{time}}</option>
              </select>
            </div>
            <div class="form-group">
              <label class="text-lg">Pick a date</label>
              <datepicker class="form-control" style="" placeholder="Select a date"/>
            </div>
            <div class="form-group">
              <label for="">Number</label>
              <input
              @blur="$v.phoneNumber.$touch()"
              v-model="phoneNumber"
              type="text" class="form-control" placeholder="Input Phone Number">
              <div v-if="$v.phoneNumber.$error">
                <p class="p-1 text-danger" v-if="!$v.phoneNumber.integer"><i class="fas fa-exclamation-circle"></i>Numbers Only</p>
                <p class="text-danger" v-if="!$v.phoneNumber.required"><i class="fas fa-exclamation-circle"></i>Numbers is required</p>
              </div> 
            </div>
            <div class="ml-auto mr-auto mt-4 flex justify-content-center">
              <button :disabled="$v.$invalid" class="btn btn-success border-r-2" type="submit">Submit</button>
            </div>
            <p v-if="$v.$anyError" class="text-danger text-center"><i class="fas fa-exclamation-circle"></i>Please fill out the required fields</p>
            </form>
        </div>  
        </div>
    </div>
</template>
<script>
import Datepicker from 'vuejs-datepicker'
import {required,email,integer,alphaNum} from 'vuelidate/lib/validators'
export default {
  name: 'App',
  components:{
    Datepicker
  },
  data(){
      const times = [];
      for(let i = 1; i <=24; i++){
        times.push(i + ':00');
    }
    return{
      times,
      email:null,
      phoneNumber:null,
      showPassword:false,
      password:null
    }
  },
  validations:{
    email: {
      required,
      email
    },
    phoneNumber:{
      required,
      integer
    },
    password:{
      required,
      alphaNum
    }
  },
  methods:{
      submit(){
        this.$v.$touch()  //this will set the dirty flag to true in every field
        if(!this.$v.$invalid){ //then if our form is invalid our form will get submitted
          console.log('Form Submitted:', this.email);
        }
    },
    // passwordShow(){
    //     this.showPassword = !this.showPassword;
    // }
  }
}
</script>
<style scoped>
  #card{
  width: 500px;
}
body{
    background-color: black;
}
input:active{
    border: greenyellow;
}
@media (max-width:900px){
    #card{
      width: 330px;
    }
}
</style>