<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title class="headline">
        <router-link :to="{ name: 'home' }">
          <span class="mx-auto font-weight-light white--text">Simply the </span>
          <span class="bold white--text">BEST Services</span>
        </router-link>
      </v-toolbar-title>
      <!-- 
      <v-spacer></v-spacer>
      <router-link to="/schedule">
        <v-btn v-if="!user" color="blue" class="white--text">
          Schedule
          <v-icon color="white">
            mdi-calendar
          </v-icon>
        </v-btn>
      </router-link> -->
      <v-spacer></v-spacer>
      <!-- <router-link to="/login">
        <v-btn v-if="!user" color="blue" class="white--text">
          Login
          <v-icon color="white">
            mdi-login
          </v-icon>
        </v-btn>
      </router-link> -->
      <v-btn v-if="user" @click="logout" color="black" class="white--text">
        <v-icon color="white">
          mdi-logout
        </v-icon>
        Logout
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
      <!-- <Login /> -->
    </v-main>
  </v-app>
</template>

<script>
// import Login from './components/Login.vue';
import { mapActions, mapGetters } from "vuex";
export default {
  // components: { Login },
  name: "App",

//   data: () => ({
//     //
//   }),
//   mounted() {
//     this.authAction();
//   },
  computed: {
    ...mapGetters({
      user: "auth/user",
    }),
  },
  methods: {
    ...mapActions("auth", ["authAction"]),
    async logout() {
      await this.$store.dispatch("auth/logout");
      this.$router.push("/");
    },
  },
};
</script>
