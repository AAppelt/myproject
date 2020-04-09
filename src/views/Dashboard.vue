<template>
  <v-row>
    <v-card class="mx-auto text-center" color="green" dark max-width="35%">
      <v-card-text>
        <v-sheet color="rgba(0, 0, 0, .12)">
          <v-sparkline
            :value="value"
            color="rgba(255, 255, 255, .7)"
            height="100"
            padding="24"
            stroke-linecap="round"
            smooth
          >
            <template v-slot:label="labels"> R${{ labels.value }} </template>
          </v-sparkline>
        </v-sheet>
      </v-card-text>

      <v-card-text>
        <div class="display-1 font-weight-thin">Estatísticas 1</div>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions class="justify-center">
        <v-btn block text>Ir para Relatório</v-btn>
      </v-card-actions>
    </v-card>

    <v-card class="mx-auto" color="grey lighten-4" max-width="600">
      <v-card-title>
        <v-icon
          :color="checking ? 'red lighten-2' : 'indigo'"
          class="mr-12"
          size="64"
          @click="takePulse"
        >
          mdi-calculator-variant
        </v-icon>
        <v-row align="start">
          <div class="caption grey--text text-uppercase">
            Interativo
          </div>
          <div>
            <span
              class="display-2 font-weight-black"
              v-text="avg || '—'"
            ></span>
            <strong v-if="avg">UN</strong>
          </div>
        </v-row>

        <v-spacer></v-spacer>

        <!-- <v-btn icon class="align-self-start" size="28">
        <v-icon>mdi-arrow-right-thick</v-icon>
      </v-btn> -->
      </v-card-title>

      <v-sheet color="transparent">
        <v-sparkline
          :key="String(avg)"
          :smooth="16"
          :gradient="['#f72047', '#ffd200', '#1feaea']"
          :line-width="3"
          :value="heartbeats"
          auto-draw
          stroke-linecap="round"
        ></v-sparkline>
      </v-sheet>
    </v-card>

    <v-card class="mt-4 mx-auto" max-width="400">
      <v-sheet
        class="v-sheet--offset mx-auto"
        color="cyan"
        elevation="12"
        max-width="calc(100% - 32px)"
      >
        <v-sparkline
          :labels="labels"
          :value="value"
          color="white"
          line-width="2"
          padding="16"
        ></v-sparkline>
      </v-sheet>

      <v-card-text class="pt-0">
        <div class="title font-weight-light mb-2">Estatsticas 2</div>
        <div class="subheading font-weight-light grey--text">
          Subtítulo estatísticas 2
        </div>
        <v-divider class="my-2"></v-divider>
        <v-icon class="mr-2" small>
          mdi-clock
        </v-icon>
        <span class="caption grey--text font-weight-light"
          >Última atualização à 26 minutos</span
        >
      </v-card-text>
    </v-card>

    
  </v-row>
</template>

<script>
const exhale = ms => new Promise(resolve => setTimeout(resolve, ms));
export default {
  data: () => ({
    checking: false,
    heartbeats: [],
    value: [423, 446, 675, 510, 590, 610, 760],
    labels: [
      "Domingo",
      "Segunda",
      "Terça",
      "Quarta",
      "Quinta",
      "Sexta",
      "Sábado"
    ]
  }),
  computed: {
    avg() {
      const sum = this.heartbeats.reduce((acc, cur) => acc + cur, 0);
      const length = this.heartbeats.length;

      if (!sum && !length) return 0;

      return Math.ceil(sum / length);
    }
  },

  created() {
    this.takePulse(false);
  },

  methods: {
    heartbeat() {
      return Math.ceil(Math.random() * (120 - 80) + 80);
    },
    async takePulse(inhale = true) {
      this.checking = true;

      inhale && (await exhale(1000));

      this.heartbeats = Array.from({ length: 20 }, this.heartbeat);

      this.checking = false;
    }
  }
};
</script>

<style></style>
