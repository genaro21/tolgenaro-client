<template>
  <v-footer class="tol-footer" color="rgba(0,100,0,.7)" padless>
    <v-row justify="center" no-gutters>
      <v-btn
        v-for="link in links"
        :key="link.title"
        color="white"
        text
        rounded
        class="my-2"
        @click="() => onClick(link.value)"
      >
        {{ link.title }}
      </v-btn>
      <v-col class="green lighten-2 py-4 text-center white--text" cols="12">
        {{ new Date().getFullYear() }} — <strong>d´Lucas</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>
<script>
export default {
  data: () => ({
    links: [
      {
        title: 'Inicio',
        value: '/home',
      },
      {
        title: 'Aceitunas',
        value: '/aceitunas',
      },
      {
        title: 'Frutos Secos',
        value: '/frutoseco',
      },
      {
        title: 'Caramelos',
        value: '/caramelos',
      },
      {
        title: 'Carrito',
        value: '/carrito',
      },

      {
        title: 'Login',
        value: '/signIn',
      },
      {
        title: 'Registrarse',
        value: '/signUp',
      },
    ],
  }),
  methods: {
    onClick(path) {
      this.$router.push(path)
    },
  },
}
</script>
