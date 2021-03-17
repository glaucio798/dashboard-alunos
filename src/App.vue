<template>
  <v-app>
    <v-app-bar color="#ff6450" class="px-0 px-md-5" height="80px" app dark>
      <v-container class="px-0 px-md-16">
        <v-row justify="end">
          <v-card
            min-width="327"
            color="#ff7362"
            elevation="15"
            tile
            height="80px"
          >
            <v-row no-gutters style="height: 100%">
              <v-list-item class="px-0">
                <v-avatar class="mx-5">
                  <img
                    src="https://cdn.vuetifyjs.com/images/john.jpg"
                    alt="John"
                  />
                </v-avatar>
                <v-list-item-content>
                  <v-list-item-title>Glaucio Martins</v-list-item-title>
                  <v-list-item-subtitle
                    >Ultimo login: 09/03/2021</v-list-item-subtitle
                  >
                </v-list-item-content>
                <v-divider light vertical></v-divider>
                <v-icon class="mx-7">mdi-menu-down</v-icon>
              </v-list-item>
            </v-row>
          </v-card>
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <v-container class="px-16">
        <v-row class="mt-8">
          <v-col cols="12" md="5" sm="12">
            <v-text-field
              v-model="filtro"
              solo
              label="Busque por nomes ou emails"
              append-icon="mdi-magnify"
            ></v-text-field
          ></v-col>
          <v-spacer></v-spacer>
          <v-col cols="12" md="3" sm="12">
            <v-row align="center" no-gutters justify="end" class="flex-nowrap">
              <p class="text-h6">Filtros:</p>
              <v-select
                class="ml-6"
                :items="['Todos', 'Ativos', 'Inativos']"
                v-model="filtroEstado"
                solo
              ></v-select>
            </v-row>
          </v-col>
          <v-col cols="12" md="3" sm="12">
            <v-row no-gutters justify="end">
              <Modal @novoaluno="submit" />
            </v-row>
          </v-col>
        </v-row>
        <v-row v-if="alunos.length > 0" align="start">
          <v-col
            sm="12"
            md="6"
            lg="4"
            xl="3"
            v-for="aluno in alunos"
            :key="aluno.idade"
          >
            <cardUsuario
              class="my-5"
              :nome="aluno.nome"
              :email="aluno.email"
              :telefone="aluno.telefone"
              :ultimaAvaliacao="aluno.ultimaAvaliacao"
              :idade="parseInt(aluno.idade)"
              :inativo="aluno.inativo"
            />
          </v-col>
        </v-row>
        <v-row justify="center" v-else-if="dados.length > 0">
          <p class="text-h3">
            Não há usuários com os critérios de busca utilizado
          </p>
        </v-row>
        <v-row justify="center" v-else>
          <p class="text-h3">Não há usuários cadastrados</p>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import cardUsuario from "./components/cardUsuario";
import Modal from "./components/modal.vue";

export default {
  name: "App",

  components: {
    cardUsuario,
    Modal,
  },

  data() {
    return {
      dados: [],
      filtro: "",
      filtroEstado: "Todos",
    };
  },
  methods: {
    submit(arg) {
      this.dados.push({
        nome: arg.nome,
        idade: arg.idade,
        telefone: arg.telefone,
        email: arg.email,
        ultimaAvaliacao: "15/03/2019",
        inativo: !arg.ativo,
      });
    },
    estado(valor) {
      console.log(this.filtroEstado);
      if (this.filtroEstado == "Todos") return true;

      if (this.filtroEstado == "Ativos") return !valor.inativo;

      return valor.inativo;
    },
  },
  computed: {
    alunos() {
      return this.dados.filter((valor) => {
        return (
          (valor.nome.includes(this.filtro) ||
            valor.email.includes(this.filtro)) &&
          this.estado(valor)
        );
      });
    },
  },
  mounted() {
    // for (let index = 0; index < 10; index++) {
    //   this.dados.push({
    //     nome: "aluno " + index,
    //     email: "aluno " + index + "@gmail.com",
    //     telefone:
    //       "(" +
    //       index +
    //       index +
    //       ") " +
    //       index +
    //       index +
    //       index +
    //       index +
    //       index +
    //       " " +
    //       index +
    //       index +
    //       index +
    //       index,
    //     ultimaAvaliacao: index + "/03/2019",
    //     idade: parseInt(String(index) + index),
    //     inativo: false,
    //   });
    // }
    // for (let index = 10; index < 15; index++) {
    //   this.dados.push({
    //     nome: "aluno " + index,
    //     email: "aluno " + index + "@gmail.com",
    //     telefone:
    //       "(" +
    //       index +
    //       index +
    //       ") " +
    //       index +
    //       index +
    //       index +
    //       index +
    //       index +
    //       " " +
    //       index +
    //       index +
    //       index +
    //       index,
    //     ultimaAvaliacao: index + "/03/2019",
    //     idade: parseInt(String(index) + index),
    //     inativo: true,
    //      });
    // }
    if (localStorage.getItem("dados")) {
      this.dados = JSON.parse(localStorage.getItem("dados"));
    }
  },
  watch: {
    dados(novosDados) {
      localStorage.setItem("dados", JSON.stringify(novosDados));
    },
  },
};
</script>
