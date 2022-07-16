<template>
  <div id="home">
    <h1>Ovo je početna stranica</h1>

    <p class="my-5">
      Napravili smo Book-explorer aplikaciju koja služi pretraživanje bestsellera.
      <br>
      <span class="grey--text"><em>"I do believe something very magical can happen when you read a good book" - J. K. Rowling</em></span>
      <br>
      Pronađite knjigu koje Vam najviše odgovara i u kojoj ćete definitivno uživati.
    </p>

    <router-link to="/explore" class="mr-3 router-link">
      <v-btn class="red darken-4">
        <v-icon class="mr-2">mdi-book</v-icon>
        Pretraži</v-btn>
    </router-link>

    <!-- mock modal -->
    <v-dialog
      v-model="dialog"
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="green"
          dark
          v-bind="attrs"
          v-on="on"
          outlined
        >
          <v-icon class="mr-2">mdi-plus</v-icon>
          Dodaj novu knjigu
        </v-btn>
      </template>
      <v-card>
        <v-card-text>
          <v-card-title>Dodaj svoju knjigu!</v-card-title>

          <v-container>
            <v-text-field
              label="Naslov"
              required
            ></v-text-field>
            
            <v-text-field
              label="Autor"
              required
            ></v-text-field>
            
            <v-text-field
              label="Izdavač"
              required
            ></v-text-field>
            
            <v-row>
              <v-col
                cols="12"
                sm="6"
              >
                <v-select
                  :items="['Fiction', 'Romance', 'Adventure', 'Drama', 'Autobiography']"
                  label="Žanr"
                  required
                ></v-select>
              </v-col>
              <v-col
                cols="12"
                sm="6"
              >
                <v-select
                  :items="['2021', '2020', '2019', '2018', '2017']"
                  label="Godina izdanja"
                  required
                ></v-select>
              </v-col>
            </v-row>
          
            <small>Provjerite unesene podatke!</small>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="red darken-4"
            text
            @click="dialog = false"
          >
            Odustani
          </v-btn>
          <v-btn
            color="green"
            text
            @click="dialog = false"
          >
            Dodaj
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- alert action -->
    <v-btn
      dark
      outlined
      color="blue lighten-1"
      class="ml-3"
      @click="snackbar = true"
    >
      <v-icon class="mr-2">mdi-reload</v-icon>
      Ponovno učitaj stranicu
    </v-btn>
    <v-snackbar
      v-model="snackbar"
      :timeout="3000"
    >
      Stranica osvježena!

      <template v-slot:action="{ attrs }">
        <v-btn
          color="blue"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Zatvori
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
export default {
  name: 'Home',

  data(){
    return {
      dialog: false,
      snackbar: false,
    }
  }
}
</script>

<style scoped>
.router-link {
  text-decoration: none;
}
</style>