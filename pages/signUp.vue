<template>
  <div class="tol-sign-up">
    <v-card class="my-16 pa-4">
      <v-app-bar class="mt-8" color="orange" height="40px">
        <v-bar-title class="mx-4 my-4 barTitle">Regístrate</v-bar-title>
      </v-app-bar>

      <!-- <v-form action="http://localhost:4900/api/user/signUp" method="post"> -->
      <v-text-field
        class="mt-8"
        label="Nombre"
        v-model="nombre"
        name="nombre"
        outlined
      ></v-text-field>
      <v-text-field
        label="Apellidos"
        v-model="apellidos"
        name="apellidos"
        outlined
      ></v-text-field>
      <v-text-field
        label="Email"
        v-model="email"
        name="email"
        outlined
      ></v-text-field>
      <v-text-field
        label="Dirección"
        v-model="direccion"
        name="direccion"
        outlined
      ></v-text-field>
      <v-text-field
        label="Localidad"
        v-model="localidad"
        name="localidad"
        outlined
      ></v-text-field>
      <v-text-field
        label="Contraseña"
        type="password"
        v-model="password1"
        name="password1"
        outlined
      ></v-text-field>
      <v-text-field
        label="Repita contraseña"
        type="password"
        v-model="password2"
        name="password2"
        outlined
      ></v-text-field>
      <v-btn type="button" @click="onClick" color="success" block>Enviar</v-btn>
      <!-- </v-form>     -->
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'auth',
  data() {
    return {
      nombre: '',
      apellidos: '',
      email: '',
      direccion: '',
      localidad: '',
      password1: '',
      password2: '',
    }
  },
  methods: {
    async onClick() {
      const body = {
        nombre: this.nombre,
        apellidos: this.apellidos,
        email: this.email,
        direccion: this.direccion,
        localidad: this.localidad,
        password1: this.password1,
        password2: this.password2,
      }
      const res = await fetch('http://localhost:4900/api/user/signUp', {
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
      this.$router.push('/signIn')
    },
  },
}
</script>

<style scoped>
.barTitle {
  font-size: 20px;
}
</style>
