<template>
  <div class="tol-aceitunas">
    <h1>Productos</h1>

    <TolBuscarProd
      :busquedaProducts.sync="busquedaProducts"
      :categoria="category"
    />

    <v-container>
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
      <div v-else>
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
.tol-aceitunas {
  min-height: 500px;
}
</style>

<script>
export default {
  data() {
    return {
      products: [],
      busquedaProducts: {},
      category: 'Caramelos',
    }
  },

  async mounted() {
    await this.fetch()
  },
  methods: {
    async fetch() {
      const res = await fetch('http://localhost:4900/api/product/all')
      const data = await res.json()
      console.log(data)

      this.products = data
      console.log(this.products)
    },
  },
}
</script>
