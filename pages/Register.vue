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
                            v-model="form.fullName"/>
                        <v-text-field
                            name="email"
                            label="Email"
                            type="email" 
                            v-model="form.email"/>
                        <v-text-field
                            name="password"
                            label="Password"
                            type="password" 
                            v-model="form.password"/>
                        <v-text-field
                            name="retype_password"
                            label="Re-Password"
                            type="password" 
                            v-model="form.retype_password"/>
                    </v-form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn @click="onSubmit" color="primary">Register</v-btn>
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
            form: {
                fullName: '',
                email: '',
                password: '',
                retype_password: '',
            }
        }
    },
    methods: {
        onSubmit() {
            console.log(this.form)
            axios.post('http://localhost:3000/auth/register', this.form).then((response) => {
                console.log(response.data)
            }).catch((err) => {
                console.log(err)
            });
        }
    }
})
</script>
