<template>
    <v-menu offset-y :close-on-content-click="false">
        <template v-slot:activator="{on, attrs}">
        <th v-bind="attrs" v-on="on" class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">
            <div class="d-flex justify-space-between">
            <div>
                {{nome_coluna}}
            </div>
            <div @click.stop="ordenar(value_prop, ordenacao_sentido == 'cresc' ? 'desc' : 'cresc')">
                <v-icon size="19" class="mr-1" :color="ordenacao_sentido == 'cresc' && ordenacao_value == value_prop ? 'black' : ''">mdi-chevron-up</v-icon>
                <v-icon size="19" :color="ordenacao_sentido == 'desc' && ordenacao_value == value_prop ? 'black' : ''">mdi-chevron-down</v-icon>
            </div>
            </div>
        </th>
        </template>
        <v-sheet max-height="500" rounded class="px-1 py-2 pb-0 overflow-auto">
        <v-text-field v-model="search" placeholder="Pesquise por " dense hide-details outlined append-icon="mdi-close" @click:append="search = ''"></v-text-field>
        <v-checkbox @change="toggleTodos" v-model="selecionar_todos" dense hide-details label="Selecionar todos"></v-checkbox>
        <v-list dense>
            <v-virtual-scroll :items="computed_items" :item-height="50" height="400">
            <template v-slot:default="{ item }">
                <v-list-item @click="addFilter(item)">
                <v-list-item-content>
                    <v-list-item-title>{{ item == '' || item == null ? '(vazio)' : item}}</v-list-item-title>
                </v-list-item-content>
                <v-list-item-action class="d-flex justify-center">
                    <input @click.prevent="addFilter(item)" type="checkbox" name="" id="" :checked="isChecked(item)">
                    <!-- <v-checkbox @click.prevent dense hide-details  :value="nomes_selected.includes(item.name)">
                    </v-checkbox> -->
                </v-list-item-action>
                </v-list-item>
            </template>
            </v-virtual-scroll>
        </v-list>
        </v-sheet>
    </v-menu>
</template>

<script>
export default {
    props: ['ordenacao_value', 'ordenacao_sentido', 'nome_coluna', 'value_selected', 'value_prop', 'items', 'value_array_selected'],
    data(){
        return{
            search: '',
            selecionar_todos: true
        }
    },
    methods: {
        isChecked(item){
            return this.value_array_selected.includes(item)
        },
        ordenar(value, sentido){
            this.$emit('ordenar', value, sentido)
        },
        addFilter(item){
            this.$emit('addFilter', item, this.value_selected, this.value_prop)
        },
        toggleTodos(){
            if(!this.selecionar_todos){
                this.$emit('toggleTodos',this.selecionar_todos, this.value_selected, [])
            }else{
                this.$emit('toggleTodos',this.selecionar_todos, this.value_selected, this.value_prop)
            }
        },
        validItem(item){
            return (item[this.value_prop] != null && item[this.value_prop] != '')
        }
    },
    computed: {
        computed_items(){
            const items = [...new Set(this.items.map(item => item[this.value_prop])
                .filter(item => {
                    return this.search == '' ? true : item.toLowerCase().includes(this.search.toLowerCase())
                }))]
                return items
        },
    }
}
</script>

<style>

</style>