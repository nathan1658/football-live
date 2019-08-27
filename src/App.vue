<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text href="https://github.com/vuetifyjs/vuetify/releases/latest" target="_blank">
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <v-row :align="start">
          <FootballCard   v-for="match in matches" :key="match.matchId" :match="match"/>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import FootballCard from "./components/FootballCard";

export default {
  name: "App",
  components: {
    FootballCard
  },
  data: () => ({
    matches: [
      {
        matchId: 12,
        home: "home1",
        away: "away1"
      },
      {
        matchId: 13,
        home: "home2",
        away: "away2"
      }
    ]
  })
};
</script>
