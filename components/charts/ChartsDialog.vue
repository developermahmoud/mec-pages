<template>
  <div>
    <v-dialog
      v-model="dialog"
      max-width="700"
      @click:outside="$emit('close-dialog')"
    >
      <v-card class="secondary">
        <v-card-title>
          {{ stock.name }}
          <v-spacer></v-spacer>
          {{ stock.price.distribution_date }}
        </v-card-title>
        <v-card-text class="showShart pt-5">
          <v-chart class="chart" :style="`width:640px`" :option="option" />
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { BarChart } from "echarts/charts";
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
} from "echarts/components";
import VChart, { THEME_KEY } from "vue-echarts";
use([
  CanvasRenderer,
  BarChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
]);

use([
  CanvasRenderer,
  BarChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
]);
export default {
  components: {
    VChart,
  },
  provide: {
    [THEME_KEY]: "dark",
  },
  props: {
    dialog: {
      required: true,
      type: Boolean,
    },
    stock: {
      required: true,
      type: Object,
    },
    dates: {
      required: true,
      type: Array,
    },
    series: {
      required: true,
      type: Array,
    },
  },
  data() {
    return {
      width: 300,
      option: {
        backgroundColor: "rgba(0, 0, 200, 0.0)",
        xAxis: {
          type: "category",
          data: this.dates,
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            data: this.series,
            type: "bar",
            barWidth: "30%",
            backgroundStyle: {
              color: "rgba(180, 180, 180, 0.2)",
            },
          },
        ],
      },
    };
  },
  mounted() {
    let box = document.querySelector(".showShart");
    this.width = box.offsetWidth;
  },
};
</script>

<style>
.chart {
  width: 500px;
  height: 300px;
}
</style>
