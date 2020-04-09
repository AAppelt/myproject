<template>
  <v-row class="fill-height">
    <v-row justify="center">
      <v-expansion-panels popout focusable>
        <v-expansion-panel v-for="(items, i) in 10" :key="i">
          <v-expansion-panel-header>Cliente {{ i }}</v-expansion-panel-header>
          <v-expansion-panel-content>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
            ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
            aliquip ex ea commodo consequat.

            <v-card-actions>
              <v-btn text color="primary" @click="prontuario = !prontuario"
                >Prontuário</v-btn
              >
              <v-spacer />
              <v-btn text color="primary" @click="dialog = false"
                >Cancelar</v-btn
              >
              <v-btn text @click="dialog = false">Salvar</v-btn>
            </v-card-actions>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-row>

    <v-btn
      large
      bottom
      color="pink"
      dark
      fab
      fixed
      right
      @click="dialog = !dialog"
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="prontuario" width="60%">
      <v-card>
        <v-card-title class="grey darken-2">Prontuário Cliente</v-card-title>

        <!-- <v-system-bar></v-system-bar> -->
        <v-toolbar flat>
          <v-toolbar-title>Lançar Atendimento</v-toolbar-title>
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
        <v-row justify="center">
          <!-- <v-col cols="10" sm="6"> -->
          <v-text-field class="mx-2" label="Tratamento"></v-text-field>
          <!-- </v-col> -->

          <!-- <v-col cols="10" sm="6"> -->
          <v-text-field class="mx-2" label="Descrição"></v-text-field>
          <!-- </v-col> -->
          <!-- <v-col cols="2">
              
            </v-col> -->
          <v-btn color="primary accent-4">Adicionar</v-btn>
        </v-row>

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

        <v-row class="mx-2">
          <v-timeline>
            <v-timeline-item
              v-for="(year, i) in years"
              :key="i"
              :color="year.color"
              small
            >
              <template v-slot:opposite>
                <span
                  :class="`headline font-weight-bold ${year.color}--text`"
                  v-text="year.year"
                ></span>
              </template>
              <div class="py-4">
                <h2
                  :class="`headline font-weight-light mb-4 ${year.color}--text`"
                >
                  Lorem ipsum
                </h2>
                <div>
                  Lorem ipsum dolor sit amet, no nam oblique veritus. Commune
                  scaevola imperdiet nec ut, sed euismod convenire principes at.
                  Est et nobis iisque percipit, an vim zril disputando
                  voluptatibus, vix an salutandi sententiae.
                </div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </v-row>
        <v-card-actions>
          <v-btn text color="primary">Mais</v-btn>
          <v-spacer />
          <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
          <v-btn text @click="dialog = false">Salvar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog v-model="dialog" width="60%">
      <div>
        <v-card-title class="grey darken-2">Cliente</v-card-title>

        <!-- <v-system-bar></v-system-bar> -->
        <!-- <v-toolbar flat>
          <v-toolbar-title>Lançar Atendimento</v-toolbar-title>
          <v-spacer></v-spacer>
          <div>
            <v-switch
              v-model="sticky"
              label="Sticky Banner"
              hide-details
            ></v-switch>
          </div>
        </v-toolbar> -->
        <v-tabs
          v-model="tab"
          background-color="deep-purple accent-4"
          class="elevation-2"
          dark
          grow="grow"
        >
          <v-tabs-slider></v-tabs-slider>

          <v-tab v-for="i in tabs" :key="i" :href="`#tab-${i}`">
            Tab {{ i }}
            <v-icon v-if="icons">mdi-phone</v-icon>
          </v-tab>

          <v-tab-item v-for="i in tabs" :key="i" :value="'tab-' + i">
            <v-card>
              <v-card-title>
                <!-- <span class="headline">Cliente</span> -->
                <small>* indica campo obrigatório </small>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field label="Nome*" required></v-text-field>
                    </v-col>
                    <!-- <v-col cols="12" sm="6" md="4">
                      <v-text-field label="Idade*" required></v-text-field>
                    </v-col> -->
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field
                        label="Data Nascimento"
                        hint="exemplo de texto auxiliar apenas quando focado"
                      ></v-text-field>
                    </v-col>
                    <v-col class="d-flex" cols="12" sm="6" md="6">
                      <v-select :items="sexo" label="Sexo"></v-select>
                    </v-col>
                    <v-col cols="12">
                      <v-text-field label="Email*" required></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field label="CPF*" required></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field label="RG*" required></v-text-field>
                    </v-col>
                    <v-container fluid>
                          <v-textarea
                            prepend-icon="mdi-comment"
                            name="input-7-1"
                            filled
                            label="Observações"
                            auto-grow                           
                          ></v-textarea>
                        </v-container>
                    <!-- <v-col cols="12">
                      <v-text-field
                        label="Password*"
                        type="password"
                        required
                      ></v-text-field>
                    </v-col> -->
                    <!-- <v-col cols="12" sm="6">
                      <v-select
                        :items="['0-17', '18-29', '30-54', '54+']"
                        label="Idade*"
                        required
                      ></v-select>
                    </v-col>
                    <v-col cols="12" sm="6">
                      <v-autocomplete
                        :items="[
                          'Skiing',
                          'Ice hockey',
                          'Soccer',
                          'Basketball',
                          'Hockey',
                          'Reading',
                          'Writing',
                          'Coding',
                          'Basejump',
                        ]"
                        label="Interests"
                        multiple
                      ></v-autocomplete>
                    </v-col> -->
                  </v-row>
                </v-container>
                <!-- <small>*indicates required field</small> -->
              </v-card-text>
              <v-card-actions>
                <v-btn text color="primary">Mais</v-btn>
                <v-spacer />
                <v-btn text color="primary" @click="dialog = false"
                  >Cancelar</v-btn
                >
                <v-btn text @click="dialog = false">Salvar</v-btn>
              </v-card-actions>
            </v-card>
          </v-tab-item>
        </v-tabs>
      </div>
    </v-dialog>
    <!-- <v-card>
        <v-card-title class="grey darken-2">
          Cadastrar Cliente
        </v-card-title>
        <v-container> -->
    <!-- <v-row class="mx-2">
            <v-col class="align-center justify-space-between" cols="12">
              <v-row align="center" class="mr-0"> -->
    <!-- <v-card class="overflow-hidden" color="purple lighten-1" dark>
                  <v-toolbar flat color="purple">
                    <v-icon>mdi-account</v-icon>
                    <v-toolbar-title class="font-weight-light"
                      >User Profile</v-toolbar-title
                    >
                    <v-spacer></v-spacer>
                    <v-btn
                      color="purple darken-3"
                      fab
                      small
                      @click="isEditing = !isEditing"
                    >
                      <v-icon v-if="isEditing">mdi-close</v-icon>
                      <v-icon v-else>mdi-pencil</v-icon>
                    </v-btn>
                  </v-toolbar> -->

    <!-- <v-card-text>
                  <v-tabs fixed-tabs background-color="indigo" dark>
                    <v-tabs-slider></v-tabs-slider>
                    <v-tab href="#clientedados">
                      Dados
                      
                    </v-tab>
                    <v-tab>
                      Endereço
                    </v-tab>
                    <v-tab>
                      Items
                    </v-tab>
                    <v-tab>
                      Another Screen
                    </v-tab>
                  </v-tabs> -->

    <!-- <v-tabs-items>
                    <v-tab-item value="clientedados">
                      <v-card flat>
                        <v-text-field
                          :rules="rules"
                          label="Endereço"
                        ></v-text-field>
                        <v-text-field
                          :rules="rules"
                          label="Cidade"
                        ></v-text-field>
                        <v-select
                          v-model="e1"
                          :items="states"
                          menu-props="auto"
                          label="Selecione"
                          hide-details
                          prepend-icon="mdi-map"
                          single-line
                        ></v-select>
                        <v-container fluid>
                          <v-textarea
                            prepend-icon="mdi-comment"
                            name="input-7-1"
                            filled
                            label="Observações"
                            auto-grow
                            value="Lorem ipsum dolor sit amet, no nam oblique veritus. Commune scaevola imperdiet nec ut, sed euismod convenire principes at. Est et nobis iisque percipit, an vim zril disputando voluptatibus, vix an salutandi sententiae."
                          ></v-textarea>
                        </v-container>
                      </v-card>
                    </v-tab-item>
                  </v-tabs-items> -->

    <!-- <v-text-field :rules="rules" label="Endereço"></v-text-field>
                  <v-text-field :rules="rules" label="Cidade"></v-text-field>
                  <v-select
                    v-model="e1"
                    :items="states"
                    menu-props="auto"
                    label="Selecione"
                    hide-details
                    prepend-icon="mdi-map"
                    single-line
                  ></v-select>
                  <v-container fluid>
                    <v-textarea
                      prepend-icon="mdi-comment"
                      name="input-7-1"
                      filled
                      label="Observações"
                      auto-grow
                      value="Lorem ipsum dolor sit amet, no nam oblique veritus. Commune scaevola imperdiet nec ut, sed euismod convenire principes at. Est et nobis iisque percipit, an vim zril disputando voluptatibus, vix an salutandi sententiae."
                    ></v-textarea>
                  </v-container> -->
    <!-- </v-card-text>
                <v-divider></v-divider> -->
    <!-- <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn :disabled="!isEditing" color="success" @click="save">
                    Save
                  </v-btn>
                </v-card-actions> -->
    <!-- <v-snackbar
                  v-model="hasSaved"
                  :timeout="2000"
                  absolute
                  bottom
                  left
                >
                  Your profile has been updated
                </v-snackbar> -->
    <!-- </v-card> -->
    <!-- </v-row> -->
    <!-- </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-btn text color="primary">Mais</v-btn>
          <v-spacer />
          <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
          <v-btn text @click="dialog = false">Salvar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row> -->
  </v-row>
