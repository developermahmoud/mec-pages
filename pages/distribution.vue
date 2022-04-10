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
              <th>
                <div style="width: 50px">إسم الشركة</div>
              </th>
              <th><div style="width: 80px">مبلغ التوزيع</div></th>
              <th>التوزيع %</th>
              <th>تاريخ التوزيع</th>
              <th>تاريخ الاستحقاق</th>
              <th>ملاحظة</th>
            </tr>
          </thead>
          <tbody>
            <template v-for="(item, i) in stocks">
              <tr :key="i" v-if="item.price">
                <td>
                  <div
                    class="d-flex"
                    style="cursor: pointer"
                    @click="showStockChart(item)"
                  >
                    <v-icon small class="ml-2">mdi-information-outline</v-icon>
                    <div>{{ item.name }}</div>
                  </div>
                  <div class="grey--text" style="font-size: 12px; width: 140px">
                    {{ item.code }}
                  </div>
                </td>
                <td>
                  <v-icon @click="showDialogPrices = true" small class="ml-2"
                    >mdi-information-outline</v-icon
                  >
                  {{ item.price.amount }}
                </td>
                <td>
                  <v-chip label small>{{ item.price.distribution.replace('%', '') }}%</v-chip>
                </td>
                <td>
                  {{ item.price.distribution_date }}
                </td>
                <td>
                  {{ item.price.due_date }}
                </td>
                <td>
                  {{ item.price.note }}
                </td>
              </tr>
            </template>
          </tbody>
        </template>
      </v-simple-table>
    </v-card>
    <charts-dialog
      v-if="showDialog"
      :dialog="showDialog"
      :stock="stock"
      :dates="dates"
      :series="series"
      @close-dialog="showDialog = false"
    />
    <v-dialog v-model="showDialogPrices" max-width="700">
      <v-card class="secondary">
        <v-card-text class="pt-5">
          <v-img src="/prices.jpeg" />
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
import ChartsDialog from "../components/charts/ChartsDialog.vue";
import InvestMakeDialog from "../components/invest/InvestMakeDialog.vue";
export default {
  components: { InvestMakeDialog, ChartsDialog },
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
      stock: {},
      stocks: [],
      dates: [],
      series: [],
      isLoading: true,
      showDialogPrices: false,
      showDialog: false,
      toggle_exclusive: null,
      makeDialog: false,
    };
  },
  mounted() {
    this.getStocks();
  },
  methods: {
    async showStockChart(item) {
      this.stock = item;
      this.dates = [];
      this.series = [];
      let i = 0;
      await this.$axios.$get(`frontend/stocks/${item.id}`).then((response) => {
        response.prices.map((item) => {
          this.dates.push(item.distribution_date);
            this.series.push(item.distribution.replace('%', ''));
          i++;
        });
        this.showDialog = true;
      });
    },
    async getStocks() {
      this.isLoading = true;
      await this.$axios.$get(`frontend/stocks`).then((response) => {
        this.stocks = response;
        this.isLoading = false;
      });
    },
  },
};
</script>

<style></style>
