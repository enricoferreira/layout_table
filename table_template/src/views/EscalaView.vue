<template>
    <div>
        <v-app-bar dense app elevate-on-scroll color="white">
            <v-app-bar-title>
                Nome escala
            </v-app-bar-title>
            <v-spacer></v-spacer>
            <v-btn color="" small class="mr-2" icon>
                <v-icon size="21">mdi-printer</v-icon>
            </v-btn>
            <v-btn icon class="mr-2" small color="">
                <v-icon size="21">mdi-bell</v-icon>
            </v-btn>
            <template v-slot:extension>
                <v-tabs align-with-title>
                    <v-tab>Assistentes | 1</v-tab>
                    <v-tab>Caixa | 4</v-tab>
                    <v-tab>Farma | 3</v-tab>
                    <v-tab>Operador | 4</v-tab>
                </v-tabs>
            </template>
        </v-app-bar>

        <div style="height: 10000px">
            
            <v-row class="mt-2">
                <v-col cols="12">
                    <v-card outlined>
                        <v-card-title class="py-2">

                        </v-card-title>
                    </v-card>
                </v-col>
            </v-row>
            
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>