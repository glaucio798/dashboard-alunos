<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-btn
        v-bind="attrs"
        v-on="on"
        class="text-h6 py-6"
        color="#fd6550"
        style="color: white"
      >
        <v-icon class="mr-2">mdi-account-multiple-plus</v-icon> NOVO ALUNO
      </v-btn>
    </template>
    <v-card>
      <v-card-title style="background-color: #290d95; color: white">
        <v-row no-gutters justify="space-between"
          ><span class="headline">Cadastrar Aluno</span>
          <v-icon
            color="white"
            @click="
              dialog = false;
              cancel();
            "
            >mdi-close</v-icon
          ></v-row
        >
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row class="pt-5">
            <v-col cols="12">
              <p class="font-weight-bold">Nome:*</p>
              <v-text-field
                v-model="aluno.nome"
                style="border-radius: 0 !important"
                required
                filled
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <p class="font-weight-bold">Email:*</p>
              <v-text-field
                v-model="aluno.email"
                style="border-radius: 0 !important"
                required
                filled
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <p class="font-weight-bold">Idade:*</p>
              <v-text-field
                v-model="aluno.idade"
                style="border-radius: 0 !important"
                required
                filled
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="9">
              <p class="font-weight-bold">Telefone:*</p>
              <v-text-field
                v-model="aluno.telefone"
                style="border-radius: 0 !important"
                required
                filled
                dense
              ></v-text-field>
            </v-col>
            <v-col cols="3">
              <v-switch
                v-model="aluno.ativo"
                :label="!aluno.ativo ? 'Inativo' : 'Ativo'"
              ></v-switch>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-row justify="space-between" no-gutters class="px-6 mb-5">
          <v-btn
            color="#30188b"
            text
            @click="
              dialog = false;
              cancel();
            "
          >
            CANCELAR
          </v-btn>

          <v-btn color="#ff6450" style="color: white" @click="submit()">
            SALVAR
          </v-btn>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      dialog: false,
      aluno: {
        nome: "",
        email: "",
        telefone: "",
        idade: "",
        ativo: true,
      },
    };
  },
  methods: {
    submit() {
      if (
        this.aluno.nome == "" ||
        this.aluno.email == "" ||
        this.aluno.telefone == "" ||
        this.aluno.idade == ""
      )
        alert("Faltam dados no formulario");
      else {
        this.dialog = false;
        this.$emit("novoaluno", this.aluno);
        this.aluno = {
          nome: "",
          email: "",
          telefone: "",
          idade: "",
          ativo: true,
        };
      }
    },
    cancel() {
      console.log("cancela amore");
      this.aluno = {
        nome: "",
        email: "",
        telefone: "",
        idade: "",
        inativo: false,
      };
    },
  },
};
</script>

<style scoped>
p {
  margin: 0;
  padding-left: 15px;
  color: black;
  background-color: #f0f0f0;
}
</style>