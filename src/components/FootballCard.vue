<template>
  <v-card>
    <v-card-title>{{match.homeTeam.teamNameCH}} 對 {{match.awayTeam.teamNameCH}}</v-card-title>
    <v-card-text>
      <span>球賽編號： {{match.matchDay}}{{match.matchNum}}</span>
      <br>
      <span>預定截止投注時間： {{match.matchTime}}</span>
      <v-divider/>
      <v-container>
        <v-row>主客和</v-row>
        <v-row>
          <v-col xs4>
            <h3>{{match.homeTeam.teamNameCH}} (主隊勝)</h3>
          </v-col>

          <v-col xs4>
            <h3>和</h3>
          </v-col>

          <v-col xs4>
            <h3>{{match.awayTeam.teamNameCH}} (客隊勝)</h3>
          </v-col>
        </v-row>
        <v-row>
          <v-col xs4>
            <span>{{match.hadodds.H}}</span>
          </v-col>

          <v-col xs4>
            <span>{{match.hadodds.D}}</span>
          </v-col>

          <v-col xs4>
            <span>{{match.hadodds.A}}</span>
          </v-col>
        </v-row>
      </v-container>

      <v-divider/>
      <v-container>
        <v-row>入球大細</v-row>
        <v-row>
          <v-col xs4>
            <span>球數</span>
          </v-col>

          <v-col xs4>
            <span>大</span>
          </v-col>

          <v-col xs4>
            <span>細</span>
          </v-col>
        </v-row>
        <v-row v-for="f in orderedhilodds" :key="f.LINEORDER">
          <v-col xs4>
            <span>{{formattedLine(f.LINE)}}</span>
          </v-col>
          <v-col xs4>
            <span>{{f.H}}</span>
          </v-col>
          <v-col xs4>
            <span>{{f.L}}</span>
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
        <v-row v-for="f in orderedchlodds" :key="f.LINEORDER">
          <v-col xs4>
            <span>{{formattedLine(f.LINE)}}</span>
          </v-col>
          <v-col xs4>
            <span>{{f.H}}</span>
          </v-col>
          <v-col xs4>
            <span>{{f.L}}</span>
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
    this.match = {
      matchID: "071eb5ac-0857-462b-9897-1a7d4ca2a035",
      matchIDinofficial: "20190828WED1",
      matchNum: "1",
      matchDate: "2019-08-28+08:00",
      matchDay: "WED",
      coupon: {
        couponID: "5",
        couponShortName: "WED",
        couponNameCH: "周三賽事",
        couponNameEN: "Wednesday Matches"
      },
      league: {
        leagueID: "128",
        leagueShortName: "AFA",
        leagueNameCH: "澳洲足總盃",
        leagueNameEN: "Australian FA Cup"
      },
      homeTeam: {
        teamID: "1156",
        teamNameCH: "布里斯班獅吼",
        teamNameEN: "Brisbane Roar"
      },
      awayTeam: {
        teamID: "1153",
        teamNameCH: "中岸水手",
        teamNameEN: "Central Coast Mariners"
      },
      matchStatus: "Defined",
      matchTime: "2019-08-28T17:30:00+08:00",
      statuslastupdated: "2019-08-25T17:44:59+08:00",
      inplaydelay: "false",
      neutralgroundvenue: {
        neutralgroundvenueNameCH: "昆士蘭海豚體育場",
        neutralgroundvenueNameEN: "Dolphin Stadium, Queensland"
      },
      liveEvent: {
        ilcLiveDisplay: true,
        hasLiveInfo: false,
        isIncomplete: false,
        matchIDbetradar: "",
        matchstate: "BeforeKickOff",
        stateTS: "",
        liveevent: []
      },
      cornerresult: "",
      Cur: "1",
      hasWebTV: false,
      hadodds: {
        A: "100@4.40",
        D: "100@3.85",
        H: "100@1.57",
        ID: "5a84c4a4-c3ba-4210-8dac-d38e613a6b0a",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "true",
        ALLUP: "true",
        Cur: "1"
      },
      fhaodds: {
        H: "100@2.05",
        A: "100@4.55",
        D: "100@2.38",
        ID: "ffb0e794-dd7f-426d-8a21-520885604ce3",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      crsodds: {
        S0104: "100@80.00",
        S0303: "100@40.00",
        SM1MD: "100@100.0",
        S0401: "100@21.00",
        S0200: "100@8.50",
        S0204: "100@80.00",
        S0205: "100@250.0",
        S0502: "100@80.00",
        S0004: "100@120.0",
        SM1MH: "100@28.00",
        S0500: "100@50.00",
        S0102: "100@12.00",
        S0005: "100@400.0",
        S0202: "100@12.00",
        S0002: "100@25.00",
        S0302: "100@17.00",
        S0101: "100@8.00",
        S0000: "100@15.00",
        SM1MA: "100@80.00",
        S0201: "100@7.00",
        S0301: "100@11.00",
        S0001: "100@15.00",
        S0501: "100@50.00",
        S0400: "100@25.00",
        S0103: "100@30.00",
        S0003: "100@50.00",
        S0105: "100@250.0",
        S0203: "100@28.00",
        S0300: "100@13.00",
        S0402: "100@35.00",
        S0100: "100@8.25",
        ID: "45ade03e-218f-4849-bb0f-209d2aa715cb",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "true",
        ALLUP: "true",
        Cur: "1"
      },
      fcsodds: {
        S0501: "100@600.0",
        S0101: "100@6.50",
        S0102: "100@23.00",
        S0302: "100@120.0",
        S0104: "100@400.0",
        S0300: "100@22.00",
        S0303: "100@500.0",
        S0201: "100@13.00",
        S0005: "100@1000",
        S0205: "100@3000",
        S0202: "100@40.00",
        S0401: "100@150.0",
        S0502: "100@1000",
        S0103: "100@80.00",
        S0001: "100@6.50",
        S0301: "100@35.00",
        S0402: "100@400.0",
        S0000: "100@3.30",
        S0004: "100@400.0",
        SM1MH: "100@600.0",
        SM1MD: "100@5000",
        S0204: "100@700.0",
        S0105: "100@1000",
        S0002: "100@22.00",
        SM1MA: "100@1000",
        S0200: "100@7.50",
        S0400: "100@80.00",
        S0500: "100@400.0",
        S0003: "100@100.0",
        S0203: "100@200.0",
        S0100: "100@3.70",
        ID: "50a97dc7-ceb6-40d0-9de2-ab51565047cc",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      ftsodds: {
        A: "100@2.62",
        H: "100@1.47",
        N: "100@15.00",
        ID: "cec1a22c-8bd6-49d0-b201-3c8d2141ae1d",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      tqlodds: {
        A: "100@3.12",
        H: "100@1.31",
        ID: "cd500bd8-5e1e-4de8-a453-c84683f96ba0",
        POOLSTATUS: "Selling",
        ET: "1",
        INPLAY: "true",
        ALLUP: "false",
        Cur: "1"
      },
      ooeodds: {
        E: "100@1.80",
        O: "100@1.90",
        ID: "687c534d-0dee-4e42-b02e-522127b8710d",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      ttgodds: {
        M7: "100@18.00",
        P5: "100@7.25",
        P3: "100@3.65",
        P1: "100@5.70",
        P0: "100@15.00",
        P6: "100@13.00",
        P4: "100@4.80",
        P2: "100@3.80",
        ID: "cfcadff9-c8d1-4ef9-bde2-98a0f18bb055",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      hftodds: {
        AH: "100@18.00",
        HA: "100@30.00",
        DA: "100@10.00",
        DD: "100@6.20",
        HH: "100@2.55",
        DH: "100@4.65",
        AA: "100@7.00",
        HD: "100@13.00",
        AD: "100@13.00",
        ID: "3615771d-fb08-430c-9a7a-b30cc5c3de78",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      hhaodds: {
        H: "100@2.60",
        D: "100@3.45",
        A: "100@2.20",
        ID: "cf667f62-dc8c-401d-a35e-83825690b512",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        HG: "-1",
        AG: "+1",
        Cur: "1"
      },
      hdcodds: {
        A: "100@1.94",
        H: "100@1.82",
        ID: "dd9e3294-a4b6-4c6c-a591-0a832fe7e4e1",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        HG: "-0.5/-1.0",
        AG: "+0.5/+1.0",
        Cur: "1"
      },
      hilodds: {
        LINELIST: [
          {
            LINENUM: "2",
            MAINLINE: "true",
            LINESTATUS: "1",
            LINEORDER: "2",
            LINE: "2.5/2.5",
            L: "100@2.30",
            H: "100@1.54"
          },
          {
            LINENUM: "3",
            MAINLINE: "false",
            LINESTATUS: "1",
            LINEORDER: "3",
            LINE: "3.5/3.5",
            L: "100@1.46",
            H: "100@2.50"
          },
          {
            LINENUM: "1",
            MAINLINE: "false",
            LINESTATUS: "1",
            LINEORDER: "1",
            LINE: "2.5/3.0",
            H: "100@1.68",
            L: "100@2.05"
          }
        ],
        ID: "6249c4a2-cd73-4ab8-99a8-a5d1a6ef2c1e",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "true",
        ALLUP: "true",
        Cur: "1"
      },
      fhlodds: {
        LINELIST: [
          {
            LINENUM: "1",
            MAINLINE: "true",
            LINESTATUS: "1",
            LINEORDER: "1",
            LINE: "1.5/1.5",
            L: "100@1.57",
            H: "100@2.25"
          },
          {
            LINENUM: "2",
            MAINLINE: "false",
            LINESTATUS: "1",
            LINEORDER: "2",
            LINE: "1.0/1.5",
            L: "100@1.82",
            H: "100@1.88"
          },
          {
            LINENUM: "3",
            MAINLINE: "false",
            LINESTATUS: "1",
            LINEORDER: "3",
            LINE: "1.5/2.0",
            H: "100@2.78",
            L: "100@1.38"
          }
        ],
        ID: "7a85b6cc-569a-443c-8a72-3253f4b40422",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "false",
        ALLUP: "true",
        Cur: "1"
      },
      chlodds: {
        LINELIST: [
          {
            LINENUM: "1",
            MAINLINE: "true",
            LINESTATUS: "1",
            LINEORDER: "1",
            LINE: "10.5/10.5",
            H: "100@1.90",
            L: "100@1.80"
          },
          {
            LINENUM: "2",
            MAINLINE: "false",
            LINESTATUS: "1",
            LINEORDER: "2",
            LINE: "11.5/11.5",
            L: "100@1.52",
            H: "100@2.35"
          }
        ],
        ID: "af133a3d-cd2f-4824-90e5-d556153a2974",
        POOLSTATUS: "Selling",
        ET: "0",
        INPLAY: "true",
        ALLUP: "true",
        Cur: "1"
      },
      hasExtraTimePools: true,
      results: {},
      definedPools: [
        "HAD",
        "FHA",
        "CRS",
        "FCS",
        "FTS",
        "TQL",
        "OOE",
        "TTG",
        "HFT",
        "HHA",
        "HDC",
        "HIL",
        "FHL",
        "CHL",
        "NTS"
      ],
      inplayPools: ["HAD", "TQL", "HIL", "CHL", "CRS", "NTS"]
    };
  },
  methods: {
    formattedLine(val) {
      var arr = val.split("/");
      if (arr[0] == arr[1]) return arr[0];
      return val;
    }
  },
  computed: {
    orderedhilodds: function() {
      return this.match.hilodds.LINELIST.sort(function(x, y) {
        var a = eval(x.LINE.replace("/", "+"));
        var b = eval(y.LINE.replace("/", "+"));
        return parseInt(a) - parseInt(b);
      });
    },
    orderedchlodds: function() {
      return this.match.chlodds.LINELIST.sort(function(x, y) {
        var a = eval(x.LINE.replace("/", "+"));
        var b = eval(y.LINE.replace("/", "+"));
        return parseInt(a) - parseInt(b);
      });
    }
  }
};
</script>

<style lang="scss" scoped>
</style>