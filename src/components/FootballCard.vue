<template>
  <v-card >
    <v-card-title>{{match.home}} 對 {{match.away}}</v-card-title>
    <v-card-text>
      <v-container>
      <v-row> 主客和 </v-row>
        <v-row>
          <v-col xs6>
            <h3>南鍚(主隊勝)</h3>
            2.12
          </v-col>
          <v-col xs6>2</v-col>
        </v-row>
      </v-container>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: {
    match: Object
  }
};
</script>

<style lang="scss" scoped>
</style>