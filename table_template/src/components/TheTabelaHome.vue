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
      <div style="height: 40px;" class="d-flex align-center px-2">
        <v-chip class="mr-1"  small>
          Nome <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Email <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Cargo <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Perfil <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Últ acesso <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Qtd acesso <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class="mr-1"  small>
          Liberado <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
        <v-chip class=""  small>
          Lojas <v-icon right>mdi-chevron-down</v-icon>
        </v-chip>
      </div>
    </div>
    <div class="content-home px-0" @scroll="teste($event)" :class="tabs == 'tabela' ? 'tabela-app' : ''">
      <table v-if="tabs == 'tabela'" style="width: 100%;">
        <thead :class="shadow ? 'shadow-header' : ''" style=";position: sticky;
    top: 3px;">
          <tr style=";position: sticky;
    top: 3px;">
            <th class="text-left white py-2 px-2" style="color: #474747; font-size: 16px;position: sticky;
    top: 3px;">Nome</th>
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
          <tr class="text-body-2" v-for="usu in usuarios.slice(0,100)" :key="usu.id">
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 200px;width: 200px">{{usu.name}}</td>
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 200px;width: 200px">{{usu.email}}</td>
            <td class="text-left py-2 px-2 text-truncate" style="max-width: 150px;width: 150px">{{usu.cargo}}</td>
            <td class="text-left py-2 px-2">{{usu.perfil_nome}}</td>
            <td class="text-center py-2 px-2">{{usu.data_ult_acesso | format_date}}</td>
            <td class="text-center py-2 px-2">{{usu.qtd_acesso}}</td>
            <td class="text-center py-2 px-2">{{usu.status_acesso}}</td>
            <td class="text-center py-2 px-2">{{usu.num_permissao}}</td>
          </tr>
        </tbody>
      </table>
      <v-col cols="12" v-if="tabs == 'importar'">oaidsjasiojoiasjiaoisd</v-col>
    </div>
    <div v-if="tabs == 'tabela'" class="py-2 white d-flex w-100 " style="position: fixed;width: calc(100vw - 56px - 6px);">
      <div class="d-flex px-2" style="width: calc(100vw - 56px - 6px);">
        <v-spacer></v-spacer>
        <v-pagination v-model="page" :length="6"></v-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
  export default {
    name: 'HelloWorld',
    filters: {
      format_date(date){
        return moment(date).format('DD/MM/YYYY')
      }
    },
    methods: {
      teste(e){
        if(e.target.scrollTop > 50){
          this.shadow = true
        }else{
          this.shadow = false
        }
      }
    },
    data: () => ({
      shadow: false,
      page: 1,
      tabs: 'tabela',
      usuarios: [
  {
    "id": 2,
    "data_ult_acesso": "2022-12-20 12:34:41",
    "cargo": "Loja",
    "name": "DSP PAULO FACCINI PARQUE",
    "email": "pfaccinipq@dpsp.com.br",
    "qtd_acesso": 511,
    "status_acesso": 1,
    "cpf": "61412110029218",
    "user_id": 2,
    "num_permissao": 1,
    "perfil_nome": "GERENTE"
  },
  {
    "id": 4,
    "data_ult_acesso": "2022-12-20 19:13:14",
    "cargo": "Loja",
    "name": "DP INGA 2",
    "email": "inga2@dpsp.com.br",
    "qtd_acesso": 344,
    "status_acesso": 1,
    "cpf": "33438250002453",
    "user_id": 4,
    "num_permissao": 1,
    "perfil_nome": "GERENTE"
  },
  {
    "id": 5,
    "data_ult_acesso": "2022-12-12 22:17:17",
    "cargo": "Loja",
    "name": "DP BARREIRO 1",
    "email": "barreiro1@dpsp.com.br",
    "qtd_acesso": 176,
    "status_acesso": 1,
    "cpf": "33438250026",
    "user_id": 5,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 7,
    "data_ult_acesso": "2021-07-01 19:34:00",
    "cargo": "GR",
    "name": "VERONICA SERRETTI MENDES GOMES",
    "email": "veronica.gomes@dpsp.com.br",
    "qtd_acesso": 11,
    "status_acesso": 1,
    "cpf": "08129009609",
    "user_id": null,
    "num_permissao": 0,
    "perfil_nome": ""
  },
  {
    "id": 8,
    "data_ult_acesso": "2022-12-21 09:01:42",
    "cargo": "Loja",
    "name": "DSP TIMOTEO PENTEADO",
    "email": "tpenteado@dpsp.com.br",
    "qtd_acesso": 377,
    "status_acesso": 1,
    "cpf": "61412110023104",
    "user_id": 8,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 9,
    "data_ult_acesso": "2022-12-21 16:07:35",
    "cargo": "Loja",
    "name": "DSP BAIRRO DOS PIMENTAS",
    "email": "bpimentas@dpsp.com.br",
    "qtd_acesso": 560,
    "status_acesso": 1,
    "cpf": "36130896883",
    "user_id": 9,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 10,
    "data_ult_acesso": "2022-12-19 17:17:08",
    "cargo": "Loja",
    "name": "DP ELDORADO 2",
    "email": "eldorado2@dpsp.com.br",
    "qtd_acesso": 123,
    "status_acesso": 1,
    "cpf": "33438250046",
    "user_id": 10,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 11,
    "data_ult_acesso": "2022-06-29 14:07:36",
    "cargo": "Analista operações",
    "name": "ANDRÉ DE LUCA TANESE",
    "email": "andre.tanese@dpsp.com.br",
    "qtd_acesso": 42,
    "status_acesso": 0,
    "cpf": "40919592880",
    "user_id": 11,
    "num_permissao": 1165,
    "perfil_nome": ""
  },
  {
    "id": 12,
    "data_ult_acesso": "2021-11-10 15:16:27",
    "cargo": "Coordenador operações",
    "name": "FREDERICO FASSINA",
    "email": "frederico.fassina@dpsp.com.br",
    "qtd_acesso": 30,
    "status_acesso": 0,
    "cpf": "40382048806",
    "user_id": 12,
    "num_permissao": 14,
    "perfil_nome": ""
  },
  {
    "id": 13,
    "data_ult_acesso": "2022-11-29 13:13:23",
    "cargo": "Loja",
    "name": "DP RAJA GABAGLIA",
    "email": "rajagabaglia@dpsp.com.br",
    "qtd_acesso": 67,
    "status_acesso": 1,
    "cpf": "33438250056",
    "user_id": 13,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 14,
    "data_ult_acesso": "2021-08-25 15:41:32",
    "cargo": "Analista de Projetos",
    "name": "MURILLO ALBERTO SOARES",
    "email": "murillo.soares@dpsp.com.br",
    "qtd_acesso": 12,
    "status_acesso": 0,
    "cpf": "29360825875",
    "user_id": 14,
    "num_permissao": 14,
    "perfil_nome": ""
  },
  {
    "id": 50,
    "data_ult_acesso": "2022-12-18 12:23:36",
    "cargo": "Loja",
    "name": "DP SANTA ROSA",
    "email": "santarosa@dpsp.com.br",
    "qtd_acesso": 442,
    "status_acesso": 1,
    "cpf": "03224249765",
    "user_id": 50,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 51,
    "data_ult_acesso": "2022-12-20 07:39:09",
    "cargo": "Loja",
    "name": "DP ICARAI 11",
    "email": "icarai11@dpsp.com.br",
    "qtd_acesso": 299,
    "status_acesso": 1,
    "cpf": "12686806772",
    "user_id": 51,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 53,
    "data_ult_acesso": "2022-12-20 21:58:18",
    "cargo": "Loja",
    "name": "DP AUGUSTO DE LIMA 2",
    "email": "augustodelima2@dpsp.com.br",
    "qtd_acesso": 70,
    "status_acesso": 1,
    "cpf": "33438250027600",
    "user_id": 53,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 54,
    "data_ult_acesso": "2022-11-30 18:32:04",
    "cargo": "Loja",
    "name": "DP BALENA 1",
    "email": "balena1@dpsp.com.br",
    "qtd_acesso": 35,
    "status_acesso": 1,
    "cpf": "33438250027367",
    "user_id": 54,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 55,
    "data_ult_acesso": "2022-12-05 09:26:33",
    "cargo": "Loja",
    "name": "DP BALENA 2",
    "email": "balena2@dpsp.com.br",
    "qtd_acesso": 22,
    "status_acesso": 1,
    "cpf": "33438250028096",
    "user_id": 55,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 56,
    "data_ult_acesso": "2022-10-24 12:31:40",
    "cargo": "Loja",
    "name": "DP BALENA 3",
    "email": "balena3@dpsp.com.br",
    "qtd_acesso": 20,
    "status_acesso": 1,
    "cpf": "33438250030589",
    "user_id": 56,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 57,
    "data_ult_acesso": "2022-12-02 11:14:09",
    "cargo": "Loja",
    "name": "DP SAO PAULO",
    "email": "saopaulomg@dpsp.com.br",
    "qtd_acesso": 40,
    "status_acesso": 1,
    "cpf": "33438250029491",
    "user_id": 57,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 59,
    "data_ult_acesso": "2022-12-21 14:00:33",
    "cargo": "Loja",
    "name": "DSP JARDIM PRESIDENTE DUTRA",
    "email": "jp.dutra@dpsp.com.br",
    "qtd_acesso": 119,
    "status_acesso": 1,
    "cpf": "61412110085711",
    "user_id": 59,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 71,
    "data_ult_acesso": "2022-08-09 16:40:38",
    "cargo": "Analista de projetos de operações sênior",
    "name": "BRUNA CORREA DE ABREU TAKAHARA",
    "email": "bruna.takahara@dpsp.com.br",
    "qtd_acesso": 55,
    "status_acesso": 0,
    "cpf": "39023470826",
    "user_id": 71,
    "num_permissao": 1165,
    "perfil_nome": ""
  },
  {
    "id": 72,
    "data_ult_acesso": "2022-12-15 10:49:51",
    "cargo": "Loja",
    "name": "DP ICARAI 2",
    "email": "icarai2@dpsp.com.br",
    "qtd_acesso": 79,
    "status_acesso": 1,
    "cpf": "33438250013900",
    "user_id": 72,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 73,
    "data_ult_acesso": "2022-12-20 17:16:09",
    "cargo": "Loja",
    "name": "DP ICARAI 3",
    "email": "icarai3@dpsp.com.br",
    "qtd_acesso": 92,
    "status_acesso": 1,
    "cpf": "33438250001724",
    "user_id": 73,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 74,
    "data_ult_acesso": "2022-12-17 08:42:23",
    "cargo": "Loja",
    "name": "DP PARANA",
    "email": "paranamg@dpsp.com.br",
    "qtd_acesso": 49,
    "status_acesso": 1,
    "cpf": "33438250027014",
    "user_id": 74,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 75,
    "data_ult_acesso": "2022-12-14 08:48:48",
    "cargo": "Loja",
    "name": "DP RIO DE JANEIRO 2",
    "email": "riodejaneiro2@dpsp.com.br",
    "qtd_acesso": 46,
    "status_acesso": 1,
    "cpf": "33438250028681",
    "user_id": 75,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 77,
    "data_ult_acesso": "2022-12-19 07:18:39",
    "cargo": "Loja",
    "name": "DP SANTA INES",
    "email": "santaines@dpsp.com.br",
    "qtd_acesso": 73,
    "status_acesso": 1,
    "cpf": "33438250053449",
    "user_id": 77,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 78,
    "data_ult_acesso": "2022-12-17 17:08:08",
    "cargo": "Loja",
    "name": "DSP VILA MARIANA II",
    "email": "vmariana2@dpsp.com.br",
    "qtd_acesso": 153,
    "status_acesso": 1,
    "cpf": "61412110090120",
    "user_id": 78,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 79,
    "data_ult_acesso": "2022-12-17 13:32:21",
    "cargo": "Loja",
    "name": "DP SANTO ANTONIO",
    "email": "santoantonio@dpsp.com.br",
    "qtd_acesso": 135,
    "status_acesso": 1,
    "cpf": "33438250048607",
    "user_id": 79,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 80,
    "data_ult_acesso": "2022-12-20 23:32:10",
    "cargo": "Loja",
    "name": "DP ICARAI 4",
    "email": "icarai4@dpsp.com.br",
    "qtd_acesso": 155,
    "status_acesso": 1,
    "cpf": "33438250024341",
    "user_id": 80,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 81,
    "data_ult_acesso": "2022-12-05 09:22:29",
    "cargo": "Loja",
    "name": "DP ICARAI 5",
    "email": "icarai5@dpsp.com.br",
    "qtd_acesso": 112,
    "status_acesso": 1,
    "cpf": "33438250024260",
    "user_id": 81,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 83,
    "data_ult_acesso": "2022-12-04 09:52:24",
    "cargo": "Loja",
    "name": "DP SERRA BH",
    "email": "serrabh@dpsp.com.br",
    "qtd_acesso": 41,
    "status_acesso": 1,
    "cpf": "33438250042676",
    "user_id": 83,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 84,
    "data_ult_acesso": "2022-12-15 10:27:48",
    "cargo": "Loja",
    "name": "DP ICARAI 8",
    "email": "icarai8@dpsp.com.br",
    "qtd_acesso": 144,
    "status_acesso": 1,
    "cpf": "33438250024007",
    "user_id": 84,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 85,
    "data_ult_acesso": "2022-12-20 14:28:15",
    "cargo": "Loja",
    "name": "DP TIMOTEO",
    "email": "timoteo@dpsp.com.br",
    "qtd_acesso": 273,
    "status_acesso": 1,
    "cpf": "33438250042595",
    "user_id": 85,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 87,
    "data_ult_acesso": "2022-12-21 11:37:14",
    "cargo": "Loja",
    "name": "DP INGA",
    "email": "inga@dpsp.com.br",
    "qtd_acesso": 140,
    "status_acesso": 1,
    "cpf": "33438250024775",
    "user_id": 87,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 88,
    "data_ult_acesso": "2022-12-16 07:05:56",
    "cargo": "Loja",
    "name": "DP TUPIS",
    "email": "tupis@dpsp.com.br",
    "qtd_acesso": 59,
    "status_acesso": 1,
    "cpf": "33438250026719",
    "user_id": 88,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 90,
    "data_ult_acesso": "2022-12-03 08:43:42",
    "cargo": "Loja",
    "name": "DP ALIPIO DE MELO",
    "email": "alipiodemelo@dpsp.com.br",
    "qtd_acesso": 31,
    "status_acesso": 1,
    "cpf": "33438250028258",
    "user_id": 90,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 91,
    "data_ult_acesso": "2022-12-21 10:49:05",
    "cargo": "Loja",
    "name": "DSP BAIRRO DOS PIMENTAS II",
    "email": "bpimentas2@dpsp.com.br",
    "qtd_acesso": 263,
    "status_acesso": 1,
    "cpf": "61412110004495",
    "user_id": 91,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 93,
    "data_ult_acesso": "2022-12-20 16:09:38",
    "cargo": "Loja",
    "name": "DSP BOM CLIMACO",
    "email": "bomclimaco@dpsp.com.br",
    "qtd_acesso": 79,
    "status_acesso": 1,
    "cpf": "61412110066920",
    "user_id": 93,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 94,
    "data_ult_acesso": "2022-12-21 14:03:49",
    "cargo": "Loja",
    "name": "DP NITEROI 11",
    "email": "niteroi11@dpsp.com.br",
    "qtd_acesso": 131,
    "status_acesso": 1,
    "cpf": "33438250023108",
    "user_id": 94,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 95,
    "data_ult_acesso": "2022-12-21 13:44:19",
    "cargo": "Loja",
    "name": "DSP CACHOEIRA",
    "email": "cachoeira@dpsp.com.br",
    "qtd_acesso": 939,
    "status_acesso": 1,
    "cpf": "61412110053518",
    "user_id": 95,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 96,
    "data_ult_acesso": "2022-12-09 15:24:44",
    "cargo": "Loja",
    "name": "DP NITEROI 15",
    "email": "niteroi15@dpsp.com.br",
    "qtd_acesso": 45,
    "status_acesso": 1,
    "cpf": "33438250032441",
    "user_id": 96,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 97,
    "data_ult_acesso": "2022-12-21 10:55:38",
    "cargo": "Loja",
    "name": "DSP CUMBICA",
    "email": "cumbica@dpsp.com.br",
    "qtd_acesso": 327,
    "status_acesso": 1,
    "cpf": "61412110011866",
    "user_id": 97,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 98,
    "data_ult_acesso": "2022-12-16 12:56:05",
    "cargo": "Loja",
    "name": "DP NITEROI 4",
    "email": "niteroi4@dpsp.com.br",
    "qtd_acesso": 99,
    "status_acesso": 1,
    "cpf": "33438250010715",
    "user_id": 98,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 99,
    "data_ult_acesso": "2022-12-21 02:18:49",
    "cargo": "Loja",
    "name": "DSP DOM PEDRO",
    "email": "dompedro@dpsp.com.br",
    "qtd_acesso": 307,
    "status_acesso": 1,
    "cpf": "61412110006358",
    "user_id": 99,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 100,
    "data_ult_acesso": "2022-12-19 17:57:27",
    "cargo": "Loja",
    "name": "DP NITEROI 5",
    "email": "niteroi5@dpsp.com.br",
    "qtd_acesso": 47,
    "status_acesso": 1,
    "cpf": "33438250009032",
    "user_id": 100,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 101,
    "data_ult_acesso": "2022-12-19 19:28:42",
    "cargo": "Loja",
    "name": "DSP GUARULHOS",
    "email": "guarulhos@dpsp.com.br",
    "qtd_acesso": 102,
    "status_acesso": 1,
    "cpf": "61412110003685",
    "user_id": 101,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 102,
    "data_ult_acesso": "2022-12-21 15:10:39",
    "cargo": "Loja",
    "name": "DP NITEROI 9",
    "email": "niteroi9@dpsp.com.br",
    "qtd_acesso": 229,
    "status_acesso": 1,
    "cpf": "33438250023027",
    "user_id": 102,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 104,
    "data_ult_acesso": "2022-12-20 08:56:03",
    "cargo": "Loja",
    "name": "DP BETANIA",
    "email": "betania@dpsp.com.br",
    "qtd_acesso": 47,
    "status_acesso": 1,
    "cpf": "33438250042",
    "user_id": 104,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 105,
    "data_ult_acesso": "2022-12-21 13:09:50",
    "cargo": "Loja",
    "name": "DSP GUARULHOS II",
    "email": "guarulhos2@dpsp.com.br",
    "qtd_acesso": 347,
    "status_acesso": 1,
    "cpf": "61412110037660",
    "user_id": 105,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 106,
    "data_ult_acesso": "2022-12-21 16:46:52",
    "cargo": "Loja",
    "name": "DSP JARDIM PARAISO",
    "email": "jardimparaiso@dpsp.com.br",
    "qtd_acesso": 242,
    "status_acesso": 1,
    "cpf": "61412110064200",
    "user_id": 106,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 108,
    "data_ult_acesso": "2022-12-15 15:08:36",
    "cargo": "Loja",
    "name": "DP BETIM 1",
    "email": "betim1@dpsp.com.br",
    "qtd_acesso": 45,
    "status_acesso": 1,
    "cpf": "33438250030",
    "user_id": 108,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 109,
    "data_ult_acesso": "2022-12-17 14:13:57",
    "cargo": "Loja",
    "name": "DP SHOPPING PLAZA NITEROI",
    "email": "plaza.niteroi@dpsp.com.br",
    "qtd_acesso": 39,
    "status_acesso": 1,
    "cpf": "33438250058750",
    "user_id": 109,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 113,
    "data_ult_acesso": "2022-12-21 12:03:07",
    "cargo": "Loja",
    "name": "DSP BARCAS",
    "email": "barcas@dpsp.com.br",
    "qtd_acesso": 214,
    "status_acesso": 1,
    "cpf": "61412110023600",
    "user_id": 113,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 115,
    "data_ult_acesso": "2022-12-20 18:06:39",
    "cargo": "Loja",
    "name": "DSP JARDIM SAO JOAO",
    "email": "jardimsaojoao@dpsp.com.br",
    "qtd_acesso": 123,
    "status_acesso": 1,
    "cpf": "61412110062932",
    "user_id": 115,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 116,
    "data_ult_acesso": "2022-12-15 10:26:53",
    "cargo": "Loja",
    "name": "DSP NITEROI",
    "email": "niteroi@dpsp.com.br",
    "qtd_acesso": 36,
    "status_acesso": 1,
    "cpf": "61412110023872",
    "user_id": 116,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 121,
    "data_ult_acesso": "2022-12-21 12:37:34",
    "cargo": "Loja",
    "name": "DSP ALDEIA DA SERRA",
    "email": "aserra@dpsp.com.br",
    "qtd_acesso": 166,
    "status_acesso": 1,
    "cpf": "61412110056290",
    "user_id": 121,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 122,
    "data_ult_acesso": "2022-12-21 16:35:28",
    "cargo": "Loja",
    "name": "DSP JARDIM TRANQUILIDADE",
    "email": "jtranquilidade@dpsp.com.br",
    "qtd_acesso": 324,
    "status_acesso": 1,
    "cpf": "61412110018526",
    "user_id": 122,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 123,
    "data_ult_acesso": "2022-12-21 15:00:59",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE",
    "email": "alphaville@dpsp.com.br",
    "qtd_acesso": 576,
    "status_acesso": 1,
    "cpf": "61412110018011",
    "user_id": 123,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 126,
    "data_ult_acesso": "2022-12-21 16:38:27",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE CENTRO DE APOIO",
    "email": "alphavillecentro@dpsp.com.br",
    "qtd_acesso": 226,
    "status_acesso": 1,
    "cpf": "61412110100966",
    "user_id": 126,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 127,
    "data_ult_acesso": "2022-12-21 07:56:13",
    "cargo": "Loja",
    "name": "DSP PAULO FACCINI II",
    "email": "pfaccini2@dpsp.com.br",
    "qtd_acesso": 181,
    "status_acesso": 1,
    "cpf": "61412110056371",
    "user_id": 127,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 128,
    "data_ult_acesso": "2022-12-20 13:59:01",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE II",
    "email": "alphaville2@dpsp.com.br",
    "qtd_acesso": 173,
    "status_acesso": 1,
    "cpf": "61412110074604",
    "user_id": 128,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 130,
    "data_ult_acesso": "2022-12-21 13:34:47",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE III",
    "email": "alphaville3@dpsp.com.br",
    "qtd_acesso": 101,
    "status_acesso": 1,
    "cpf": "61412110079827",
    "user_id": 130,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 132,
    "data_ult_acesso": "2022-12-19 15:17:22",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE IV",
    "email": "alphaville4@dpsp.com.br",
    "qtd_acesso": 67,
    "status_acesso": 1,
    "cpf": "61412110081058",
    "user_id": 132,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 134,
    "data_ult_acesso": "2022-12-18 19:28:32",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE V",
    "email": "alphaville5@dpsp.com.br",
    "qtd_acesso": 205,
    "status_acesso": 1,
    "cpf": "61412110085479",
    "user_id": 134,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 135,
    "data_ult_acesso": "2022-12-21 16:00:12",
    "cargo": "Loja",
    "name": "DSP PONTE GRANDE",
    "email": "pontegrande@dpsp.com.br",
    "qtd_acesso": 151,
    "status_acesso": 1,
    "cpf": "61412110071842",
    "user_id": 135,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 136,
    "data_ult_acesso": "2022-12-19 11:36:37",
    "cargo": "Loja",
    "name": "DSP ALPHAVILLE VI",
    "email": "alphaville6@dpsp.com.br",
    "qtd_acesso": 131,
    "status_acesso": 1,
    "cpf": "61412110094117",
    "user_id": 136,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 138,
    "data_ult_acesso": "2022-12-20 19:01:31",
    "cargo": "Loja",
    "name": "DSP SHOPPING INTERNACIONAL",
    "email": "shopinternacional@dpsp.com.br",
    "qtd_acesso": 138,
    "status_acesso": 1,
    "cpf": "61412110037580",
    "user_id": 138,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 139,
    "data_ult_acesso": "2022-12-21 07:21:41",
    "cargo": "Loja",
    "name": "DSP BARUERI",
    "email": "barueri@dpsp.com.br",
    "qtd_acesso": 334,
    "status_acesso": 1,
    "cpf": "61412110010380",
    "user_id": 139,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 140,
    "data_ult_acesso": "2022-12-15 17:45:58",
    "cargo": "Loja",
    "name": "DP BETIM 2",
    "email": "betim2@dpsp.com.br",
    "qtd_acesso": 63,
    "status_acesso": 1,
    "cpf": "33438250030",
    "user_id": 140,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 141,
    "data_ult_acesso": "2022-12-21 09:19:18",
    "cargo": "Loja",
    "name": "DSP SHOPPING MAIA",
    "email": "shopmaia@dpsp.com.br",
    "qtd_acesso": 159,
    "status_acesso": 1,
    "cpf": "61412110061103",
    "user_id": 141,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 142,
    "data_ult_acesso": "2022-12-03 22:34:37",
    "cargo": "Loja",
    "name": "DSP BARUERI II",
    "email": "barueri2@dpsp.com.br",
    "qtd_acesso": 83,
    "status_acesso": 1,
    "cpf": "61412110034807",
    "user_id": 142,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 144,
    "data_ult_acesso": "2022-12-19 15:15:40",
    "cargo": "Loja",
    "name": "DSP BARUERI III",
    "email": "barueri3@dpsp.com.br",
    "qtd_acesso": 144,
    "status_acesso": 1,
    "cpf": "61412110051736",
    "user_id": 144,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 145,
    "data_ult_acesso": "2022-12-20 17:44:52",
    "cargo": "Loja",
    "name": "DSP CAIEIRAS",
    "email": "caieiras@dpsp.com.br",
    "qtd_acesso": 143,
    "status_acesso": 1,
    "cpf": "61412110041854",
    "user_id": 145,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 147,
    "data_ult_acesso": "2022-12-21 16:26:56",
    "cargo": "Loja",
    "name": "DP CARREFOUR",
    "email": "carrefour@dpsp.com.br",
    "qtd_acesso": 111,
    "status_acesso": 1,
    "cpf": "33438250030",
    "user_id": 147,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 148,
    "data_ult_acesso": "2022-12-20 09:12:23",
    "cargo": "Loja",
    "name": "DSP CAJAMAR",
    "email": "cajamar@dpsp.com.br",
    "qtd_acesso": 228,
    "status_acesso": 1,
    "cpf": "61412110055480",
    "user_id": 148,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 149,
    "data_ult_acesso": "2022-12-21 15:58:02",
    "cargo": "Loja",
    "name": "DSP VILA AUGUSTA",
    "email": "vilaaugusta@dpsp.com.br",
    "qtd_acesso": 662,
    "status_acesso": 1,
    "cpf": "61412110053275",
    "user_id": 149,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 151,
    "data_ult_acesso": "2022-12-15 21:18:32",
    "cargo": "Loja",
    "name": "DSP CARAPICUIBA",
    "email": "carapicuiba@dpsp.com.br",
    "qtd_acesso": 64,
    "status_acesso": 1,
    "cpf": "61412110005033",
    "user_id": 151,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 152,
    "data_ult_acesso": "2022-12-21 14:29:03",
    "cargo": "Loja",
    "name": "DSP VILA BARROS",
    "email": "vbarros@dpsp.com.br",
    "qtd_acesso": 571,
    "status_acesso": 1,
    "cpf": "61412110047119",
    "user_id": 152,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 153,
    "data_ult_acesso": "2022-12-06 21:13:40",
    "cargo": "Loja",
    "name": "DSP FRANCO DA ROCHA",
    "email": "francodarocha@dpsp.com.br",
    "qtd_acesso": 80,
    "status_acesso": 1,
    "cpf": "61412110070447",
    "user_id": 153,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 154,
    "data_ult_acesso": "2022-12-21 15:51:09",
    "cargo": "Loja",
    "name": "DP ELDORADO",
    "email": "eldorado@dpsp.com.br",
    "qtd_acesso": 43,
    "status_acesso": 1,
    "cpf": "33438250030",
    "user_id": 154,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 156,
    "data_ult_acesso": "2022-12-19 11:03:06",
    "cargo": "Loja",
    "name": "DSP JARDIM BARUERI",
    "email": "jardimbarueri@dpsp.com.br",
    "qtd_acesso": 98,
    "status_acesso": 1,
    "cpf": "61412110067225",
    "user_id": 156,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 157,
    "data_ult_acesso": "2022-12-19 22:26:14",
    "cargo": "Loja",
    "name": "DSP VILA GALVAO",
    "email": "vgalvao@dpsp.com.br",
    "qtd_acesso": 204,
    "status_acesso": 1,
    "cpf": "61412110012080",
    "user_id": 157,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 158,
    "data_ult_acesso": "2022-12-21 12:57:36",
    "cargo": "Loja",
    "name": "DSP SANTANA DE PARNAIBA",
    "email": "sparnaiba@dpsp.com.br",
    "qtd_acesso": 163,
    "status_acesso": 1,
    "cpf": "61412110057505",
    "user_id": 158,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 159,
    "data_ult_acesso": "2022-12-21 14:07:42",
    "cargo": "Loja",
    "name": "DSP VILA PROGRESSO",
    "email": "vprogresso@dpsp.com.br",
    "qtd_acesso": 159,
    "status_acesso": 1,
    "cpf": "61412110062266",
    "user_id": 159,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 160,
    "data_ult_acesso": "2022-12-11 13:56:32",
    "cargo": "Loja",
    "name": "DSP SHOPPING BARUERI",
    "email": "shopbarueri@dpsp.com.br",
    "qtd_acesso": 124,
    "status_acesso": 1,
    "cpf": "61412110033401",
    "user_id": 160,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 161,
    "data_ult_acesso": "2022-11-29 15:32:03",
    "cargo": "Loja",
    "name": "DP GALERIA NITEROI",
    "email": "galerianiteroi@dpsp.com.br",
    "qtd_acesso": 20,
    "status_acesso": 1,
    "cpf": "33438250061972",
    "user_id": 161,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 162,
    "data_ult_acesso": "2022-12-20 16:58:44",
    "cargo": "Loja",
    "name": "DSP SHOPPING TAMBORE",
    "email": "shoptambore@dpsp.com.br",
    "qtd_acesso": 141,
    "status_acesso": 1,
    "cpf": "61412110028831",
    "user_id": 162,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 163,
    "data_ult_acesso": "2022-11-30 19:11:17",
    "cargo": "Loja",
    "name": "DSP TAMBORE",
    "email": "tambore@dpsp.com.br",
    "qtd_acesso": 81,
    "status_acesso": 1,
    "cpf": "61412110090715",
    "user_id": 163,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 164,
    "data_ult_acesso": "2022-12-17 15:55:53",
    "cargo": "Loja",
    "name": "DP ICARAI 1",
    "email": "icarai1@dpsp.com.br",
    "qtd_acesso": 90,
    "status_acesso": 1,
    "cpf": "33438250004901",
    "user_id": 164,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 165,
    "data_ult_acesso": "2022-12-20 09:54:46",
    "cargo": "Loja",
    "name": "DP GOV VALADARES",
    "email": "governadorvaladares@dpsp.com.br",
    "qtd_acesso": 222,
    "status_acesso": 1,
    "cpf": "33438250028",
    "user_id": 165,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 167,
    "data_ult_acesso": "2022-12-21 16:05:45",
    "cargo": "Loja",
    "name": "DP GOV VALADARES 2",
    "email": "governadorvaladares2@dpsp.com.br",
    "qtd_acesso": 80,
    "status_acesso": 1,
    "cpf": "33438250016",
    "user_id": 167,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 168,
    "data_ult_acesso": "2022-12-21 13:50:31",
    "cargo": "Loja",
    "name": "DP ICARAI 12",
    "email": "icarai12@dpsp.com.br",
    "qtd_acesso": 90,
    "status_acesso": 1,
    "cpf": "33438250052",
    "user_id": 168,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 169,
    "data_ult_acesso": "2022-12-20 20:07:51",
    "cargo": "Loja",
    "name": "DSP ACLIMACAO",
    "email": "aclimacao@dpsp.com.br",
    "qtd_acesso": 292,
    "status_acesso": 1,
    "cpf": "61412110014610",
    "user_id": 169,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 170,
    "data_ult_acesso": "2022-12-18 19:18:08",
    "cargo": "Loja",
    "name": "DSP ACLIMACAO II",
    "email": "aclimacao2@dpsp.com.br",
    "qtd_acesso": 173,
    "status_acesso": 1,
    "cpf": "61412110091282",
    "user_id": 170,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 171,
    "data_ult_acesso": "2022-11-30 15:50:19",
    "cargo": "Loja",
    "name": "DP GOV VALADARES 4",
    "email": "governadorvaladares4@dpsp.com.br",
    "qtd_acesso": 62,
    "status_acesso": 1,
    "cpf": "334.382.500-48",
    "user_id": 171,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 172,
    "data_ult_acesso": "2022-12-21 12:19:53",
    "cargo": "Loja",
    "name": "DP MANHUACU",
    "email": "manhuacu@dpsp.com.br",
    "qtd_acesso": 199,
    "status_acesso": 1,
    "cpf": "33438250037",
    "user_id": 172,
    "num_permissao": 1,
    "perfil_nome": ""
  },
  {
    "id": 173,
    "data_ult_acesso": "2022-12-21 14:27:45",
    "cargo": "Loja",
    "name": "DP GUTIERREZ 1",
    "email": "gutierrez1@dpsp.com.br",
    "qtd_acesso": 144,
    "status_acesso": 1,
    "cpf": "33438250028",
    "user_id": 173,
    "num_permissao": 1,
    "perfil_nome": ""
  },
]
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
      padding-top: 135px;
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
