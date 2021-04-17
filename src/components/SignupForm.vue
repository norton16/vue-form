<template>
    <form @submit.prevent="handleSubmit">
        <!-- v-model directive - two way data binding between form & data -->
        <label>Email:</label>
        <input type="email" required v-model="email">

        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        
        <label>Role:</label>
        <select v-model="role">
            <option value="dev">Web Developer</option>
            <option value="design">Web Designer</option>
        </select>

        <!-- <input type="checkbox" value="aaa" v-model="names">
        <label>AAA</label>
        <input type="checkbox" value="bbb" v-model="names">
        <label>BBB</label>
        <input type="checkbox" value="ccc" v-model="names">
        <label>CCC</label> -->

        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">

        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>
        
        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms</label>
        </div>

        <div class="submit">
            <button>Submit</button>
        </div>
    </form>

    <p>Email: {{ email }}</p>
    <p>Pass: {{ password }}</p>
    <p>Role: {{ role }}</p>  
    <p>Terms accepted: {{ terms }}</p>
    <p>Names: {{ names }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'dev',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        // When comma is pressed, add skill to skill array
        addSkill(e) {
            if(e.key === ',' && this.tempSkill) {
                // Check for duplicates
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ""
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            // Validate password
            this.passwordError = this.password.length > 5 ? 
            '' : 'Password must be at least 6 characters long'

            !this.passwordError && console.log('submitted')
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
        width: 100%;
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
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background: cornflowerblue;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
        cursor: pointer;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>