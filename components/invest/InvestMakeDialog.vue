<template>
  <div>
    <v-dialog v-model="dialog" fullscreen hide-overlay>
      <v-card class="secondary">
        <v-toolbar flat class="secondary">
          <v-btn icon @click="$emit('close-dialog')">
            <v-icon>mdi-arrow-left</v-icon>
          </v-btn>
          <v-toolbar-title>Symbol Chart</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-icon class="mr-2">mdi-bell</v-icon>
          <v-icon color="amber">mdi-star</v-icon>
        </v-toolbar>
        <v-list-item two-line>
          <v-list-item-avatar>
            <v-img src="/currency/4.jpg" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title>
              AAPL
              <v-icon small @click="showInformationDialog = true"
                >mdi-information-outline</v-icon
              ></v-list-item-title
            >
            <v-list-item-subtitle>
              Apple inc
            </v-list-item-subtitle>
            <v-list-item-subtitle
              >
              <v-icon small>mdi-clock</v-icon>
              <span class="grey--text" style="font-size:12px;'"
                >MARKET OPEN
              </span>
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action
            >$172.44<br />
            <span class="green--text">8.35%</span></v-list-item-action
          >
        </v-list-item>
        <v-tabs
          center-active
          centered
          v-model="tab"
          background-color="secondary"
          class="px-0 mx-0"
        >
          <v-tab
            href="#chart"
            style="font-size: 13px; min-width: 20px; max-width: 65px"
          >
            Chart
          </v-tab>
          <v-tab
            href="#news"
            style="font-size: 13px; min-width: 20px; max-width: 65px"
          >
            <v-badge color="red" dot> News </v-badge>
          </v-tab>
          <v-tab style="font-size: 13px; min-width: 20px; max-width: 85px"
            >Analysis</v-tab
          >
          <v-tab style="font-size: 13px; min-width: 20px; max-width: 85px"
            >Company</v-tab
          >
          <v-tabs-slider color="primary"></v-tabs-slider>
        </v-tabs>
        <v-tabs-items v-model="tab" class="background">
          <v-tab-item value="chart">
            <div>
              <div class="tradingview-widget-container">
                <div id="tradingview_2e912"></div>
              </div>
            </div>
            <div class="text-center my-5 mx-2" >
              <v-btn block text large class="blue" @click="
                  buyDialog = true;
                  typeDialog = 'sell';
                ">
                <v-icon>mdi-sync-alert</v-icon>
                TRADE
              </v-btn>
            </div>
          </v-tab-item>
          <v-tab-item value="news">
            <user-idias class="ma-2" />
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-dialog>
    <invest-information
      v-if="showInformationDialog"
      :dialog="showInformationDialog"
      @close-dialog="showInformationDialog = false"
    />
    <invest-buy
      v-if="buyDialog"
      :dialog="buyDialog"
      :type="typeDialog"
      @close-dialog="buyDialog = false"
    />
  </div>
</template>

<script>
import InvestBuy from "./InvestBuy.vue";
import InvestInformation from "./InvestInformation.vue";
export default {
  components: { InvestBuy, InvestInformation },
  props: {
    dialog: {
      required: true,
      type: Boolean,
    },
  },
  data() {
    return {
      tab: "chart",
      showInformationDialog: false,
      buyDialog: false,
      typeDialog: "sell",
    };
  },
  mounted() {
    new TradingView.widget({
      width: "100%",
      height: window.innerHeight - 260,
      symbol: "NASDAQ:AAPL",
      interval: "D",
      timezone: "Etc/UTC",
      theme: "dark",
      style: "1",
      locale: "en",
      toolbar_bg: "#f1f3f6",
      enable_publishing: false,
      allow_symbol_change: true,
      container_id: "tradingview_2e912",
    });
  },
};
</script>

<style>
</style>
