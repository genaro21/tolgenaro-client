<template>
  <div class="tol-frutoseco">
    <h1>Frutos Secos</h1>
    <TolBuscarProd
      :busquedaProducts.sync="busquedaProducts"
      :categoria="category"
    />
    <v-container class="colocate">
      <div class="colocate" v-if="Object.values(busquedaProducts).length === 0">
        <TolArticulo
          v-for="obj in products"
          :key="obj.nombre"
          :nombre="obj.nombre"
          :peso1="obj.peso0"
          :peso2="obj.peso1"
          :peso3="obj.peso2"
          :precio1="obj.precio0"
          :precio2="obj.precio1"
          :precio3="obj.precio2"
          :imagen="obj.image"
          :id0="obj.id0"
          :id1="obj.id1"
          :id2="obj.id2"
        />
      </div>
      <div class="colocate" v-else>
        <TolArticulo
          v-for="obj in busquedaProducts"
          :key="obj.nombre"
          :nombre="obj.nombre"
          :peso1="obj.peso0"
          :peso2="obj.peso1"
          :peso3="obj.peso2"
          :precio1="obj.precio0"
          :precio2="obj.precio1"
          :precio3="obj.precio2"
          :imagen="obj.image"
          :id0="obj.id0"
          :id1="obj.id1"
          :id2="obj.id2"
        />
      </div>
    </v-container>
  </div>
</template>

<style scoped>
.colocate {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.tol-frutoseco {
}
</style>

<script>
export default {
  data() {
    return {
      products: [],
      busquedaProducts: {},
      category: 'Frutos secos',
    }
  },

  async mounted() {
    await this.fetch()
  },
  methods: {
    async fetch() {
      const res = await fetch(
        'http://localhost:4900/api/product/getCategory/Frutos secos'
      )
      const data = await res.json()
      console.log(data)
      this.products = data
    },
  },
}
</script>
