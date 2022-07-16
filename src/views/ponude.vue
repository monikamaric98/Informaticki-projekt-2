<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-dialog
            v-model="addDialog"
            width="500"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
                color="pink"
                dark
                v-bind="attrs"
                v-on="on"
            >
              Dodaj novu sminku
            </v-btn>
          </template>

          <v-card>
            <v-card-title class="text-h5 grey lighten-2">
              Dodaj novu sminku
            </v-card-title>

            <v-card-text>
              <new-form @success="addDialog = false; successAlert=true;"></new-form>
            </v-card-text>

            <v-divider></v-divider>
          </v-card>
        </v-dialog>
      </v-col>
      <v-col cols="12">
        <v-alert type="success"
                 v-model="successAlert"
                 dismissible>
          Uspjesno spaseno.
        </v-alert>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Pretraži po brendu"
            single-line
            hide-details
            @keyup.enter="getData()"
            :loading="isLoading"
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
            v-model="category"
            append-icon="mdi-magnify"
            label="Pretraži po kategoriji"
            single-line
            hide-details
            :loading="isLoadingCategory"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col
          v-for="sminka in sminke.slice((this.page-1) * this.perPage, this.page * this.perPage)"
          :key="sminka.brand"
          cols="12"
          md="3"
          style="padding-bottom:65px"
      >
        <sminka :sminka="sminka"></sminka>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-pagination
            v-model="page"
            total-visible="10"
            :length="Math.ceil(totalSminke/perPage)"
        ></v-pagination>
      </v-col>
    </v-row>
  </v-container>
</template> 

<script>

import Sminka from "../components/Sminka";
import NewForm from "../components/NewForm";
export default {
  name: 'ponude',

  components: {
    NewForm,
    Sminka
  },

  data() {
    return {
      test: 'Testna varijabla',
      sminke: [],
      page: 1,
      totalSminke: 0,
      perPage: 12,
      search: 'maybelline',
      category: '',
      isLoading: false,
      isLoadingCategory: false,
      addDialog: false,
      successAlert: false
    }
  },

  created() {
    console.log('created')
    this.getData();
  },

  methods: {
    getData: function() {
      this.axios.get("http://makeup-api.herokuapp.com/api/v1/products.json",
          { 
        params: {
          //'offset': this.perPage * (this.page - 1),
          'brand': this.search,
          //'category': this.category
        }
      }).then((response) => {
        console.log(response.data)
        this.sminke = response.data
        this.totalSminke = response.data.length
        this.isLoading = false
        this.isLoadingCategory = false
      })
    },
    fetchEntriesDebounced() {
      clearTimeout(this._searchTimerId)
      this._searchTimerId = setTimeout(() => {
        this.getData()
      }, 500) 
    },
    searchEntries() {
      this.sminke = []
      this.page = 1
      this.fetchEntriesDebounced()
    }
  },

  watch: {
    page: function() {
      this.getData();
    },
    search (val) {
      if (!val) {
        return
      }
      this.isLoading = true
      this.searchEntries()
    },
    category (val) {
      if (!val) {
        return
      }
      this.isLoadingCategory = true
      this.searchEntries();
    }
  }
}
</script>
