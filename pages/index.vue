<template>
  <div class="tol-index">
    <h1>Index</h1>
    <TolArticle />
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
</template>

<script>
export default {
  data() {
    return {
      products: [],
    }
  },
  mounted() {
    this.$router.push('/home')
  },
}
</script>
