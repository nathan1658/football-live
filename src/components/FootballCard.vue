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
        <v-row v-for="f in orderedhilodds" >
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
            <span>角球數</span>
          </v-col>

          <v-col xs4>
            <span>大</span>
          </v-col>

          <v-col xs4>
            <span>細</span>
          </v-col>
        </v-row>
        <v-row v-for="f in orderedCHLodds" >
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
    // this.match = {
    //   $: {
    //     Date: "28/08",
    //     MatchDateTime: "28-08-2019 20:00",
    //     MLCKickOff: "1",
    //     MatchDay: "WED",
    //     MatchNum: "4",
    //     MatchID: "f701c5aa-c0e2-491a-af4e-b70650451e2b",
    //     MatchBDate: "28-08-2019",
    //     MatchPoolCloseTime: "20:00",
    //     MatchPoolCloseDate: "28/08",
    //     Enabled: "1",
    //     Inplay: "1",
    //     Opened: "0",
    //     League: "亞洲聯賽冠軍盃",
    //     Home: "FC廣州",
    //     Away: "鹿島鹿角",
    //     MatchAbandoned: "0",
    //     MatchConcluded: "0",
    //     InplayDelay: "0",
    //     FixedOddsPoolEnabled: "1",
    //     AllUpEnabled: "1"
    //   },
    //   Progress: [
    //     {
    //       $: {
    //         MatchProgress: "PENDING",
    //         Result: "0:0",
    //         ResultFull: "",
    //         Corner: "0",
    //         CornerFull: "0",
    //         UpdateDateTime: "",
    //         MatchProgressEx: "PENDING"
    //       }
    //     }
    //   ],
    //   TV: [
    //     {
    //       Channel: [
    //         { $: { Code: "671", NameEng: "NOW 671", NameChi: "NOW 671台" } },
    //         {
    //           $: { Code: "C652", NameEng: "i-CABLE 652", NameChi: "有線652台" }
    //         },
    //         {
    //           $: { Code: "C612", NameEng: "i-CABLE 612", NameChi: "有線612台" }
    //         },
    //         { $: { Code: "FOXP", NameEng: "FOX+", NameChi: "FOX+" } }
    //       ]
    //     }
    //   ],
    //   Pools: [
    //     {
    //       PoolInfo: [
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "HAD",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "1",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Odds: "4.70",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@4.70"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X",
    //                     Odds: "3.95",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "X@3.95"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Odds: "1.52",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@1.52"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "FHA",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Odds: "4.65",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@4.65"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X",
    //                     Odds: "2.35",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "X@2.35"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Odds: "2.05",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@2.05"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "HHA",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Odds: "2.30",
    //                     Enabled: "1",
    //                     Condition: "+1",
    //                     Value: "2@2.30"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X",
    //                     Odds: "3.45",
    //                     Enabled: "1",
    //                     Condition: "-1",
    //                     Value: "X@3.45"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Odds: "2.48",
    //                     Enabled: "1",
    //                     Condition: "-1",
    //                     Value: "1@2.48"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "HDC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Odds: "2.08",
    //                     Enabled: "1",
    //                     Condition: "+0.5/+1",
    //                     Value: "2@2.08"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Odds: "1.76",
    //                     Enabled: "1",
    //                     Condition: "-0.5/-1",
    //                     Value: "1@1.76"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "HIL",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "1",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { MainLine: "1" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.57",
    //                     Enabled: "1",
    //                     Condition: "2.5",
    //                     Value: "H@1.57"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "2.25",
    //                     Enabled: "1",
    //                     Condition: "2.5",
    //                     Value: "L@2.25"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { MainLine: "0" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.72",
    //                     Enabled: "1",
    //                     Condition: "2.5/3",
    //                     Value: "H@1.72"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "2.00",
    //                     Enabled: "1",
    //                     Condition: "2.5/3",
    //                     Value: "L@2.00"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { MainLine: "0" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "2.45",
    //                     Enabled: "1",
    //                     Condition: "3.5",
    //                     Value: "H@2.45"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "1.48",
    //                     Enabled: "1",
    //                     Condition: "3.5",
    //                     Value: "L@1.48"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "FHL",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { MainLine: "0" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.36",
    //                     Enabled: "1",
    //                     Condition: "0.5/1",
    //                     Value: "H@1.36"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "2.88",
    //                     Enabled: "1",
    //                     Condition: "0.5/1",
    //                     Value: "L@2.88"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { MainLine: "0" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.87",
    //                     Enabled: "1",
    //                     Condition: "1/1.5",
    //                     Value: "H@1.87"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "1.83",
    //                     Enabled: "1",
    //                     Condition: "1/1.5",
    //                     Value: "L@1.83"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { MainLine: "1" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "2.20",
    //                     Enabled: "1",
    //                     Condition: "1.5",
    //                     Value: "H@2.20"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "1.59",
    //                     Enabled: "1",
    //                     Condition: "1.5",
    //                     Value: "L@1.59"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "CHL",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "1",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { MainLine: "1" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.80",
    //                     Enabled: "1",
    //                     Condition: "9.5",
    //                     Value: "H@1.80"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "1.90",
    //                     Enabled: "1",
    //                     Condition: "9.5",
    //                     Value: "L@1.90"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { MainLine: "0" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "2.25",
    //                     Enabled: "1",
    //                     Condition: "10.5",
    //                     Value: "H@2.25"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "L",
    //                     Odds: "1.57",
    //                     Enabled: "1",
    //                     Condition: "10.5",
    //                     Value: "L@1.57"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "CRS",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "1",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { Tag: "H" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1:0",
    //                     Odds: "7.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:0@7.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:0",
    //                     Odds: "7.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:0@7.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:1",
    //                     Odds: "6.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:1@6.75"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:0",
    //                     Odds: "11.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:0@11.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:1",
    //                     Odds: "12.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:1@12.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:2",
    //                     Odds: "21.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:2@21.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:0",
    //                     Odds: "21.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:0@21.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:1",
    //                     Odds: "22.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:1@22.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:2",
    //                     Odds: "40.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:2@40.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:0",
    //                     Odds: "40.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:0@40.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:1",
    //                     Odds: "40.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:1@40.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:2",
    //                     Odds: "80.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:2@80.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "HO",
    //                     Odds: "28.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "HO@28.00"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "D" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "0:0",
    //                     Odds: "14.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:0@14.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:1",
    //                     Odds: "7.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:1@7.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:2",
    //                     Odds: "13.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:2@13.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:3",
    //                     Odds: "50.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:3@50.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "DO",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "DO@150.0"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "A" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "0:1",
    //                     Odds: "14.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:1@14.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:2",
    //                     Odds: "28.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:2@28.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:2",
    //                     Odds: "14.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:2@14.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:3",
    //                     Odds: "80.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:3@80.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:3",
    //                     Odds: "40.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:3@40.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:3",
    //                     Odds: "35.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:3@35.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:4",
    //                     Odds: "300.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:4@300.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:4",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:4@150.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:4",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:4@150.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:5",
    //                     Odds: "800.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:5@800.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:5",
    //                     Odds: "600.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:5@600.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:5",
    //                     Odds: "600.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:5@600.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "AO",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "AO@150.0"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "FCS",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { Tag: "H" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1:0",
    //                     Odds: "3.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:0@3.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:0",
    //                     Odds: "7.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:0@7.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:1",
    //                     Odds: "16.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:1@16.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:0",
    //                     Odds: "21.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:0@21.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:1",
    //                     Odds: "50.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:1@50.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:2",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:2@150.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:0",
    //                     Odds: "70.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:0@70.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:1",
    //                     Odds: "150.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:1@150.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4:2",
    //                     Odds: "500.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4:2@500.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:0",
    //                     Odds: "300.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:0@300.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:1",
    //                     Odds: "500.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:1@500.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5:2",
    //                     Odds: "1000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5:2@1000"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "HO",
    //                     Odds: "600.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "HO@600.0"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "D" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "0:0",
    //                     Odds: "2.95",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:0@2.95"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:1",
    //                     Odds: "6.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:1@6.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:2",
    //                     Odds: "60.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:2@60.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3:3",
    //                     Odds: "600.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3:3@600.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "DO",
    //                     Odds: "5000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "DO@5000"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "A" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "0:1",
    //                     Odds: "7.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:1@7.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:2",
    //                     Odds: "27.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:2@27.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:2",
    //                     Odds: "27.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:2@27.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:3",
    //                     Odds: "100.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:3@100.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:3",
    //                     Odds: "100.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:3@100.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:3",
    //                     Odds: "300.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:3@300.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:4",
    //                     Odds: "700.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:4@700.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:4",
    //                     Odds: "700.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:4@700.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:4",
    //                     Odds: "1000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:4@1000"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "0:5",
    //                     Odds: "4000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0:5@4000"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1:5",
    //                     Odds: "4000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1:5@4000"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2:5",
    //                     Odds: "5000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2:5@5000"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "AO",
    //                     Odds: "2000",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "AO@2000"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "FTS",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "A",
    //                     Odds: "2.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "A@2.75"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "H",
    //                     Odds: "1.44",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "H@1.44"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "N",
    //                     Odds: "14.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "N@14.00"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "TTG",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "0",
    //                     Odds: "14.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "0@14.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Odds: "5.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@5.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Odds: "3.80",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@3.80"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Odds: "3.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@3.75"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Odds: "5.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@5.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Odds: "7.25",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@7.25"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "6",
    //                     Odds: "12.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "6@12.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "7",
    //                     Odds: "19.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "7@19.00"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "OOE",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "E",
    //                     Odds: "1.80",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "E@1.80"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "O",
    //                     Odds: "1.90",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "O@1.90"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "HFT",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "1",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0"
    //           },
    //           OddsSet: [
    //             {
    //               $: { Tag: "H" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1-1",
    //                     Odds: "2.30",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1-1@2.30"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X-1",
    //                     Odds: "4.35",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "X-1@4.35"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2-1",
    //                     Odds: "22.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2-1@22.00"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "D" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1-X",
    //                     Odds: "15.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1-X@15.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X-X",
    //                     Odds: "6.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "X-X@6.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2-X",
    //                     Odds: "15.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2-X@15.00"
    //                   }
    //                 }
    //               ]
    //             },
    //             {
    //               $: { Tag: "A" },
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1-2",
    //                     Odds: "35.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1-2@35.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "X-2",
    //                     Odds: "10.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "X-2@10.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2-2",
    //                     Odds: "8.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2-2@8.75"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "SPC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             ByItem: "0"
    //           },
    //           OddsSet: [
    //             {
    //               Question: [
    //                 {
    //                   $: {
    //                     ItemNumber: "1",
    //                     Text: "那一件事會首先發生在 艾克森 (FC廣州) 身上?"
    //                   }
    //                 }
    //               ],
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Answer: "被罰黃牌",
    //                     Odds: "7.25",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@7.25"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Answer: "被罰紅牌",
    //                     Odds: "90.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@90.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Answer: "入球",
    //                     Odds: "2.10",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@2.10"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Answer: "被換出",
    //                     Odds: "5.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@5.75"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Answer: "上述事件沒有發生",
    //                     Odds: "2.28",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@2.28"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "SPC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             ByItem: "0"
    //           },
    //           OddsSet: [
    //             {
    //               Question: [
    //                 {
    //                   $: {
    //                     ItemNumber: "2",
    //                     Text: "那一件事會首先發生在 塔利斯卡 (FC廣州) 身上?"
    //                   }
    //                 }
    //               ],
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Answer: "被罰黃牌",
    //                     Odds: "5.25",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@5.25"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Answer: "被罰紅牌",
    //                     Odds: "100.0",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@100.0"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Answer: "入球",
    //                     Odds: "2.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@2.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Answer: "被換出",
    //                     Odds: "5.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@5.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Answer: "上述事件沒有發生",
    //                     Odds: "2.28",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@2.28"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "SPC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             ByItem: "0"
    //           },
    //           OddsSet: [
    //             {
    //               Question: [
    //                 {
    //                   $: {
    //                     ItemNumber: "3",
    //                     Text: "那一件事會首先發生在 荷西保連奴 (FC廣州) 身上?"
    //                   }
    //                 }
    //               ],
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Answer: "被罰黃牌",
    //                     Odds: "5.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@5.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Answer: "被罰紅牌",
    //                     Odds: "70.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@70.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Answer: "入球",
    //                     Odds: "2.45",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@2.45"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Answer: "被換出",
    //                     Odds: "9.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@9.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Answer: "上述事件沒有發生",
    //                     Odds: "1.96",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@1.96"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "SPC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             ByItem: "0"
    //           },
    //           OddsSet: [
    //             {
    //               Question: [
    //                 {
    //                   $: {
    //                     ItemNumber: "4",
    //                     Text: "那一件事會首先發生在 韋世豪 (FC廣州) 身上?"
    //                   }
    //                 }
    //               ],
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Answer: "被罰黃牌",
    //                     Odds: "5.75",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@5.75"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Answer: "被罰紅牌",
    //                     Odds: "80.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@80.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Answer: "入球",
    //                     Odds: "3.85",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@3.85"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Answer: "被換出",
    //                     Odds: "1.52",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@1.52"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Answer: "上述事件沒有發生",
    //                     Odds: "7.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@7.50"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "SPC",
    //             OddsUpdateTime: "12:00",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             ByItem: "0"
    //           },
    //           OddsSet: [
    //             {
    //               Question: [
    //                 {
    //                   $: {
    //                     ItemNumber: "5",
    //                     Text:
    //                       "那一件事會首先發生在 沙真奴安東尼奧 (鹿島鹿角) 身上?"
    //                   }
    //                 }
    //               ],
    //               OddsInfo: [
    //                 {
    //                   $: {
    //                     Number: "1",
    //                     Answer: "被罰黃牌",
    //                     Odds: "6.25",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "1@6.25"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "2",
    //                     Answer: "被罰紅牌",
    //                     Odds: "90.00",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "2@90.00"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "3",
    //                     Answer: "入球",
    //                     Odds: "3.40",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "3@3.40"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "4",
    //                     Answer: "被換出",
    //                     Odds: "6.50",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "4@6.50"
    //                   }
    //                 },
    //                 {
    //                   $: {
    //                     Number: "5",
    //                     Answer: "上述事件沒有發生",
    //                     Odds: "1.64",
    //                     Enabled: "1",
    //                     Condition: "",
    //                     Value: "5@1.64"
    //                   }
    //                 }
    //               ]
    //             }
    //           ]
    //         },
    //         {
    //           $: {
    //             Enabled: "1",
    //             Pool: "DHCP",
    //             OddsUpdateTime: "",
    //             StopSell: "28/08 20:00",
    //             AllUpFlag: "0",
    //             SingleFlag: "1",
    //             InPlayFlag: "0",
    //             InplayDelay: "0",
    //             HalfTimeFlag: "0",
    //             XT: "0",
    //             InvestmentTotal: "$396,525",
    //             JackpotGenerated: "$0"
    //           },
    //           LegInfo: [
    //             {
    //               $: {
    //                 Date: "28/08",
    //                 MatchDateTime: "28-08-2019 20:00",
    //                 MLCKickOff: "1",
    //                 MatchDay: "WED",
    //                 MatchNum: "4",
    //                 MatchID: "f701c5aa-c0e2-491a-af4e-b70650451e2b",
    //                 Inplay: "0",
    //                 Opened: "0",
    //                 League: "亞洲聯賽冠軍盃",
    //                 Home: "FC廣州",
    //                 Away: "鹿島鹿角",
    //                 MatchAbandoned: "0",
    //                 MatchConcluded: "0",
    //                 LegNo: "1",
    //                 MatchInplay: "1"
    //               },
    //               Progress: [
    //                 {
    //                   $: {
    //                     MatchProgress: "PENDING",
    //                     Result: "0:0",
    //                     UpdateDateTime: "",
    //                     MatchProgressEx: "PENDING"
    //                   }
    //                 }
    //               ],
    //               OddsSet: [
    //                 {
    //                   $: { Tag: "H" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "1:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "HO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "HO@"
    //                       }
    //                     }
    //                   ]
    //                 },
    //                 {
    //                   $: { Tag: "D" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "0:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "DO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "DO@"
    //                       }
    //                     }
    //                   ]
    //                 },
    //                 {
    //                   $: { Tag: "A" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "0:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "AO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "AO@"
    //                       }
    //                     }
    //                   ]
    //                 }
    //               ]
    //             },
    //             {
    //               $: {
    //                 Date: "29/08",
    //                 MatchDateTime: "29-08-2019 01:00",
    //                 MLCKickOff: "1",
    //                 MatchDay: "WED",
    //                 MatchNum: "5",
    //                 MatchID: "6a501e9b-d3f8-4d50-992c-82e8a46d45c8",
    //                 Inplay: "0",
    //                 Opened: "0",
    //                 League: "法國甲組聯賽",
    //                 Home: "里爾",
    //                 Away: "聖伊天",
    //                 MatchAbandoned: "0",
    //                 MatchConcluded: "0",
    //                 LegNo: "2",
    //                 MatchInplay: "1"
    //               },
    //               Progress: [
    //                 {
    //                   $: {
    //                     MatchProgress: "PENDING",
    //                     Result: "0:0",
    //                     UpdateDateTime: "",
    //                     MatchProgressEx: "PENDING"
    //                   }
    //                 }
    //               ],
    //               OddsSet: [
    //                 {
    //                   $: { Tag: "H" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "1:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "4:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "4:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "5:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "5:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "HO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "HO@"
    //                       }
    //                     }
    //                   ]
    //                 },
    //                 {
    //                   $: { Tag: "D" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "0:0",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:0@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "3:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "3:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "DO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "DO@"
    //                       }
    //                     }
    //                   ]
    //                 },
    //                 {
    //                   $: { Tag: "A" },
    //                   OddsInfo: [
    //                     {
    //                       $: {
    //                         Number: "0:1",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:1@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "0:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "0:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:2",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:2@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "1:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "1:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:3",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:3@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:4",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:4@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "2:5",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "2:5@"
    //                       }
    //                     },
    //                     {
    //                       $: {
    //                         Number: "AO",
    //                         Odds: "",
    //                         Enabled: "1",
    //                         Condition: "",
    //                         Value: "AO@"
    //                       }
    //                     }
    //                   ]
    //                 }
    //               ]
    //             }
    //           ]
    //         }
    //       ]
    //     }
    //   ]
    // };
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