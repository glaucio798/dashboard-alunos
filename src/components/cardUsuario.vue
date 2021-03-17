<template>
  <v-card
    :elevation="inativo ? '0' : '3'"
    class="mx-auto"
    width="389"
    outlined
    :color="inativo ? 'indigo lighten-5' : ''"
  >
    <v-list-item class="my-3">
      <v-avatar class="mr-3">
        <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
      </v-avatar>
      <v-list-item-content>
        <v-list-item-title class="headline mb-0">
          {{ nome }}
        </v-list-item-title>
        <v-list-item-subtitle>
          Ultima avaliação: {{ ultimaAvaliacao }}
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-divider></v-divider>

    <v-list-item class="my-2" two-line>
      <v-list-item-content>
        <v-row no-gutters>
          <v-col cols="12" class="px-0 py-0">
            <v-list-item-subtitle class="mb-2">
              {{ email }}
            </v-list-item-subtitle>
          </v-col>
          <v-col cols="12" class="px-0 py-0">
            <v-list-item-subtitle>
              <span class="mr-1">{{ idade }} anos</span>
              {{ telefone }}
            </v-list-item-subtitle>
          </v-col>
        </v-row>
      </v-list-item-content>
      <v-card-actions>
        <v-btn class="mr-4" small fab>
          <v-icon :color="inativo ? 'grey lighten-1' : 'blue darken-4'"
            >mdi-pencil</v-icon
          ></v-btn
        >
        <v-icon
          class="mr-2"
          :color="inativo ? 'grey lighten-1' : 'blue darken-4'"
          >mdi-dots-horizontal</v-icon
        ></v-card-actions
      >
    </v-list-item>
  </v-card>
</template>

<script>
export default {
  name: "cardUsuario",
  props: {
    nome: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    telefone: {
      type: String,
      required: true,
    },
    ultimaAvaliacao: {
      type: String, //Aqui vai ser date caso integre com um backend
      required: true,
    },
    idade: {
      type: Number,
      required: true,
    },
    inativo: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
};
</script>

<style>
</style>