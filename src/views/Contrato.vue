<template>
  <v-row class="fill-height">
    <v-row class="fill-height">
      <!-- <template>
          <v-breadcrumbs :items="items">
            <template v-slot:item="{ item }">
              <v-breadcrumbs-item :href="item.href" :disabled="item.disabled">
                {{ item.text.toUpperCase() }}
              </v-breadcrumbs-item>
            </template>
          </v-breadcrumbs>
        </template>
       -->

      <template>
        <!--  :single-select="singleSelect" -->
        <!-- show-select -->
        <v-data-table
          :headers="headers"
          :items="desserts"
          :search="search"
          item-key="name"
          class="elevation-1"
          multi-sort
        >
          <template v-slot:top>
            <v-toolbar flat color="white">
              <v-toolbar-title>Contratos</v-toolbar-title>
              <v-divider class="mx-4" inset vertical></v-divider>

              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Buscar"
                single-line
                hide-details
              ></v-text-field>

              <v-spacer></v-spacer>
              <v-dialog v-model="dialog" max-width="70%">
                <template v-slot:activator="{ on }">
                  <v-btn color="primary" dark class="mb-2" v-on="on"
                    >Cadastrar</v-btn
                  >
                </template>
                <v-card>
                  <v-card-title>
                    <span class="headline">{{ formTitle }}</span>
                  </v-card-title>

                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12" sm="6" md="4">
                          <v-text-field
                            v-model="editedItem.name"
                            label="Dessert name"
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                          <v-text-field
                            v-model="editedItem.calories"
                            label="Calories"
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="4">
                          <v-text-field
                            v-model="editedItem.fat"
                            label="Fat (g)"
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                          <v-text-field
                            v-model="editedItem.carbs"
                            label="Carbs (g)"
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6">
                          <v-text-field
                            v-model="editedItem.protein"
                            label="Protein (g)"
                          ></v-text-field>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" text @click="close"
                      >Cancelar</v-btn
                    >
                    <v-btn color="blue darken-1" text @click="save"
                      >Salvar</v-btn
                    >
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-toolbar>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon small class="mr-2" @click="editItem(item)">
              mdi-pencil
            </v-icon>
            <v-icon small @click="deleteItem(item)">
              mdi-delete
            </v-icon>
          </template>
          <template v-slot:no-data>
            <v-btn color="primary" @click="initialize">Reset</v-btn>
          </template>
        </v-data-table>
      </template>
    </v-row>

    <!-- <template>
      <v-card>
        <v-card-title>
         
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Buscar"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <template>
          <v-row class="fill-height">
            <div>
              <v-data-table
                :headers="headers"
                :items="desserts"
                :search="search"
                :single-select="singleSelect"
                item-key="name"
                show-select
                multi-sort
              >
                <template v-slot:item.selecionado="{ item }">
                  <v-simple-checkbox
                    v-model="item.selecionado"
                    disabled
                  ></v-simple-checkbox>
                </template>
              </v-data-table>
            </div>
          </v-row>
        </template>
      </v-card>
    </template> -->

    <!-- Lista Padrao com painel expansivo -->
    <!-- <v-row justify="center">
      <v-expansion-panels popout focusable>
        <v-expansion-panel v-for="(items, i) in 10" :key="i">
          <v-expansion-panel-header>Contrato {{ i }}</v-expansion-panel-header>
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
    </v-row> -->
    <v-btn
      large
      bottom
      color="pink"
      dark
      fab
      fixed
      right
      @click="contrato = !contrato"
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn>

    <v-dialog v-model="contrato" width="60%">
      <v-card>
        <v-card-title class="grey darken-2">Contrato</v-card-title>

        <!-- <v-system-bar></v-system-bar> -->
        <v-toolbar flat>
          <v-toolbar-title>Novo Contrato</v-toolbar-title>
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
          <template>
            <v-card>
              <v-card-title>
                Selecione os serviços
                <v-spacer></v-spacer>
                <v-text-field
                  v-model="search"
                  append-icon="mdi-magnify"
                  label="Buscar"
                  single-line
                  hide-details
                ></v-text-field>
              </v-card-title>
              <template>
                <div>
                  <v-data-table
                    :headers="headers"
                    :items="desserts"
                    :search="search"
                    :single-select="singleSelect"
                    item-key="name"
                    show-select
                  >
                    <template v-slot:item.selecionado="{ item }">
                      <v-simple-checkbox
                        v-model="item.selecionado"
                        disabled
                      ></v-simple-checkbox>
                    </template>
                  </v-data-table>
                </div>
              </template>
            </v-card>
          </template>
          <!-- <v-row justify="center">
            <v-card>
              <v-card-title>
                Selecionar Serviços
                <v-spacer></v-spacer>
                <v-text-field
                  v-model="search"
                  append-icon="mdi-magnify"
                  label="Buscar"
                  single-line
                  hide-details
                ></v-text-field>
              </v-card-title>
              <v-data-table
                :headers="headers"
                :items="desserts"
                :search="search"
              ></v-data-table>
            </v-card>
          </v-row> -->
        </v-container>

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
          <v-btn text color="primary">Gerar Contrato</v-btn>
          <v-spacer />
          <v-btn text color="primary">Imprimir</v-btn>
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
    contrato: false,
    servicos: ["Reparação", "Canal", "Limpeza", "Clareamento"],

    search: "",
    singleSelect: false,
    selected: [],
    items: [
      {
        text: "Dashboard",
        disabled: false,
        href: "breadcrumbs_dashboard",
      },
      {
        text: "Link 1",
        disabled: false,
        href: "breadcrumbs_link_1",
      },
      {
        text: "Link 2",
        disabled: true,
        href: "breadcrumbs_link_2",
      },
    ],
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
      { text: "Carbs (g)", value: "carbs" },
      { text: "Protein (g)", value: "protein" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
    defaultItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Novo Item" : "Editar Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      const index = this.desserts.indexOf(item);
      confirm("Are you sure you want to delete this item?") &&
        this.desserts.splice(index, 1);
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>

<style></style>
