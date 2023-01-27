<template>
    <v-navigation-drawer dark color="blue-grey darken-3" mini-variant expand-on-hover app permanent >
        <v-list-item>
            <v-list-item-content>
                <v-list-item-title class="text-h6">
                    Moavi
                </v-list-item-title>
                <v-list-item-subtitle>
                    DPSP
                </v-list-item-subtitle>
            </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list dense nav>
            <v-list-item :to="{name: item.to}" v-for="item in items" :key="item.title" link>
                <v-list-item-icon>
                    <v-icon>{{ item.icon }}</v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
    data(){
        return{
            items: [{
                        title: 'Colaboradores',
                        icon: 'mdi-account-group',
                        to: 'home'
                    },
                    // {
                    //     title: 'Photos',
                    //     icon: 'mdi-image'
                    // },
                    {
                        title: 'Cargos',
                        icon: 'mdi-briefcase',
                        to: 'about'
                    },
                ],
                right: null,
        }
    }
}
</script>

<style>

</style>