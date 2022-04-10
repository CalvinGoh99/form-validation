<template>
    <h1>Sign Up Form</h1>

    <form @submit.prevent="Submit"> 
        <div class="signup-container">
            <div class="signup-info">
                <label class="signup-label">First name</label>
                <input type="text" v-model="fname">
                <div v-show="fnameError">
                    <p class="error-message">{{ fnameError }}</p>
                </div>
            </div>
            <div class="signup-info">
                <label class="signup-label">Last name</label>
                <input type="text" v-model="lname">
                <div v-show="lnameError">
                    <p class="error-message">{{ lnameError }}</p>
                </div>
            </div>

            <div class="signup-info">
                <label class="signup-label">Email</label>
                <input type="email" v-model="email">
                <div v-show="emailError">
                    <p class="error-message">{{ emailError }}</p>
                </div>
            </div>

            <div class="signup-info">
                <label class="signup-label">Password</label>
                <input type="password" v-model="password">
                <div v-show="passwordError">
                    <p class="error-message">{{ passwordError }}</p>
                </div>    
            </div>

            <div class="signup-info">
                <label class="signup-label">Confirm password</label>
                <input type="password" v-model="confirmPassword">
                <div v-show="confirmpasswordError">
                    <p class="error-message">{{ confirmpasswordError }}</p>
                </div>
            </div>

            <div>    
                <button type="submit" class="signup">Submit</button>
            </div>
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue'

    const fname = ref('')
    const lname = ref('')
    const email = ref('')
    const password = ref('')
    const confirmPassword = ref('')
    const fnameError = ref('')
    const lnameError = ref('')
    const emailError = ref('')
    const passwordError = ref('')
    const confirmpasswordError = ref('')

    const Submit = () => {
        
        //Validation
        fnameError.value = lname.value.length < 1 ? 'First name is required' 
        : fname.value.length < 5 ? 'First name must be at least 5 characters' : ''

        lnameError.value = lname.value.length < 1 ? 'Last name is required' 
        : lname.value.length < 5 ? 'Last name must be at least 5 characters' : ''

        let emailDomain = email.value.substring(email.value.length-10)
        emailError.value = email.value.length < 1 ? 'Email is required' 
        : emailDomain != '@gmail.com' ? 'Email must end with @gmail.com' : ''

        let regularExpression = /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$/
        passwordError.value = password.value.length < 1 ? 'Password is required' 
        : !regularExpression.test(password.value) ? 'Password must contain atleast : 8 characters, 1 number and 1 special characters (@, #, $ and etc)' : ''
        
        confirmpasswordError.value = (confirmPassword.value != password.value) ? 'Confirm password must be same as password' : ''

        // Check password and confirm password matches
        console.log(password.value)
        console.log(confirmPassword.value)

        //If validated successfully
        if(fnameError.value == '' &&
        lnameError.value == '' &&
        emailError.value == '' &&
        passwordError.value == '' &&
        confirmpasswordError.value == '') {
            alert('Succesfully Submitted')
        }
    }

</script>

<style>
.error-message{
    color: red;
    font-size: 0.8rem;
    margin: 5px 0 0 0;
}

.signup-container {
    margin: 0 35rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.signup-info {
    display: inline-flex;
    flex-direction: column;
    padding: 0px 0px 12px 0px;
}

.signup-label{
    display: flex;
    flex-direction: start;
    padding-bottom: 5px;
}

.signup {
    background-color: #f1f1f1;
    border: 1px solid;
    border-radius: 4px;
    padding: 1rem 3.5rem;
    margin: 1rem 0;
}

input{
    padding: 5px;
    font-size: 1rem;
    border: 0.05rem solid #90959b;
    border-radius: 4px;
}
</style>