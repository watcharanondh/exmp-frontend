<template>
  <v-container style="background:#D1DAE4;;height:100% ">
    <v-row>
      <v-col>
        <v-row class="justify-center">
          <v-card-title>
            <h2 class=" #2C3E50--text mt-7">Text fetch API</h2>
          </v-card-title>
        </v-row>
      </v-col>

      <v-col class="mt-2 ma-2" cols="12"> </v-col>
      <v-col class="justify-center">
        <v-row>
          <div class="d-flex flex-wrap justify-center">
            <v-card
              v-for="Pokemon in Pokemons"
              :key="Pokemon"
              color="#D1DAE4"
              class="ma-3"
              height="5%"
              width="15%"
              outlined
            >
              <v-col>
                <v-col>
                  <v-img
                    :src="Pokemon.sprites.front_default"
                    contain
                    height="200px"
                    width="200px"
                  >
                    <template v-slot:placeholder>
                      <v-sheet
                        color="#B3BDCD"
                        class="d-flex flex-wrap"
                      >
                        <v-skeleton-loader
                          class="mx-auto"
                          max-width="300"
                          type="card"
                        ></v-skeleton-loader>
                      </v-sheet>
                    </template>
                  </v-img>

                  <v-row>
                    <v-btn block depressed color="black" class="white--text">
                      {{ Pokemon.name }}
                    </v-btn>
                  </v-row>
                </v-col>
              </v-col>
            </v-card>
          </div>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    Pokemons: [],
    PokemonsID: 104,
  }),

  async mounted() {
    for (var i = 1; i <= this.PokemonsID; i++) {
      await axios
        .get(`https://pokeapi.co/api/v2/pokemon/${i}/`)
        .then((response) => {
          console.log("Name: ",response.data.name,"pic:",response.data.sprites.front_default);
          this.Pokemons.push(response.data);
        });
    }
  },
};
</script>

<style></style>
