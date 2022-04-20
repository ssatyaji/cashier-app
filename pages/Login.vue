<template>
    <v-row>
        <v-col cols="10" offset="1" md="4" offset-md="4">
            <v-card class="mb-2">
                <v-toolbar color="primary" dark>Login</v-toolbar>
                <v-card-text>
                    <v-form>
                        <v-text-field
                            name="email"
                            label="Email"
                            type="email" 
                            v-model="form.email"/>
                        <v-text-field
                            name="password"
                            label="Password"
                            type="password"
                            v-model="form.password" />
                    </v-form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn @click="onSubmit" color="primary">Login</v-btn>
                </v-card-actions>
            </v-card>
            <p>Sudah punya akun ? <v-btn to="/register" plain>Daftar disini</v-btn></p>
        </v-col>
    </v-row>
</template>

<script>
import axios from 'axios'

export default ({
    data() {
        return {
            form: {
                email: '',
                password: '',
            }
        }
    },
    methods: {
        onSubmit() {
            axios.post('http://localhost:3000/auth/login', this.form).then((response) => {
                console.log(response.data)
            })
        }
    }
})
</script>
