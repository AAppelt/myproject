<template>
  <v-row class="fill-height">
    <v-row justify="center"> </v-row>
    <v-btn
      large
      bottom
      color="pink"
      dark
      fab
      fixed
      right
      @click="servico = !servico"
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn>

    <v-dialog v-model="servico" width="60%">
      <v-card>
        <v-card-title class="grey darken-2">Serviço</v-card-title>

        <!-- <v-system-bar></v-system-bar> -->
        <v-toolbar flat>
          <v-toolbar-title>Cadastrar Serviço</v-toolbar-title>
          <v-spacer></v-spacer>
          <!-- <div>
            <v-switch
              v-model="sticky"
              label="Sticky Banner"
              hide-details
            ></v-switch>
          </div> -->
        </v-toolbar>

        <!-- <v-banner> -->
        <!-- <v-avatar slot="icon" color="deep-purple accent-4" size="40">
            <v-icon icon="mdi-lock" color="white">
              mdi-lock
            </v-icon>
          </v-avatar> -->
        <v-container>
          <v-row justify="center">
            <v-col cols="12" sm="12" md="12">
              <v-text-field class="mx-2" label="Serviço"></v-text-field>
            </v-col>

            <!-- <v-col cols="12" sm="12" md="12">
            <v-text-field class="mx-2" label="Descrição"></v-text-field>
          </v-col> -->

            <v-container fluid>
              <v-textarea
                prepend-icon="mdi-comment"
                name="input-7-1"
                filled
                label="Descrição"
                auto-grow
              ></v-textarea>
            </v-container>
            <v-col cols="12" sm="4" md="4">
              <v-text-field
                class="mx-2"
                label="Código Serviço Município"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field class="mx-2" label="CNAE"></v-text-field>
            </v-col>
            <v-col cols="12" sm="4" md="4">
              <v-text-field class="mx-2" label="Valor Unitário"></v-text-field>
            </v-col>
          </v-row>
        </v-container>

        <!-- <v-banner single-line :sticky="sticky">

          <v-row class="fill-width">
            <v-text-field label="Tratamento"></v-text-field>
            <v-text-field label="Descrição"></v-text-field>
            <v-btn  text color="deep-purple accent-4">Adicionar</v-btn>
          </v-row> -->

        <!-- <template v-slot:actions>
            <v-btn text color="deep-purple accent-4">Adicionar</v-btn>
          </template> -->

        <!--</v-banner> -->
        <v-spacer></v-spacer>

        
        <v-card-actions>
          <v-btn text color="primary">Mais</v-btn>
          <v-spacer />
          <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
          <v-btn text @click="dialog = false">Salvar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    servico: false
  })
};
</script>

<style></style>
