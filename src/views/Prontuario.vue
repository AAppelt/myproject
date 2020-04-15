<template>
  <v-row class="fill-height">
    <v-row justify="center">
      <v-expansion-panels popout focusable>
        <v-expansion-panel v-for="(items, i) in 10" :key="i">
          <v-expansion-panel-header>Cliente {{ i }}</v-expansion-panel-header>
          <v-expansion-panel-content>

            <v-row justify="fill-height">
              <v-text-field
                v-model="name"
                :counter="10"
                :rules="nameRules"
                label="Name"
                required
              ></v-text-field>

              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                required
              ></v-text-field>

              <v-btn
                :disabled="!valid"
                color="success"
                class="mr-4"
                @click="validate"
              >
                ADICIONAR
              </v-btn>             
           </v-row>

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
                    :class="
                      `headline font-weight-light mb-4 ${year.color}--text`
                    "
                  >
                    Lorem ipsum
                  </h2>
                  <div>
                    Lorem ipsum dolor sit amet, no nam oblique veritus. Commune
                    scaevola imperdiet nec ut, sed euismod convenire principes
                    at. Est et nobis iisque percipit, an vim zril disputando
                    voluptatibus, vix an salutandi sententiae.
                  </div>
                </div>
              </v-timeline-item>
            </v-timeline>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-row>

    <!-- <v-col cols="12">
      <v-card color="#385F73" dark>
        <v-card-title class="headline">Unlimited music now</v-card-title>

        <v-card-subtitle
          >Listen to your favorite artists and albums whenever and wherever,
          online and offline.</v-card-subtitle
        >

        <v-card-actions>
          <v-btn text>Listen Now</v-btn>
        </v-card-actions>
      </v-card>
    </v-col> -->

    <!-- <v-col v-for="(item, i) in items" :key="i" cols="12">
      <v-card :color="item.color" dark>
        <div class="d-flex flex-no-wrap justify-space-between">
          <div>
            <v-card-title class="headline" v-text="item.title"></v-card-title>

            <v-card-subtitle v-text="item.artist"></v-card-subtitle>
          </div>

          <v-avatar class="ma-3" size="125" tile>
            <v-img :src="item.src"></v-img>
          </v-avatar>
        </div>
      </v-card>
    </v-col> -->
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
    <v-dialog v-model="dialog" width="800px">
      <v-card>
        <v-card-title class="grey darken-2">
          Criar Prontuário
        </v-card-title>
        <v-container>
          <v-row class="mx-2">
            <v-col class="align-center justify-space-between" cols="12">
              <v-row align="center" class="mr-0">
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
                <v-card-text>
                  <v-text-field
                    :disabled="!isEditing"
                    color="white"
                    label="Name"
                  ></v-text-field>
                  <v-autocomplete
                    :disabled="!isEditing"
                    :items="states"
                    :filter="customFilter"
                    color="white"
                    item-text="name"
                    label="State"
                  ></v-autocomplete>
                </v-card-text>
                <v-divider></v-divider>
                <!-- <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn :disabled="!isEditing" color="success" @click="save">
                    Save
                  </v-btn>
                </v-card-actions> -->
                <v-snackbar
                  v-model="hasSaved"
                  :timeout="2000"
                  absolute
                  bottom
                  left
                >
                  Your profile has been updated
                </v-snackbar>
                <!-- </v-card> -->
              </v-row>
            </v-col>
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
  </v-row>
</template>

<script>
export default {
  data: () => ({
    hasSaved: false,
    isEditing: null,
    dialog: false,
    model: null,
    states: [
      { name: "Florida", abbr: "FL", id: 1 },
      { name: "Georgia", abbr: "GA", id: 2 },
      { name: "Nebraska", abbr: "NE", id: 3 },
      { name: "California", abbr: "CA", id: 4 },
      { name: "New York", abbr: "NY", id: 5 }
    ],
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

    // items: [
    //   {
    //     color: "#1F7087",
    //     src: "https://cdn.vuetifyjs.com/images/cards/foster.jpg",
    //     title: "Supermodel",
    //     artist: "Foster the People"
    //   },
    //   {
    //     color: "#952175",
    //     src: "https://cdn.vuetifyjs.com/images/cards/halcyon.png",
    //     title: "Halcyon Days",
    //     artist: "Ellie Goulding"
    //   },
    //   {
    //     color: "#1F7087",
    //     src: "https://cdn.vuetifyjs.com/images/cards/foster.jpg",
    //     title: "Supermodel",
    //     artist: "Foster the People"
    //   },
    //   {
    //     color: "#952175",
    //     src: "https://cdn.vuetifyjs.com/images/cards/halcyon.png",
    //     title: "Halcyon Days",
    //     artist: "Ellie Goulding"
    //   },
    //   {
    //     color: "#1F7087",
    //     src: "https://cdn.vuetifyjs.com/images/cards/foster.jpg",
    //     title: "Supermodel",
    //     artist: "Foster the People"
    //   },
    //   {
    //     color: "#952175",
    //     src: "https://cdn.vuetifyjs.com/images/cards/halcyon.png",
    //     title: "Halcyon Days",
    //     artist: "Ellie Goulding"
    //   }
    // ],
    years: [
      {
        color: "cyan",
        year: "1960"
      },
      {
        color: "green",
        year: "1970"
      },
      {
        color: "pink",
        year: "1980"
      },
      {
        color: "amber",
        year: "1990"
      },
      {
        color: "orange",
        year: "2000"
      }
    ]
  })
};
</script>

<style></style>
