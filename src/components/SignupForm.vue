<template>
  <form @submit.prevent="handleSubmit">
      <label>Email:</label>
      <input type="email" required v-model="email">

      <label>Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{passwordError}}</div>
      <label>Role:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="developer">Web Designer</option>
      </select>
      <label>Skills:</label>
      <input type="text" v-model="tempSkills" @keyup="addSkill">
      <div v-for="skill in skills" :key="skill" class="pill">
         <span @click="deleteSkill(skill)"> {{skill}}</span>
      </div>
      <div class="terms">
          <input type="checkbox" required v-model="terms">
          <label>Accept terms and conditions</label>
      </div>
      <div class="submit">
          <button>Createan an Account</button>
      </div>
      <!-- <div>
          <input type="checkbox" value="Ahmet" v-model="names">
          <label>Ahmet</label>
      </div>
      <div>
          <input type="checkbox" value="Mehmet" v-model="names">
          <label>Mehmet</label>
      </div>
      <div>
          <input type="checkbox" value="Hasan" v-model="names">
          <label>Hasan</label>
      </div> -->
  </form>
  <p> Email : {{email}}</p>
  <p> Password : {{password}}</p>
  <p> Role : {{role}}</p>
  <p> Terms accepted: {{terms}}</p>
  <!-- <p> Names: {{names}}</p> -->
</template>

<script>
export default {
    data(){
        return{
            email: 'mario',
            password: '',
            role: 'designer',
            terms: false,
            tempSkills: '',
            skills:[],
            passwordError: ''
            
        }
    },
    methods: {
        addSkill(e) {
            if (e.key == ',' && this.tempSkills){
                this.skills.push(this.tempSkills)
                this.tempSkills = ''
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item)=>{
                return skill != item
            })
        },
        handleSubmit(){
            this.passwordError = this.password.length > 5 ? 
            '' : 'Error min 6 char  !!!!'
            console.log('form submitted')
            if(!this.passwordError){
                console.log('email:', this.email)
                console.log('password:', this.password)
                console.log('role:', this.role)
                console.log('skills:', this.skills)
                console.log('terms:', this.terms)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6ex;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;

    }
    input,select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color:#555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position:relative;
        top:2px;
    }
    .submit{
        text-align: center;
    }
    .error{
        color:red;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>