<template>
  <div class="tol-buscar-prod">
    <v-btn class="mx-16 mt-2">
      <v-icon class="mt-4">mdi-magnify</v-icon>

      <v-text-field
        @keyup="fetch"
        placeholder="Buscar artículo"
        v-model="producto"
        name="producto"
        class="mt-8 mx-2"
        >Buscar artículo</v-text-field
      >
    </v-btn>
  </div>
</template>
<script>
export default {
  props: {
    busquedaProducts: {
      type: Object,
      required: true,
    },
    categoria: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      producto: '',
    }
  },

  mounted() {},

  methods: {
    async fetch() {
      const body = {
        nombre: this.producto,
        categoria: this.categoria,
      }

      const res = await fetch('http://localhost:4900/api/product/getName', {
        method: 'post',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(body),
      })

      const data = await res.json()
      if (data.error) {
        alert(data.error)
      }
      this.$emit('update:busquedaProducts', data)
      console.log({ data })
    },
  },
}
</script>
<style scoped></style>
