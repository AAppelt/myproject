<template>
  <v-row class="fill-height">
    <v-row class="fill-height">
      <!-- DESTAQUES OU ULTIMOS ATENDIDOS -->
      <v-row no-gutters justify="center">
      
      </v-row>

      <!-- LISTA PADRAO -->
      <!-- <v-card class="mx-auto">
        <v-list nav three-line>
          <template v-for="(item, index) in cards">
            <v-subheader v-if="item.header" :key="item.header" v-text="item.header"></v-subheader>
            <v-divider v-else-if="item.divider" :key="index" :inset="item.inset"></v-divider>

            <v-list-item v-else :key="item.title">
              <v-card>
                <v-row>
                  <v-col cols="12" sm="2" md="2">
                    <v-list-item-avatar>
                      <v-img :src="item.src"></v-img>
                    </v-list-item-avatar>
                  </v-col>

                  <v-list-item-content>
                    <v-col align-self="left" cols="12" sm="5" md="5">
                      <v-list-item-title v-html="item.title"></v-list-item-title>
                    </v-col>
                    <v-col cols="12" sm="5" md="5">
                      <v-list-item-subtitle v-html="text"></v-list-item-subtitle>
                    </v-col>
                  </v-list-item-content>
                </v-row>
                <v-card-actions>
                  <v-btn text color="primary" @click="prontuario = !prontuario">Prontuário</v-btn>
                  <v-spacer />
                  <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
                  <v-btn text @click="dialog = false">Salvar</v-btn>
                </v-card-actions>
              </v-card>
            </v-list-item>
          </template>
        </v-list>
      </v-card> -->

      <!-- Expsansion List -->
      <!-- <v-expansion-panels popout focusable>
        <v-expansion-panel v-for="(items, i) in 10" :key="i">
          <v-expansion-panel-header>Cliente {{ i }}</v-expansion-panel-header>
          <v-expansion-panel-content>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
            ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
            aliquip ex ea commodo consequat.
            <v-card-actions>
              <v-btn text color="primary" @click="prontuario = !prontuario">Prontuário</v-btn>
              <v-spacer />
              <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
              <v-btn text @click="dialog = false">Salvar</v-btn>
            </v-card-actions>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels> -->

      <!-- CARDS -->
      <v-container fluid>
        <v-row dense>
          <v-col v-for="card in cards" :key="card.title" :cols="card.flex">
            <v-card>
              <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title v-text="card.title"></v-card-title>
              </v-img>

              <v-card-actions style="background:grey">
                <v-spacer></v-spacer>

                <v-btn icon @click="prontuario = !prontuario">
                  <v-icon>mdi-heart</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-bookmark</v-icon>
                </v-btn>

                <v-btn icon>
                  <v-icon>mdi-share-variant</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-row>

    <v-btn large bottom color="pink" dark fab fixed right @click="dialog = !dialog">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="prontuario" width="70%">
      <v-container>
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
            </div>-->
          </v-toolbar>

          <v-row class="fill-height" justify="center">
            <v-col cols="12">
              <v-text-field class="mx-2" label="Tratamento"></v-text-field>
            </v-col>

            <v-col cols="12" sm="8" md="8">
              <v-container fluid>
                <v-textarea
                  prepend-icon="mdi-comment"
                  name="input-7-1"
                  filled
                  label="Descrição"
                  auto-grow
                ></v-textarea>
              </v-container>
            </v-col>
            <v-col align-self="center" cols="12" sm="4" md="4">
              <v-btn color="primary accent-4">Adicionar</v-btn>
            </v-col>
          </v-row>

          <v-spacer></v-spacer>

          <v-row class="mx-2">
            <v-timeline>
              <v-timeline-item v-for="(year, i) in years" :key="i" :color="year.color" small>
                <template v-slot:opposite>
                  <span :class="`headline font-weight-bold ${year.color}--text`" v-text="year.year"></span>
                </template>
                <div class="py-4">
                  <h2 :class="`headline font-weight-light mb-4 ${year.color}--text`">Lorem ipsum</h2>
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
      </v-container>
    </v-dialog>

    <v-dialog v-model="dialog" width="60%">
      <div>
        <v-card-title class="grey darken-2">Cliente</v-card-title>

        <v-tabs
          v-model="tab"
          background-color="deep-purple accent-4"
          class="elevation-2"
          dark
          grow="grow"
        >
          <v-tabs-slider></v-tabs-slider>

          <!-- <v-tab v-for="i in tabs" :key="i" :href="`#tab-${i}`"> -->
          <v-tab href="#tab-1">
            Dados
            <v-icon v-if="icons">mdi-phone</v-icon>
          </v-tab>
          <v-tab href="#tab-2">
            Endereço
            <v-icon v-if="icons">mdi-phone</v-icon>
          </v-tab>
          <v-tab href="#tab-3">
            Financeiro
            <v-icon v-if="icons">mdi-phone</v-icon>
          </v-tab>

          <!-- <v-tab-item v-for="i in tabs" :key="i" :value="'tab-' + i"> -->
          <v-tab-item value="tab-1">
            <v-card>
              <v-card-title>
                <!-- <span class="headline">Cliente</span> -->
                <small>* indica campo obrigatório</small>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row dense>
                    <v-col cols="12">
                      <v-text-field label="Nome*" required></v-text-field>
                    </v-col>
                    <!-- <v-col cols="12" sm="6" md="4">
                      <v-text-field label="Idade*" required></v-text-field>
                    </v-col>-->
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
                  </v-row>
                </v-container>
                <!-- <small>*indicates required field</small> -->
              </v-card-text>
              <v-card-actions>
                <v-btn text color="primary">Mais</v-btn>
                <v-spacer />
                <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
                <v-btn text @click="dialog = false">Salvar</v-btn>
              </v-card-actions>
            </v-card>
          </v-tab-item>

          <v-tab-item value="tab-2">
            <v-card>
              <v-card-title>
                <!-- <span class="headline">Cliente</span> -->
                <small>* indica campo obrigatório</small>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row dense>
                    <v-col cols="12">
                      <v-text-field label="Endereço*" required></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field
                        label="Bairro"
                        hint="exemplo de texto auxiliar apenas quando focado"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field label="Cidade*" required></v-text-field>
                    </v-col>
                    <v-col class="d-flex" cols="12" sm="6" md="6">
                      <v-select :items="states" label="Estado"></v-select>
                    </v-col>
                    <v-col cols="12" sm="6" md="6">
                      <v-text-field label="CEP*" required></v-text-field>
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
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-btn text color="primary">Mais</v-btn>
                <v-spacer />
                <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
                <v-btn text @click="dialog = false">Salvar</v-btn>
              </v-card-actions>
            </v-card>
          </v-tab-item>

          <v-tab-item value="tab-3">
            <v-card>
              <v-card-title>
                <!-- <span class="headline">Cliente</span> -->
                <small>Dados Financeiros</small>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row dense></v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-btn text color="primary">Mais</v-btn>
                <v-spacer />
                <v-btn text color="primary" @click="dialog = false">Cancelar</v-btn>
                <v-btn text @click="dialog = false">Salvar</v-btn>
              </v-card-actions>
            </v-card>
          </v-tab-item>
        </v-tabs>
      </div>
    </v-dialog>
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
      }
    },
    items: ["web", "shopping", "videos", "images", "news"],
    text:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",

    years: [
      {
        color: "cyan",
        year: "2000"
      },
      {
        color: "green",
        year: "1990"
      },
      {
        color: "pink",
        year: "1980"
      },
      {
        color: "amber",
        year: "1970"
      },
      {
        color: "orange",
        year: "1960"
      }
    ],
    items1: [
      { text: "State 1" },
      { text: "State 2" },
      { text: "State 3" },
      { text: "State 4" },
      { text: "State 5" },
      { text: "State 6" },
      { text: "State 7" }
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
      "Tocantins (TO)"
    ],
    cards: [
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/80.jpg",
        flex: 2
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 2
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/50.jpg",
        flex: 2
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/60.jpg",
        flex: 2
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/women/66.jpg",
        flex: 2
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/61.jpg",
        flex: 2
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/22.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/women/70.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/85.jpg",
        flex: 3
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/44.jpg",
        flex: 3
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/80.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/50.jpg",
        flex: 3
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/60.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/women/66.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/61.jpg",
        flex: 3
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/women/22.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/women/70.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/85.jpg",
        flex: 3
      },
      {
        title: "Pre-fab homes",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 3
      },
      {
        title: "Favorite road trips",
        src: "https://randomuser.me/api/portraits/lego/6.jpg",
        flex: 3
      },
      {
        title: "Best airlines",
        src: "https://randomuser.me/api/portraits/women/44.jpg",
        flex: 3
      }
    ]
  })
};
</script>

<style></style>
