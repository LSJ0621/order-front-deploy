<template>
    <v-container>
        <v-row justify="center">
            <v-col cols="12" sm="2" md="4">
                <v-card>
                    <v-card-title class="text-h5 text-center">
                        로그인
                    </v-card-title>
                    <v-card-text>
                        <v-form>
                            <v-text-field
                            label="email"
                            v-model="email"
                            type="email"
                            prepend-icon = "mdi-email"
                            required
                            />
                            <v-text-field
                            label="password"
                            v-model="password"
                            type="password"
                            prepend-icon = "mdi-lock"
                            required
                            />
                            <v-row>
                                <v-col cols="12">
                                    <v-btn color="primary" block @click="doLogin()">로그인</v-btn>
                                </v-col>
                            </v-row>
                        </v-form>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import axios from 'axios';
    export default{
        data(){
            return{
                email:"",
                password:""
            }
        },
        methods: {
            async doLogin(){
                // form데이터인지 json인지 주의
                const loginData = {email: this.email,password:this.password}
                const response = await axios.post(`${process.env.VUE_APP_API_BASE_URL}/member/doLogin`,loginData)
                const token = response.data.token;
                const refreshToken = response.data.refreshToken;
                localStorage.setItem('token',token);
                localStorage.setItem('refreshToken',refreshToken);
                window.location.href = "/"
            }
        }
    }
</script>