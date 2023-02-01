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
            <v-menu offset-y :close-on-content-click="false">
              <template v-slot:activator="{on, attrs}">
                <th v-bind="attrs" v-on="on" class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
            top: 3px;">
                  <div class="d-flex justify-space-between">
                    <div>
                      Nome
                    </div>
                    <div @click.stop="ordenar('name', ordenacao_sentido == 'cresc' ? 'desc' : 'cresc')">
                      <v-icon size="19" class="mr-1" :color="ordenacao_sentido == 'cresc' && ordenacao_value == 'name' ? 'black' : ''">mdi-chevron-up</v-icon>
                      <v-icon size="19" :color="ordenacao_sentido == 'desc' && ordenacao_value == 'name' ? 'black' : ''">mdi-chevron-down</v-icon>
                    </div>
                  </div>
                </th>
              </template>
              <v-sheet max-height="500" rounded class="px-1 py-2 pb-0 overflow-auto">
                <v-text-field v-model="search_nome" placeholder="Pesquise por nome" dense hide-details outlined append-icon="mdi-close" @click:append="search_nome = ''"></v-text-field>
                <v-checkbox @change="toggleTodosNomes" v-model="selecionar_todos_nomes" dense hide-details label="Selecionar todos"></v-checkbox>
                <v-list dense>
                  <v-virtual-scroll :items="usuarios_por_nome" :item-height="50" height="400">
                    <template v-slot:default="{ item }">
                      <v-list-item @click="addFilterNome(item)">
                        <v-list-item-content>
                          <v-list-item-title>{{ item.name }}</v-list-item-title>
                        </v-list-item-content>
                        <v-list-item-action class="d-flex justify-center">
                          <input @click.prevent="addFilterNome(item)" type="checkbox" name="" id="" :checked="nomes_selected.includes(item.name)">
                          <!-- <v-checkbox @click.prevent dense hide-details  :value="nomes_selected.includes(item.name)">
                          </v-checkbox> -->
                        </v-list-item-action>
                      </v-list-item>
                    </template>
                  </v-virtual-scroll>
                </v-list>
              </v-sheet>
            </v-menu>
            
            <th class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Email</th>
            <th class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Cargo</th>
            <th class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Perfil</th>
            <th class="text-center white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Últ Acesso</th>
            <th class="text-center white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Qtd Acesso</th>
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
            <td class="text-left py-2 px-2">{{usu.perfil_nome}}</td>
            <td class="text-center py-2 px-2">{{usu.data_ult_acesso | format_date}}</td>
            <td class="text-center py-2 px-2">{{usu.qtd_acesso}}</td>
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
        <span class="text-body-2">344 resultados</span>
        <v-spacer></v-spacer>
        <v-pagination v-model="page" :length="6"></v-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import usuarios from '../api/usuarios'
  export default {
    name: 'HelloWorld',
    filters: {
      format_date(date){
        return moment(date).format('DD/MM/YY')
      }
    },
    computed:{
      usuarios_por_nome(){
        return this.usuarios.filter(usu => {
          return this.search_nome == '' ? true : usu.name.toLowerCase().includes(this.search_nome.toLowerCase())
        })
      },
      usuarios_computed_filter(){
        return this.usuarios.filter(usu => {
          return this.nomes_selected.includes(usu.name)
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
      toggleTodosNomes(){
        if(!this.selecionar_todos_nomes){
          this.nomes_selected = []
        }else{
          this.nomes_selected = this.usuarios.map(usu => usu.name)
        }
      },
      addFilterNome(usu){
        const index_find = this.nomes_selected.findIndex(item => {
          return  item == usu.name
        });
        if(index_find != -1){
          this.nomes_selected.splice(index_find, 1)
        }else{
          this.nomes_selected.push(usu.name)
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
      // filtro por nome
      nomes_selected: usuarios.map(usu => usu.name),
      selecionar_todos_nomes: true,
      search_nome: '',

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
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      /* box-shadow: inset 0 0 6px rgba(133, 32, 32, 0.3); */
    }
    ::-webkit-scrollbar-thumb {
      background-color: darkgrey;
      border-radius: 10px;
    }
    .content-home{
      padding-top: 101px;
      overflow: auto;
    }
    .tabela-app{
      height: calc(100vh - 50px);
    }
    table tr:nth-child(even){
      background: rgb(249, 249, 249);
    }
    .shadow-header{
      box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 12px;
    }
    
</style>
