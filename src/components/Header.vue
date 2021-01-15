<template>
  <v-card>
    <v-app-bar app flat color="#718096" prominent>
      <v-col>
        <v-col>
          <v-row></v-row>
        </v-col>
        <v-row justify="center">
          <v-toolbar-title
            ><h1 class="white--text">Test Fontend</h1></v-toolbar-title
          >
        </v-row>
        <v-col>
          <v-row></v-row>
        </v-col>
      </v-col>
      <template v-slot:extension>
            <v-tabs
              centered
              class="ml-n9 "
              color="green"
              background-color="#FFFFFF"
            >
              <v-tab
                v-for="link in links"
                :key="link.text"
                router
                :to="link.route"
              >
                <h2>{{ link.text }}</h2>
              </v-tab>
            </v-tabs>
    
      </template>
    </v-app-bar>
  </v-card>
</template>

<script>
export default {
  name: "Header",
  data: () => ({
    links: [
      { text: "Home", route: "/Home" },
      { text: "Pokemon", route: "/Pokemon" },
      { text: "Function1", route: "/Function1" },
      { text: "Function2", route: "/Function2" },
      { text: "Function3", route: "/Function3" },
    ],
  }),
};
</script>

<style></style>
