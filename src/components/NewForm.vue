<template>
  <v-form @submit.prevent="submit">
    <v-container>
      <v-row>
        <v-col
            cols="12"
        >
          <v-text-field
              v-model="brand"
              :counter="10"
              label="Brend"
              required
          ></v-text-field>
        </v-col>

        <v-col
            cols="12"
        >
          <v-text-field
              v-model="name"
              :counter="10"
              label="Naziv"
              required
          ></v-text-field>
        </v-col>

        <v-col
            cols="12"
        >
          <v-text-field
              v-model="price"
              label="Cijena"
              type="number"
              required
          ></v-text-field>
        </v-col>

         <v-col
            cols="12"
        >
          <v-text-field
              v-model="description"
              label="Detalji"
              required
          ></v-text-field>
        </v-col>

        <v-col cols="12">
          <v-btn type="submit" variant="primary">
            Submit
          </v-btn>
        </v-col>

      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data () {
    return {
      name: '',
      brand: '',
      price: '',
      description: ''
    }
  },
  methods: {
    submit: function () {
      this.$emit('success')
    }
  }
}
</script>
