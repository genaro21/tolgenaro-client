<template>
  <div class="tol-header-ppal">
    <v-card class="overflow-hidden">
      <v-app-bar
        absolute
        color="#006a00"
        dark
        shrink-on-scroll
        prominent
        src="/img/images.jpg"
        fade-img-on-scroll
        scroll-target="#scrolling-techniques-3"
      >
        <template v-slot:img="{ props }">
          <v-img
            v-bind="props"
            gradient="to top right, rgba(100,115,201,.7), rgba(25,32,72,.7)"
          ></v-img>
        </template>

        <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-app-bar-title class="mx-4 my-4"
          >Frut secos y variantes GENARO</v-app-bar-title
        >
        <v-spacer></v-spacer>

        <!-- <v-btn icon class="mx-16 mt-2">
          <v-icon class="mt-4">mdi-magnify</v-icon>

          <v-text-field
            placeholder="Buscar artículo"
            id="nombre"
            class="mt-8 mx-2"
            >Buscar artículo</v-text-field
          >
        </v-btn> -->

        <div v-if="!token">
          <v-btn text class="mx-4 my-4"
            ><nuxt-link to="/signIn" class="tol-menu-link"
              >Login</nuxt-link
            ></v-btn
          >
          <v-btn text class="mx-4 my-4"
            ><nuxt-link to="/signUp" class="tol-menu-link"
              >Registrarse</nuxt-link
            ></v-btn
          >
        </div>
        <div v-else>
          <v-btn text class="mx-16 my-4" @click="logout">Logout</v-btn>
          <p>Hola {{ email }}</p>
        </div>

        <template v-slot:extension>
          <v-tabs align-with-title>
            <v-tab class="mx-4"
              ><nuxt-link to="/home" class="tol-menu-link"
                >Inicio</nuxt-link
              ></v-tab
            >
            <v-tab class="mx-4"
              ><nuxt-link to="/aceitunas" class="tol-menu-link"
                >Aceitunas</nuxt-link
              ></v-tab
            >
            <v-tab class="mx-4"
              ><nuxt-link to="/frutoseco" class="tol-menu-link"
                >Frutos Secos</nuxt-link
              ></v-tab
            >
            <v-tab class="mx-4"
              ><nuxt-link to="/caramelos" class="tol-menu-link"
                >Caramelos</nuxt-link
              ></v-tab
            >
          </v-tabs>
        </template>
      </v-app-bar>
      <v-sheet
        id="scrolling-techniques-3"
        class="overflow-y-auto"
        max-height="600"
      >
        <v-container style="height: 225px"></v-container>
      </v-sheet>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      token: undefined,
      email: '',
    }
  },
  beforeMount() {
    this.token = localStorage.getItem('token')
    this.email = localStorage.getItem('email')
  },
  methods: {
    logout() {
      localStorage.clear()
      this.token = ''
    },
  },
}
</script>

<style scoped>
.tol-menu-link {
  color: white;
  text-decoration: none;
}
</style>
