<template>
    <div class="admin">
        <h1>Administrador</h1>
        <v-card class="my-16 pa-4">
            <v-row>
                <v-col cols="3"></v-col>
                <v-col cols="6">
                
                <h3 style="margin-left: 100px;margin-bottom: 20px; background-color: orange;width: 120px;">Crear artículo</h3>
                <!-- <v-app-bar app class="mt-8"
                    color="orange"
                    height="40px">
                        <v-app-bar-title class="mx-4 my-4">Artículo</v-app-bar-title>
                </v-app-bar> -->

                <!-- <v-form action="http://localhost:4900/api/product/create" method="post" enctype="multipart/form-data"> -->
                    <input class="mx-3" type="file" name="image" ref="file" outlined>
                    <v-text-field class="mt-8 mx-3" label="Nombre" v-model="nombre" name="nombre" required outlined></v-text-field>
                    <!-- <v-text-field class="mx-3" label="Categoría" v-model="categoria" name="categoria" required outlined></v-text-field> -->
                    <v-select
                        :items="items"
                        :menu-props="{ top: true, offsetY: true }"
                        class="mx-3"
                        label="Categoría"
                        v-model="categoria" name="categoria" required outlined
                    ></v-select>
                    <div class="doblete">
                    <v-text-field class="unico" label="Peso 1" v-model="peso1" name="peso1" required outlined></v-text-field>
                    <v-text-field class="unico" label="Precio 1" v-model="precio1" name="precio1" required outlined></v-text-field>
                    <v-text-field class="unico" label="Peso 2" v-model="peso2" name="peso2" required outlined></v-text-field>
                    <v-text-field class="unico" label="Precio 2" v-model="precio2" name="precio2" required outlined></v-text-field>
                    <v-text-field class="unico" label="Peso 3" v-model="peso3" name="peso3" required outlined></v-text-field>
                    <v-text-field class="unico" label="Precio 3" v-model="precio3" name="precio3" required outlined></v-text-field>
                    </div>
                    <!-- <v-btn  @click="createArticle" color="success" block>Enviar</v-btn> -->
                    <v-btn @click="onClick" color="success">Enviar formulario</v-btn>
                <!-- </v-form> -->
                </v-col>
                <v-col cols="3"></v-col>
            </v-row>   
        </v-card>
    </div>
</template>

<style scoped>
.doblete {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;

}
.unico {
    width: 45%;
    margin: 0px 10px;
}
</style>

<script>
export default {
    data () {
        return {
            nombre: "",
            categoria: "",
            peso1: "",
            precio1: "",
            peso2: "",
            precio2: "",
            peso3: "",
            precio3: "",
            items: ['Aceitunas', 'Caramelos', 'Frutos secos'],
        }
    },
    
    methods: {
        async onClick () {
            const formData = new FormData()
            const image = this.$refs.file.files[0]
            formData.append("image", image)
            formData.append("nombre", this.nombre)
            formData.append("categoria", this.categoria)
            formData.append("peso1", this.peso1)
            formData.append("precio1", this.precio1)
            formData.append("peso2", this.peso2)
            formData.append("precio2", this.precio2)
            formData.append("peso3", this.peso3)
            formData.append("precio3", this.precio3)
            const res = await fetch("http://localhost:4900/api/product/create", {
                method: "post",
                // headers: {
                //     "Content-Type": "multipart/form-data"
                // },
                body: formData
            })
            const data = await res.json()
            console.log(data)
            this.$router.push('/admin') 
        },
        async createArticle() {
            
            const body = {
                nombre: this.nombre,
                categoria: this.categoria,
                peso1: this.peso1,
                precio1: this.precio1,
                peso2: this.peso2,
                precio2: this.precio2,
                peso3: this.peso3,
                precio3: this.precio3,
            }

            const res = await fetch('http://localhost:4900/api/product/create', {
                method: 'post',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(body),

            })

            const data = await res.json()
            if(data.error) {
                alert(data.error)
            }
            console.log({ data })

        },
        
    },

}
</script>
