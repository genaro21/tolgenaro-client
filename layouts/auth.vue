<template>
    <div class="tol-layout-auth">
        <v-app>
            <TolHeaderPpal />    
            <v-main>
                <v-container>
                   
                    <v-row>
                        <v-col cols="3"></v-col>
                        <v-col cols="6">
                            
                            <Nuxt />
                        </v-col>
                        <v-col cols="3"></v-col>
                    </v-row>    
                </v-container>    
            </v-main>
        <TolFooter />    
        </v-app>
    </div>
</template>
<style scoped>

</style>