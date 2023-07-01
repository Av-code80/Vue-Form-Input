<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");

const role = ref("");

const terms = ref(false);
const names = ref([]);

const tempSkill = ref("");
const skills = ref([]);

const passwordError = ref('')

const addSkill = (e) => {
  if (e.key == "," && tempSkill.value) {
    if (!skills.value.includes(tempSkill.value)) {
      // or skills.value = skills.value.filter((el) => el !== tempSkill.value)
      skills.value.push(tempSkill.value);
    }
    tempSkill.value = "";
  }
};

const handleDelete = (index) => {
    skills.value = skills.value.filter((item) => item !== index)
//  or skills.value.splice(index, 1)
}

const handleSubmit = () => {
   passwordError.value = passwordError.value.length > 5 ? '' : 'Password should be at least 5 caracters'
   
if(!passwordError.value) {
    console.log('email', email.value)
    console.log('role', role.value)
    console.log('skils', skills.value)
    console.log('terms accepted', terms.value)
    console.log('email', email.value)
}
}

</script>

<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Email:</label>
    <input type="email" required v-model="email" />

    <label for="">Password</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label for="">Role:</label>
    <select name="role" id="role" v-model="role">
      <option value="web developer">Web developer</option>
      <option value="web designer">Web designer</option>
    </select>

    <label for="">Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" placeholder="finish typing with ',' " />
    <div class="pill" v-for="skill in skills" :key="skill" >
      <span @click="handleDelete(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept Terms and Conditions</label>
    </div>

    <div class="submit">
        <button>Create an Acount</button>
    </div>

   
  </form>
</template>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
.terms {
    margin-top: 20px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px, 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="chekbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background:  #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color:#777;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}

.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>
