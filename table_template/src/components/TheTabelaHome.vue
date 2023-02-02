<template>
  <div class="tabela-main">
    <div class="text-h5" style="
    position: fixed;background: white; padding: 10px 0;
    width: calc(100vw - 56px - 6px);
">
      <div class="px-2 d-flex align-center">
        Usuários
        <v-spacer></v-spacer>
        <v-btn text color="success" depressed small>
          <v-icon left>mdi-file-excel</v-icon> Excel
        </v-btn>
        <v-btn class="ml-1" text color="primary" depressed small>
          <v-icon left>mdi-file</v-icon> csv
        </v-btn>
        <v-btn color="" icon><v-icon>mdi-bell</v-icon></v-btn>
      </div> 
      <div class="px-0">
        <v-tabs v-model="tabs">
          <v-tab href="#tabela">
            Usuários
          </v-tab>
          <v-tab href="#importar">
            Importar Cluster
          </v-tab>
          <v-tab href="#extrato">
            Importar Usuários
          </v-tab>
          <v-tab href="#downloads">
            Emails não enviados
          </v-tab>
        </v-tabs>
      </div>
      
    </div>
    <div class="content-home px-0" @scroll="activeShadow($event)" :class="tabs == 'tabela' ? 'tabela-app' : ''">
      <table v-if="tabs == 'tabela'" style="width: 100%;">
        <thead :class="shadow ? 'shadow-header' : ''" style=";position: sticky;
    top: 3px;">
          <tr style=";position: sticky;
    top: 3px;">
            
            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Nome"
              :value_prop="'name'" :value_selected="'nomes_selected'" :items="usuarios" :value_array_selected="nomes_selected" />
            
            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Email"
              :value_prop="'email'" :value_selected="'email_selected'" :items="usuarios" :value_array_selected="email_selected" />
            
            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Cargos"
              :value_prop="'cargo'" :value_selected="'cargos_selected'" :items="usuarios" :value_array_selected="cargos_selected" />

            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Perfil"
              :value_prop="'perfil_nome'" :value_selected="'perfil_selected'" :items="usuarios" :value_array_selected="perfil_selected" />

            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Últ acesso"
            :value_prop="'data_ult_acesso'" :value_selected="'ult_acesso_selected'" :items="usuarios" :value_array_selected="ult_acesso_selected" />
            
            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Qtd Acesso"
            :value_prop="'qtd_acesso'" :value_selected="'qtd_acesso_selected'" :items="usuarios" :value_array_selected="qtd_acesso_selected" />

            <!-- <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Últ acesso"
            :value_prop="'data_ult_acesso'" :value_selected="'ult_acesso_selected'" :items="usuarios" :value_array_selected="ult_acesso_selected" />

            <TH @addFilter="addFilter" @ordenar="ordenar" @toggleTodos="toggleTodos" :ordenacao_sentido="ordenacao_sentido" :ordenacao_value="ordenacao_value" nome_coluna="Últ acesso"
            :value_prop="'data_ult_acesso'" :value_selected="'ult_acesso_selected'" :items="usuarios" :value_array_selected="ult_acesso_selected" />
             -->
            <th class="text-center white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Liberado/ bloq</th>
            <th class="text-center white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Lojas</th>
          </tr>
        </thead>
        <tbody>
          <tr class="text-body-2" v-for="usu in usuarios_computed_filter.slice(0,100)" :key="usu.id">
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 200px;width: 200px">{{usu.name}}</td>
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 200px;width: 200px">{{usu.email}}</td>
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 150px;width: 150px">{{usu.cargo}}</td>
            <td class="text-left py-2 px-2 text-truncate" style="min-width: 97px">{{usu.perfil_nome}}</td>
            <td class="text-center py-2 px-2" style="min-width: 137px">{{usu.data_ult_acesso | format_date}}</td>
            <td class="text-center py-2 px-2" style="min-width: 137px">{{usu.qtd_acesso}}</td>
            <td class="text-center py-2 px-2" @click.stop="usu.status_acesso = !usu.status_acesso">
              <input :checked="usu.status_acesso == 1" type="checkbox" name="" id="" :value="usu.status_acessso">
              <!-- <div class="d-flex justify-center" style="width: 100%">
                <v-checkbox dense hide-details class="mt-0" v-model="usu.status_acesso"></v-checkbox>
              </div> -->
            </td>
            <td class="text-center py-2 px-2">{{usu.num_permissao}}</td>
          </tr>
        </tbody>
      </table>
      <v-col cols="12" v-if="tabs == 'importar'">oaidsjasiojoiasjiaoisd</v-col>
    </div>
    <div v-if="tabs == 'tabela'" class="py-2 white d-flex w-100 " style="position: fixed;width: calc(100vw - 56px - 6px);">
      <div class="d-flex px-2 align-center" style="width: calc(100vw - 56px - 6px);">
        <span class="text-body-2">{{usuarios.length}} resultados</span>
        <v-spacer></v-spacer>
        <v-pagination v-model="page" :length="6"></v-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import TH from '../components/table/TH.vue'

