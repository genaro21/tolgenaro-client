<template>
  <div class="finalizar">
    <h1 class="my-12 mx-10">Finalizar compra</h1>
    <v-container>
      <v-row>
        <v-col cols="8" class="direction pr-16 mt-16">
          <v-row>
            <v-col cols="3"
              ><p class="mb-6"><b>Articulo</b></p></v-col
            >
            <v-col cols="3"
              ><p class="mb-6"><b>Peso</b></p></v-col
            >
            <v-col cols="2"
              ><p class="mb-6"><b>Precio</b></p></v-col
            >
            <v-col cols="2"
              ><p class="mb-6"><b>Cantidad</b></p></v-col
            >
            <v-col cols="2"
              ><p class="mb-6"><b>Total</b></p></v-col
            >
          </v-row>

          <v-row v-for="(prod, index) in pruebaprod" :key="prod.id">
            <v-col cols="3">
              <div>
                <p>{{ prod.nombre }}</p>
              </div>
            </v-col>
            <v-col cols="3">
              <p>{{ prod.peso }}</p></v-col
            >
            <v-col cols="2">
              <p>{{ prod.precio }}</p></v-col
            >
            <v-col cols="2">
              <p class="mx-6">
                {{ prod.cantidad }}
              </p></v-col
            >
            <v-col cols="2">
              <p>{{ obtenerTotal(index) }}</p></v-col
            >
          </v-row>
        </v-col>
        <v-col cols="4" class="factura">
          <div class="frontal">
            <h3>Resumen del pedido</h3>
            <v-row>
              <v-col cols="8">
                <p class="mt-12">Total de productos</p>
                <p>Gastos de envío</p>
                <p class="mt-12"><b>Total</b></p>
                <p class="iva">IVA incluido</p>
              </v-col>
              <v-col cols="4">
                <p class="mt-12">{{ totalCompra() }}</p>
                <p>Gratuitos</p>
                <p class="mt-12">
                  <b>{{ totalCompra() }}</b>
                </p>
              </v-col>
            </v-row>

            <v-btn class="botona" color="black">Aceptar</v-btn>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pruebaprod: [],
      acumulador: 0,
    }
  },

  mounted() {
    if (localStorage.getItem('pruebaprod')) {
      this.pruebaprod = JSON.parse(localStorage.getItem('pruebaprod'))
    }
  },
  methods: {
    obtenerTotal(index) {
      const prod = this.pruebaprod[index]
      if (!prod) {
        return 0
      }
      console.log(prod, index)
      const numero = parseFloat(prod.precio.replace('€', ''))
      return numero * prod.cantidad + ' €'
    },
    totalCompra() {
      let index = 0
      let acumulador = 0
      for (const prod of this.pruebaprod) {
        acumulador += parseFloat(this.obtenerTotal(index).replace('€', ''))
        index = index + 1
      }
      return acumulador + ' €'
    },
  },
}
</script>
<style scoped>
.frontal {
  height: 400px;
  background-color: rgba(0, 250, 0, 0.1);
  border-radius: 25px;
  box-shadow: 5px 5px 10px;
  margin-bottom: 50px;
  padding: 30px;
}

.liso {
  color: black;
  text-decoration: none;
}
.botona {
  margin-top: 60px;
  color: white;
}
.factura {
}
.direction {
  font-family: cursive;
}
.iva {
  font-size: 10px;
  margin-top: -20px;
}
</style>
