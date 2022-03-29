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
              <th><div style="width: 50px">مبلغ التوزيع</div></th>
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
                  <v-icon small class="ml-2">mdi-information-outline</v-icon>
                  <div> {{ item.name }}</div>
                </div>
              </td>
              <td>
                {{ item.amount }} <v-icon @click="showDialogPrices=true" small class="ml-2">mdi-information-outline</v-icon>
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
      showDialogPrices: false,
      showDialog: false,
      toggle_exclusive: null,
      makeDialog: false,
      items: [
        {
          name: "طيبة",
          code: "4090",
          subtitle: "Bitcoin vs US Dollar ",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.25",
        },
        {
          name: "اسمنت  نجران",
          code: "3002",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت المدينة",
          code: "3003",
          subtitle: "Bitcoin vs US Dollar ",
          color: "red",
          change: "0.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "شهرى",
          amount: "0.25",
        },
        {
          name: "اسمنت العربية",
          code: "3010",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت الشرقية",
          code: "3080",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "المراكز  العربية",
          code: "4321",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت السعودية",
          code: "3030",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت ينبع",
          code: "3060",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "التعمير  ",
          code: "4150",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "البحري",
          code: "4030",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت حائل",
          code: "3001",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "سافكو",
          code: "2020",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "المملكة",
          code: "4280",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "االتايفات",
          code: "4081",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "سيكيم ",
          code: "2310",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "اسمنت القصيم",
          code: "3040",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
        {
          name: "مهارة الموارد  البشرية ",
          code: "1831",
          subtitle: "Gold vs US Dollar ",
          color: "green",
          change: "10.5%",
          date: "12/02/2022",
          date_dist: "12/02/2022",
          notes: "سنوى",
          amount: "0.87",
        },
      ],
    };
  },
};
</script>

<style></style>
