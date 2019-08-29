<template>
  <v-card min-width="500" class="ma-5">
    <v-card-title>{{match.$.Home}} 對 {{match.$.Away}}</v-card-title>
    <v-card-text>
      <span>球賽編號： {{match.$.MatchDay}}{{match.$.MatchNum}}</span>
      <br>
      <span>預定截止投注時間： {{match.$.MatchDateTime}}</span>
      <v-divider/>
      <v-container>
        <v-row>主客和</v-row>
        <v-row>
          <v-col xs4>
            <h3>{{match.$.Home}} (主隊勝)</h3>
          </v-col>

          <v-col xs4>
            <h3>和</h3>
          </v-col>

          <v-col xs4>
            <h3>{{match.$.Away}} (客隊勝)</h3>
          </v-col>
        </v-row>
        <v-row>
          <v-col xs4>
            <span>{{getTargetOddsInfo("HAD").OddsSet[0].OddsInfo[2].$.Value}}</span>
          </v-col>

          <v-col xs4>
            <span>{{getTargetOddsInfo("HAD").OddsSet[0].OddsInfo[1].$.Value}}</span>
          </v-col>

          <v-col xs4>
            <span>{{getTargetOddsInfo("HAD").OddsSet[0].OddsInfo[0].$.Value}}</span>
          </v-col>
        </v-row>
      </v-container>


     <v-divider/>
      <v-container>
        <v-row>入球大細</v-row>
        <v-row>
          <v-col xs4>
            <h3>球數</h3>
          </v-col>

          <v-col xs4>
            <h3>大</h3>
          </v-col>

          <v-col xs4>
            <h3>細</h3>
          </v-col>
        </v-row>
        <v-row v-for="f in orderedhilodds" :key="f.OddsInfo[0].$.Condition">
          <v-col xs4>
            <span>{{f.OddsInfo[0].$.Condition}}</span>
          </v-col>

          <v-col xs4>
            <span>{{f.OddsInfo[0].$.Odds}}</span>
            
          </v-col>

          <v-col xs4>
            <span>{{f.OddsInfo[1].$.Odds}}</span>
            
          </v-col>
        </v-row>
      </v-container>

 <v-divider/>

      <v-container>
        <v-row>角球大細</v-row>
        <v-row>
          <v-col xs4>
            <h3>角球數</h3>
          </v-col>

          <v-col xs4>
            <h3>大</h3>
          </v-col>

          <v-col xs4>
            <h3>細</h3>
          </v-col>
        </v-row>
        <v-row v-for="f in orderedCHLodds" :key="f.OddsInfo[0].$.Condition">
          <v-col xs4>
            <span>{{f.OddsInfo[0].$.Condition}}</span>
          </v-col>
          <v-col xs4>
            <span>{{f.OddsInfo[0].$.Odds}}</span>
 
          </v-col>
          <v-col xs4>
            <span>{{f.OddsInfo[1].$.Odds}}</span>
            
          </v-col>
        </v-row>
      </v-container>
     
      <v-divider/>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: {
    match: Object
  },
  created: function() {
   
  },
  methods: {
    formattedLine(val) {
      var arr = val.split("/");
      if (arr[0] == arr[1]) return arr[0];
      return val;
    },
    getTargetOddsInfo(val) {
      return this.match.Pools[0].PoolInfo.filter(function(x) {
        return x.$.Pool == val;
      })[0];
    }
  },
  computed: {
    orderedhilodds: function() {
      return this.getTargetOddsInfo("HIL").OddsSet.sort(function(x, y) {
        var a = eval(x.OddsInfo[0].$.Condition.split('/')[0]);
        var b = eval(y.OddsInfo[0].$.Condition.split('/')[0]);
        return parseInt(a) - parseInt(b);
      });
    },
    orderedCHLodds: function() {
      var result= this.getTargetOddsInfo("CHL").OddsSet.sort(function(x, y) {
        var a = eval(x.OddsInfo[0].$.Condition.split('/')[0]);
        var b = eval(y.OddsInfo[0].$.Condition.split('/')[0]);
        return parseInt(a) - parseInt(b);
      });
      return result;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>