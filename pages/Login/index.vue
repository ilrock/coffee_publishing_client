<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs12 sm8 md4>
        <v-form ref="loginForm" @submit.prevent="onSubmit">
          <v-card class="elevation-12">
            <v-toolbar dark color="primary">
              <v-toolbar-title>Login</v-toolbar-title>
              <v-spacer></v-spacer>
            </v-toolbar>
            <v-card-text>
              <v-text-field 
                prepend-icon="alternate_email" 
                v-model="email" 
                label="Email" />
              <v-text-field 
                prepend-icon="lock" 
                v-model="password" 
                label="Password" 
                type="password" />
            </v-card-text>
            <v-card-actions>
              <small> I don't have an account </small>
              <v-spacer></v-spacer>
              <v-btn color="primary" type="submit">Login</v-btn>
            </v-card-actions>
          </v-card>
        </v-form>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      email: '',
      password: ''
    }
  },
  computed: {
    currentUser () {
      return this.$store.getters['users/currentUser']
    }
  },
  watch: {
    currentUser (val) {
      if (val) this.$router.replace('/')
    }
  },
  methods: {
    onSubmit () {
      this.$store.dispatch('users/login', {
        email: this.email,
        password: this.password
      })
    }
  }
}
</script>

<style>

</style>
