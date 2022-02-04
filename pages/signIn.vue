<template>
  <div class="tol-sign-in">
    <v-card class="my-16 pa-4">
      <v-app-bar class="mt-8" color="orange" height="40px">
        <v-bar-title class="mx-4 my-4 barTitle">Login</v-bar-title>
      </v-app-bar>

      <v-text-field
        class="mt-8"
        label="Email"
        v-model="email"
        name="email"
        outlined
      ></v-text-field>
      <v-text-field
        label="Password"
        type="password"
        v-model="password"
        name="password"
        outlined
      ></v-text-field>
      <v-btn type="button" @click="onClick" color="success" block>Enviar</v-btn>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'auth',
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    async onClick() {
      const body = {
        email: this.email,
        password: this.password,
      }
      const res = await fetch('http://localhost:4900/api/user/signIn', {
        method: 'post',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(body),
      })

      const data = await res.json()
      if (data.error) {
        alert(data.error)
        return
      }
      console.log({ data })
      const token = data.token
      const email = data.user.email

      localStorage.setItem('token', token)
      localStorage.setItem('email', email)
      this.$router.push('/home')
    },
  },
}
</script>

<style scoped>
.barTitle {
  font-size: 20px;
}
</style>
