<template>
  <v-card height="350"
          class="sminka text--white pa-2 d-flex flex-column justify-space-between">
    <img :src="sminka.image_link " />
    <h3 class="text-center sminka-title">{{ sminka.brand }}</h3>
    <h6>{{ sminka.name }}</h6>
    <h6>Price: {{ sminka.price }} {{ sminka.price_sign }}</h6>
    <v-dialog
        v-model="dialog"
        width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
            dark
            v-bind="attrs"
            v-on="on"
            color="pink"
        >
          Detalji
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          <!--{{ sminka.category }}-->
          Detalji
        </v-card-title>

        <v-card-text>
          {{ sminka.description }}
        </v-card-text>

        <v-divider></v-divider>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
export default {
  props: ['sminka'],
  data () {
    return {
      dialog: false
    }
  }
}
</script>

<style>
.sminka {
  background: #d96459 !important;
  color: white !important;
}

.sminka-title {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
</style>