import usuarios from '../api/usuarios'
  export default {
    components:{
      TH
    },
    name: 'HelloWorld',
    filters: {
      format_date(date){
        return moment(date).format('DD/MM/YY HH:mm')
      }
    },
    computed:{
      usuarios_computed_filter(){
        return this.usuarios.filter(usu => {
          return this.nomes_selected.includes(usu.name) &&
          this.email_selected.includes(usu.email) &&
          this.cargos_selected.includes(usu.cargo) &&
          this.perfil_selected.includes(usu.perfil_nome) &&
          this.ult_acesso_selected.includes(usu.data_ult_acesso) &&
          this.qtd_acesso_selected.includes(usu.qtd_acesso)
        }).sort((a, b) => {
          const a_format = a[this.ordenacao_value]
          const b_format = b[this.ordenacao_value]

          if (a_format > b_format) {
              return this.ordenacao_sentido == 'cresc' ? 1 : -1;
          }
          if (a_format < b_format) {
              return this.ordenacao_sentido == 'desc' ? 1 : -1;
          }
          return 0;
        })
      }
    },
    methods: {
      ordenar(value, sentido){
        this.ordenacao_value = value;
        this.ordenacao_sentido = sentido;
      },
      toggleTodos(selecionar_todos, value_selected, value_prop){
        if(!selecionar_todos){
          this[value_selected] = []
        }else{
          this[value_selected] = this.usuarios.map(item => item[value_prop])
        }
      },
      addFilter(item, value_selected, value_prop){
        const index_find = this[value_selected].findIndex(item_v => {
          return item_v == item
        });
        if(index_find != -1){
          this[value_selected].splice(index_find, 1)
        }else{
          this[value_selected].push(item)
        }
      },
      activeShadow(e){
        if(e.target.scrollTop > 50){
          this.shadow = true
        }else{
          this.shadow = false
        }
      }
    },
    data: () => ({
      // filtros
      email_selected: [...new Set(usuarios.map(usu => usu.email))],
      nomes_selected: [...new Set(usuarios.map(usu => usu.name))],
      cargos_selected: [...new Set(usuarios.map(usu => usu.cargo))],
      perfil_selected: [...new Set(usuarios.map(usu => usu.perfil_nome))],
      ult_acesso_selected: [...new Set(usuarios.map(usu => usu.data_ult_acesso))],
      qtd_acesso_selected: [...new Set(usuarios.map(usu => usu.qtd_acesso))],
      
      // Ordenacao
      ordenacao_value: '',
      ordenacao_sentido: 'cresc',
      
      shadow: false,
      // paginacao
      page: 1,
      // tab atual
      tabs: 'tabela',
      // DADOS
      usuarios: usuarios
    }),
  }
</script>
<style>
@import '../styles/table_home.css';
</style>
