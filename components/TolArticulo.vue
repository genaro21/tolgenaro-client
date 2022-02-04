<template>
  <div class="tol-article">
    <v-card class="mx-auto my-8 total" max-width="90%">
      <v-img
        class="white--text align-end imagen"
        height="200px"
        width="280px"
        :src="imagen"
      >
      </v-img>
      <v-card-title class="nombre">{{ nombre }}</v-card-title>

      <v-card-text class="text--primary">
        <v-row class="my-1">
          <v-col cols="5">{{ peso1 }}</v-col>
          <v-col cols="4">{{ precio1 }}</v-col>
          <v-col cols="3" class="mx-n4">
            <v-btn class="my-n2" @click="onClick0">
              <v-icon large color="purple darken-2">mdi-cart</v-icon>
            </v-btn>
          </v-col>
        </v-row>

        <v-row class="my-2">
          <v-col cols="5">{{ peso2 }}</v-col>
          <v-col cols="4">{{ precio2 }}</v-col>
          <v-col cols="3" class="mx-n4">
            <v-btn class="my-n2" @click="onClick1">
              <v-icon large color="purple darken-2">mdi-cart</v-icon>
            </v-btn>
          </v-col>
        </v-row>

        <v-row class="my-1">
          <v-col cols="5">{{ peso3 }}</v-col>
          <v-col cols="4">{{ precio3 }}</v-col>
          <v-col cols="3" class="mx-n4">
            <v-btn class="my-n2" @click="onClick2">
              <v-icon large color="purple darken-2">mdi-cart</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    nombre: {
      type: String,
      required: true,
    },
    peso1: {
      type: String,
      required: true,
    },
    peso2: {
      type: String,
      required: true,
    },
    peso3: {
      type: String,
      required: true,
    },
    precio1: {
      type: String,
      required: true,
    },
    precio2: {
      type: String,
      required: true,
    },
    precio3: {
      type: String,
      required: true,
    },
    imagen: {
      type: String,
      required: true,
    },
    id0: {
      type: String,
      required: true,
    },
    id1: {
      type: String,
      required: true,
    },
    id2: {
      type: String,
      required: true,
    },
  },
  methods: {
    onClick() {
      console.log(this.$route)
      const prePage = this.$route.name
      this.$router.push('/carrito?prePage=' + prePage)
    },
    onClick0() {
      const data = {
        nombre: this.nombre,
        peso: this.peso1,
        precio: this.precio1,
        id: this.id0,
      }

      if (!localStorage.getItem('token')) {
        alert('El usuario no está logueado')
      } else {
        let productos = []
        if (localStorage.getItem('productos')) {
          productos = JSON.parse(localStorage.getItem('productos'))
        }
        productos.push(data)
        localStorage.setItem('productos', JSON.stringify(productos))
        console.log(this.$route)
        const prePage = this.$route.name
        this.$router.push('/carrito?prePage=' + prePage)
      }
    },
    onClick1() {
      const data = {
        nombre: this.nombre,
        peso: this.peso2,
        precio: this.precio2,
        id: this.id1,
      }

      if (!localStorage.getItem('token')) {
        alert('El usuario no está logueado')
      } else {
        let productos = []
        if (localStorage.getItem('productos')) {
          productos = JSON.parse(localStorage.getItem('productos'))
        }
        productos.push(data)
        localStorage.setItem('productos', JSON.stringify(productos))
        console.log(this.$route)
        const prePage = this.$route.name
        this.$router.push('/carrito?prePage=' + prePage)
      }
    },
    onClick2() {
      const data = {
        nombre: this.nombre,
        peso: this.peso3,
        precio: this.precio3,
        id: this.id2,
      }

      if (!localStorage.getItem('token')) {
        alert('El usuario no está logueado')
      } else {
        let productos = []
        if (localStorage.getItem('productos')) {
          productos = JSON.parse(localStorage.getItem('productos'))
        }
        productos.push(data)
        localStorage.setItem('productos', JSON.stringify(productos))
        console.log(this.$route)
        const prePage = this.$route.name
        this.$router.push('/carrito?prePage=' + prePage)
      }
    },
  },
}
</script>

<style scoped>
.imagen {
  border-radius: 5% 25%;
}
.total {
  border-radius: 5% 25%;
}
.v-card__title {
  justify-content: center;
}
</style>
