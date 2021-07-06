<template>
    <v-content>
      <v-card width="500" class="mx-auto mt-9">
        <v-card-title>Login</v-card-title>
        <v-card-text>
          <v-text-field v-model="username" label="Username" prepend-icon="mdi-account-circle"/>
          <v-text-field v-model="password"
          label="Password" 
          :type="showPassword ? 'text' : 'password'"
          prepend-icon="mdi-lock"
          :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
          @click:append="showPassword = !showPassword"/>
        </v-card-text>

        <v-divider></v-divider>
        <v-card-actions>
          <v-btn color="success">Sign Up</v-btn>
          <v-btn @click="login" color="info">Login</v-btn>
        </v-card-actions>
      </v-card>
      <v-divider></v-divider>
      <v-card-text>
          {{ error.message }}
      </v-card-text>
    </v-content>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  data:()=> ({
    showPassword: false,
    username: "",
    password: "",
    email: "",
    error: ""
  }),
  methods: {
    ...mapActions({
        loginVue: "auth/login"
    }),
    async login() {
    try {
        await this.loginVue({
        username: this.username,
        password: this.password,
        });
        this.$router.push("/calendar");
    } catch (error) {
        this.error = error;
    }
    },
  }    
}
</script>