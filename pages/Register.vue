<template>
    <v-row>
        <v-col cols="10" offset="1" md="4" offset-md="4">
            <v-card class="mb-2">
                <v-toolbar color="primary" dark>Register</v-toolbar>
                <v-card-text>
                    <v-form>
                        <v-text-field
                            name="fullName"
                            label="Full Name"
                            type="text" 
                            :rules="rules.fullName"
                            v-model="form.fullName"/>
                        <v-text-field
                            name="email"
                            label="Email"
                            type="email" 
                            :rules="rules.email"
                            v-model="form.email"
                            @keyup="checkEmail"/>
                        <v-text-field
                            name="password"
                            label="Password"
                            type="password" 
                            :rules="rules.password"
                            v-model="form.password"/>
                        <v-text-field
                            name="retype_password"
                            label="Re-Password"
                            type="password" 
                            :rules="rules.retype_password"
                            v-model="form.retype_password"/>
                    </v-form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn @click="onSubmit" color="primary" :disabled="isDisabled">
                    <span v-if="!isDisabled">Register</span>
                    <v-progress-circular 
                    v-else color="deep-orange lighten-2" indeterminate>
                    </v-progress-circular>
                    </v-btn>
                </v-card-actions>
            </v-card>
            <p>Sudah punya akun ? <v-btn to="/login" plain>Login</v-btn></p>
        </v-col>
    </v-row>
</template>

<script>
import axios from 'axios'

export default({
    data() {
        return{
            emailExsit: false,
            isDisabled: false,
            form: {
                fullName: '',
                email: '',
                password: '',
                retype_password: '',
            },
            rules: {
                fullName: [
                    v => !!v || 'Fullname is required',
                ],
                email: [
                    v => !!v || 'Email is required',
                    v => /.+@.+/.test(v) || 'Email invalid',
                    // v => !!this.emailExsit || 'Email already exist',
                ],
                password: [
                    v => !!v || 'Password is required',
                    v => v.length >= 6 || 'Password must be at least 6 characters',
                ],
                retype_password: [
                    v => v === this.form.password || 'Re-Password must be same with password',
                ],
            }
        }
    },
    methods: {
        checkEmail() {
            axios.post('http://localhost:3000/auth/check-email', this.form).then((response) => {
                console.log(response.data)
                this.emailExsit = false
            }).catch((err) => {
                console.log(err)
                this.emailExsit = true
            });
        },
        onSubmit() {
            this.isDisabled = true
            axios.post('http://localhost:3000/auth/register', this.form).then((response) => {
                this.isDisabled = false
                this.$router.push('/login')
            })
            .catch(err => {
                this.isDisabled = false
            })
        }
    }
})
</script>