</template>

<script>
export default {
  data: () => ({
    e1: "Paraná",
    tabs: 3,
    hasSaved: false,
    isEditing: null,
    dialog: false,
    prontuario: false,
    model: null,
    sexo: ["Masculino", "Femenino"],
    // states: [
    //   { name: "Florida", abbr: "FL", id: 1 },
    //   { name: "Georgia", abbr: "GA", id: 2 },
    //   { name: "Nebraska", abbr: "NE", id: 3 },
    //   { name: "California", abbr: "CA", id: 4 },
    //   { name: "New York", abbr: "NY", id: 5 }
    // ],
    methods: {
      customFilter(item, queryText) {
        const textOne = item.name.toLowerCase();
        const textTwo = item.abbr.toLowerCase();
        const searchText = queryText.toLowerCase();

        return (
          textOne.indexOf(searchText) > -1 || textTwo.indexOf(searchText) > -1
        );
      },
      save() {
        this.isEditing = !this.isEditing;
        this.hasSaved = true;
      },
    },
    items: ["web", "shopping", "videos", "images", "news"],
    text:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",

    years: [
      {
        color: "cyan",
        year: "2000",
      },
      {
        color: "green",
        year: "1990",
      },
      {
        color: "pink",
        year: "1980",
      },
      {
        color: "amber",
        year: "1970",
      },
      {
        color: "orange",
        year: "1960",
      },
    ],
    items1: [
      { text: "State 1" },
      { text: "State 2" },
      { text: "State 3" },
      { text: "State 4" },
      { text: "State 5" },
      { text: "State 6" },
      { text: "State 7" },
    ],
    states: [
      "Acre (AC)",
      "Alagoas (AL)",
      "Amapá (AP)",
      "Amazonas (AM)",
      "Bahia (BA)",
      "Ceará (CE)",
      "Distrito Federal (DF)",
      "Espírito Santo (ES)",
      "Goiás (GO)",
      "Maranhão (MA)",
      "Mato Grosso (MT)",
      "Mato Grosso do Sul (MS)",
      "Minas Gerais (MG)",
      "Pará (PA)",
      "Paraíba (PB)",
      "Paraná (PR)",
      "Pernambuco (PE)",
      "Piauí (PI)",
      "Rio de Janeiro (RJ)",
      "Rio Grande do Norte (RN)",
      "Rio Grande do Sul (RS)",
      "Rondônia (RO)",
      "Roraima (RR)",
      "Santa Catarina (SC)",
      "São Paulo (SP)",
      "Sergipe (SE)",
      "Tocantins (TO)",
    ],
  }),
};
</script>

<style></style>
