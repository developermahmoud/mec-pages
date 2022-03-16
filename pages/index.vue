<template>
  <div>
    <v-card class="secondary" flat tile>
      <v-card-text class="text-center">
        <v-text-field
          outlined
          prepend-inner-icon="mdi-magnify"
          placeholder="بحث"
          dense
          filled
        ></v-text-field>
        <v-slide-group mandatory v-model="toggle_exclusive">
          <v-slide-item class="mr-2" v-slot="{ active, toggle }">
            <v-btn
              :input-value="active"
              active-class="primary"
              @click="toggle"
              small
              outlined
              >توزيع شهرى
            </v-btn>
          </v-slide-item>
          <v-slide-item class="mr-2" v-slot="{ active, toggle }">
            <v-btn
              :input-value="active"
              active-class="primary"
              @click="toggle"
              small
              outlined
            >
              ربع سنوى
            </v-btn>
          </v-slide-item>
          <v-slide-item class="mr-2" v-slot="{ active, toggle }">
            <v-btn
              :input-value="active"
              active-class="primary"
              @click="toggle"
              small
              outlined
            >
              نصف سنوى
            </v-btn>
          </v-slide-item>
          <v-slide-item class="mr-2" v-slot="{ active, toggle }">
            <v-btn
              :input-value="active"
              active-class="primary"
              @click="toggle"
              small
              outlined
              >سنوى
            </v-btn>
          </v-slide-item>
        </v-slide-group>
      </v-card-text>
      <v-simple-table class="secondary">
        <template v-slot:default>
          <thead>
            <tr>
              <th>إسم الشركة</th>
               <th><div style="width:50px;">مبلغ التوزيع</div></th>
              <th>التوزيع %</th>
              <th>تاريخ التوزيع</th>
              <th>تاريخ الاستحقاق</th>
              <th>ملاحظة</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, i) in items" :key="i">
              <td>
                <div
                  class="d-flex"
                  style="cursor: pointer"
                  @click="showDialog = true"
                >
                  <img
                    :src="item.icon"
                    style="width: 18px; height: 18px"
                    class="ml-2"
                  />
                  <div>{{ item.name }}</div>
                </div>
                <div class="grey--text" style="font-size: 12px; width: 140px">
                  {{ item.subtitle }}
                </div>
              </td>
              <td>
                {{ item.amount }}
              </td>
              <td>
                <v-chip label x-small style="width: 57px" :class="item.color">{{
                  item.change
                }}</v-chip>
              </td>
              <td>
                {{ item.date }}
              </td>
              <td>
                {{ item.date_dist }}
              </td>
              <td>
                {{ item.notes }}
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
    <v-dialog v-model="showDialog" max-width="700">
      <v-card class="secondary">
        <v-card-text class="pt-5">
          <v-img src="/chart.jpeg" />
        </v-card-text>
      </v-card>
    </v-dialog>
    <invest-make-dialog
      v-if="makeDialog"
      :dialog="makeDialog"
      @close-dialog="makeDialog = false"
    />
  </div>
</template>

<script>
import InvestMakeDialog from "../components/invest/InvestMakeDialog.vue";
export default {
  components: { InvestMakeDialog },
  head() {
    return {
      script: [
        {
          src: "https://s3.tradingview.com/tv.js",
        },
      ],
    };
  },
  data() {
    return {
      showDialog: false,
      toggle_exclusive: null,
      makeDialog: false,
      items: [
        {
          icon: "/currency/1.png",
          name: "BTC",
          subtitle: "Bitcoin vs US Dollar ",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.25",
        },
        {
          icon: "/currency/usdc.svg",
          name: "XAU/USD",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          icon: "/currency/3.png",
          name: "SOL",
          subtitle: "Solana Token vs US Dollar ",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "نصف سنوى",
          amount: "0.02",
        },
        {
          icon: "/currency/4.jpg",
          name: "AAPL",
          subtitle: "Apple inc.",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "نصف سنوى",
          amount: "0.29",
        },
        {
          icon: "/currency/4.png",
          name: "EUR/USD",
          subtitle: "Euro vs US Dollar",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.85",
        },
        {
          icon: "/currency/eth.svg",
          name: "ETH",
          subtitle: "Ethereum vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "نصف سنوى",
          amount: "0.36",
        },
        {
          icon: "/opengraph.png",
          name: "AMZN",
          subtitle: "AMZN vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.45",
        },
        {
          icon: "/currency/oil.jpg",
          name: "Oil",
          subtitle: "Oil vs US Dollar",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.2",
        },
        {
          icon: "/currency/gold.jpeg",
          name: "Gold",
          subtitle: "Gold vs US Dollar",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "نصف سنوى",
          amount: "0.22",
        },
        {
          icon: "/currency/silver.jpg",
          name: "Silver",
          subtitle: "Silver vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.25",
        },
        {
          icon: "/currency/fb.png",
          name: "FB",
          subtitle: "FB vs US Dollar",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.24",
        },
        {
          icon: "/currency/TWTR.png",
          name: "TWTR",
          subtitle: "TWTR vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "نصف سنوى",
          amount: "0.31",
        },
        {
          icon: "/currency/tesla--600.png",
          name: "TSLA",
          subtitle: "TSLA vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.20",
        },
        {
          icon: "/currency/symbol-Ripple.jpg",
          name: "Ripple XRP",
          subtitle: "Ripple XRP  vs US Dollar",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          amount: "0.20",
          notes: "شهرى",
        },
        {
          icon: "/currency/150x150.png",
          name: "SPY. ETF",
          subtitle: "SPY. ETF vs US Dollar",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.25",
        },
      ],
    };
  },
};
</script>

<style></style>
