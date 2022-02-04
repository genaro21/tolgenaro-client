<template>
  <div class="tol-layout-default">
    <v-app>
      <TolHeaderPpal />
      <Nuxt />
      <TolFooter />
    </v-app>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
    }
  },
}
</script>
