<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input type="email" required v-model="email">

    <label>Password</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError">{{ passwordError }}</div> <!-- will be false and not output if its emptyy string, will be true and output if its not empty string -->

    <label>Role: </label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill"> 

    <div v-for="skill in skills" :key="skill"> 
       <span @click="deleteSkill(skill)">{{ skill }} </span> 
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
    </div>

    <div>
        <input type="checkbox" value="bob" v-model="names">
        <label>Bob</label>
    </div>
    <div>
        <input type="checkbox" value="Susan" v-model="names">
        <label>Susan</label>
    </div>    <div>
        <input type="checkbox" value="Jim" v-model="names">
        <label>Jim</label>
    </div>

    <div class="submit">
        <button>Create an Account</button>
    </div>

  </form>

  <p> Email: {{ email }} </p>
  <p> Password: {{ password }} </p>
  <p> Role: {{ role }} </p>
  <p> Terms accepted {{ terms }} </p>
  <p> Name {{ names }} </p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'designer',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            console.log(e)
            if (e.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = '' //to clear the input field now (once the previous skill has been added)
            }
            if (!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            //validate password
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'

            if (!this.passwordError) {
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('role: ', this.role)
                console.log('skills: ', this.skills)
                console.log('terms accepted: ', this.terms)
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
    padding: 40px;
    border-radius: 10px; 
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select { 
    display: block;
    padding: 10px 6px;
    width: 100px;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px; 
}

</style>