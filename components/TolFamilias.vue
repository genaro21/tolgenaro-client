<template>
    <div class="tol-familias mt-4" >
            <v-row class="mx-8 my-16">
                <v-col cols="1.5"></v-col>
                <v-col cols="3">
                    <v-card class="mx-auto elemento" max-width="400">
                        <v-img
                        class="white--text align-end"
                        height="200px"
                        src="/img/images.jpg"
                        >
                        <v-card-title class="d-flex justify-center letra"></v-card-title>
                        </v-img>

                        <v-card-actions>
                        <v-btn
                            color="orange"
                            text
                            class="center"
                        >
                        <nuxt-link to="/aceitunas" class="enlace">Aceitunas</nuxt-link>
                        </v-btn>
                        </v-card-actions>
                    </v-card>
                </v-col>

                <v-col cols="3" class="mx-16" >
                    <v-card class="mx-auto elemento" max-width="400">
                        <v-img
                        class="white--text align-end"
                        height="200px"
                        src="/img/imagesf.jpg"
                        >
                        <v-card-title class="d-flex justify-center"></v-card-title>
                        </v-img>

                        <v-card-actions>
                        <v-btn
                            color="orange"
                            text
                            class="center"
                        >
                        <nuxt-link to="/frutoseco" style="text-decoration: none; color: orange">Frutos secos</nuxt-link>
                        </v-btn>
                        </v-card-actions>
                    </v-card>
                </v-col>
                <v-col cols="3">
                    <v-card class="mx-auto elemento" max-width="400">
                        <v-img
                        class="white--text align-end"
                        height="200px"
                        src="/img/images.jfif"
                        >
                        <v-card-title class="d-flex justify-center"></v-card-title>
                        </v-img>
                        <v-card-actions>
                        <v-btn
                            color="orange"
                            text
                            class="center"
                        >
                        <nuxt-link to="/caramelos" style="text-decoration: none; color: orange">Caramelos</nuxt-link>
                        </v-btn>

                        </v-card-actions>
                    </v-card>
                </v-col>
                 <v-col cols="1.5"></v-col> 
            </v-row>
    </div>
</template>

<style scoped>
.elemento {
    border-radius: 15%;
}
.center {
   margin: auto;
    font-size: 20px;
   
}

.enlace {
    text-decoration: none;
    color: orange;
    /* margin-left: -85px; */
    
}
</style>