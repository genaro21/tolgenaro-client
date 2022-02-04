<template>
  <div class="tol-carrito">
    <v-container class="my-10">
      <h1>Carrito</h1>
      <v-row>
        <v-col>
          <v-data-table
            dense
            :headers="headers"
            :items="productos"
            item-key="name"
            class="elevation-1"
          >
            <template v-slot:[`item.cantidad`]="{ item }">
              <v-text-field
                v-model="cantidades[productos.indexOf(item)]"
                type="number"
                min="1"
                placeholder="cantidad"
                class="canti"
              />
            </template>
            <template v-slot:[`item.total`]="{ item }">
              <p class="my-6">
                {{ obtenerTotal(productos.indexOf(item)) + ' €' }}
              </p>
            </template>
            <template v-slot:[`item.remover`]="{ item }">
              <v-btn
                color="rgba(200,0,0,.4)"
                @click="removerItem(productos.indexOf(item))"
                >Eliminar</v-btn
              >
            </template>
          </v-data-table>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="9"></v-col>
        <v-col cols="2" class="compra izquierda">
          <p class="colorTotal">Total compra</p>
        </v-col>
        <v-col cols="1" class="compra">
          <p class="colorTotal">{{ superTotal + ' €' }}</p>
        </v-col>
      </v-row>

      <v-row class="fila-2">
        <v-btn color="rgba(0,250,0,.4)" @click="onClick">Volver a tienda</v-btn>

        <v-btn
          color="rgba(0,250,250,.4)"
          @click="finalizarCompra"
          :disabled="!(productos.length > 0)"
          >Finalizar compra</v-btn
        >
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cantidades: [],
      productos: [],
      acumulador: 0,

      headers: [
        {
          text: 'Nombre',
          value: 'nombre',
        },
        { text: 'Peso', value: 'peso' },
        { text: 'Cantidad', value: 'cantidad' },
        { text: 'Precio', value: 'precio' },
        { text: 'Total', value: 'total' },
        { text: 'Remover', value: 'remover' },
      ],
    }
  },

  mounted() {
    if (localStorage.getItem('productos')) {
      this.productos = JSON.parse(localStorage.getItem('productos'))
      for (let i = 0; i < this.productos.length; i++) {
        this.cantidades.push(1)
      }
    }
  },
  computed: {
    superTotal() {
      let index = 0
      let acumulador = 0
      for (const producto of this.productos) {
        acumulador += this.obtenerTotal(index)
        index = index + 1
      }

      return acumulador
    },
  },
  methods: {
    onClick() {
      this.actualizarProd()
      const prePage = this.$route.query.prePage
      if (prePage) {
        this.$router.push('/' + prePage)
      } else {
        this.$router.push('/home')
      }
    },
    obtenerTotal(index) {
      const resultado = this.productos[index].precio.replace('€', '')
      const value = parseFloat(resultado)
      const total = value * parseInt(this.cantidades[index])
      return total
    },
    removerItem(index) {
      this.productos.splice(index, 1)
      localStorage.setItem('productos', JSON.stringify(this.productos))
    },

    async finalizarCompra() {
      const token = localStorage.getItem('token')
      if (!localStorage.getItem('productos')) {
        alert('El carrito está vacío')
      } else {
        this.productos = JSON.parse(localStorage.getItem('productos'))
        const productsId = []
        for (let i = 0; i < this.productos.length; i++) {
          productsId.push({
            cantidad: this.cantidades[i],
            producto: this.productos[i].id,
          })
        }
        console.log('productsId: ', productsId)
        const body = {
          token,
          products: productsId,
        }

        const res = await fetch('http://localhost:4900/api/sale/createSale', {
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
        this.actualizarProd()
        this.$router.push('/finalizar_compra')
      }
    },
    actualizarProd() {
      localStorage.removeItem('pruebaprod')
      for (let i = 0; i < this.productos.length; i++) {
        const cantidad = this.cantidades[i]
        const nombreProducto = this.productos[i].nombre
        const precioProducto = this.productos[i].precio
        const pesoProducto = this.productos[i].peso
        const idProducto = this.productos[i].id

        const data = {
          cantidad,
          nombre: nombreProducto,
          precio: precioProducto,
          peso: pesoProducto,
          id: idProducto,
        }

        console.log(data)

        let pruebaprod = []

        if (localStorage.getItem('pruebaprod')) {
          pruebaprod = JSON.parse(localStorage.getItem('pruebaprod'))
        }
        pruebaprod.push(data)
        localStorage.setItem('pruebaprod', JSON.stringify(pruebaprod))
      }
    },
  },
}
</script>

<style scoped>
.fila-2 {
  display: flex;
  justify-content: space-around;
  margin-top: 50px;
  margin-bottom: 10px;
}
.liso {
  color: black;
  text-decoration: none;
}
.canti {
  width: 45px;
}
.compra {
  background-color: rgba(114, 169, 6, 0.2);
}
.colorTotal {
  margin-top: 15px;
}
.izquierda {
  padding-left: 50px;
}
</style>
