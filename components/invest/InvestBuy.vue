<template>
  <div>
    <v-dialog v-model="dialog" fullscreen hide-overlay>
      <v-card class="secondary">
        <v-toolbar flat class="secondary">
          <v-btn icon @click="$emit('close-dialog')">
            <v-icon>mdi-arrow-left</v-icon>
          </v-btn>
          <v-toolbar-title>New Order</v-toolbar-title>
        </v-toolbar>
        <v-divider></v-divider>
        <v-list-item three-line>
          <v-list-item-avatar>
            <v-img src="/currency/4.jpg" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title> Apple </v-list-item-title>
            <v-list-item-subtitle>
              <v-chip-group v-model="typeChip" active-class="green" mandatory>
                <v-chip value="cfd" outlined x-small>CFD</v-chip>
                <v-chip value="real" outlined x-small>REAL</v-chip>
              </v-chip-group>
            </v-list-item-subtitle>
            <v-list-item-subtitle>
              <v-icon small>mdi-clock</v-icon>
              <span class="grey--text" style="font-size:12px;'"
                >MARKET OPEN</span
              >
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action
            >$172.44<br />
            <span class="green--text">8.35%</span></v-list-item-action
          >
        </v-list-item>
        <v-alert class="mx-2" color="info" dense text v-if="typeChip == 'cfd'">
          <v-icon color="info" size="20">mdi-alert-box</v-icon> This symbol is a
          CFD.
        </v-alert>
        <v-alert class="mx-2" color="info" dense text v-else>
          <v-icon color="info" size="20">mdi-alert-box</v-icon> This symbol is a
          Real Stock.
        </v-alert>
        <v-card-text>
          <div class="d-flex justify-space-between pa-1 background rounded-lg">
            <div style="width: 50%">
              <v-btn
                small
                text
                block
                @click="topChange = 'current_price'"
                :class="topChange == 'current_price' ? 'secondary' : ''"
                >Market Price
              </v-btn>
            </div>
            <div style="width: 50%">
              <v-btn
                small
                text
                block
                @click="topChange = 'specefic_rate'"
                :class="topChange == 'specefic_rate' ? 'secondary' : ''"
                >Specfic Price</v-btn
              >
            </div>
          </div>
          <div class="mt-5">
            <div class="text-center">
              <v-menu offset-y>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn text v-bind="attrs" v-on="on">
                    {{ wordValue }}
                    <v-icon>mdi-chevron-down</v-icon>
                  </v-btn>
                </template>
                <v-list class="py-0 secondary" dense>
                  <v-list-item
                    @click="
                      wordValue = 'Value';
                      valuePrefix = '$';
                    "
                  >
                    <v-list-item-title>Value</v-list-item-title>
                  </v-list-item>
                  <v-list-item
                    @click="
                      wordValue = 'Position size';
                      valuePrefix = '';
                    "
                  >
                    <v-list-item-title>Position size</v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
            </div>
            <div class="d-flex justify-space-between align-center">
              <v-icon @click="autoFocus()">mdi-cash-multiple</v-icon>
              <div class="text-center">
                <v-text-field
                  type="number"
                  id="simplePrice"
                  dense
                  hide-details
                  single-line
                  class="mx-auto"
                  style="width: 60px; font-size: 25px; text-align: center"
                  :prefix="valuePrefix"
                  v-model="priceInEuru"
                ></v-text-field>
                <div>~0.0268 {{wordValue == 'Value' ?  'size' : '$'}}</div>
              </div>
              <v-icon @click="autoFocus()">mdi-dialpad</v-icon>
            </div>
            <v-slider max="250" min="-0" hide-details v-model="priceInEuru">
            </v-slider>
          </div>
          <v-text-field
            class="mt-2"
            v-if="topChange === 'specefic_rate'"
            value="178.85"
            dense
            label="Entry price"
            type="number"
          ></v-text-field>
          <div style="font-size: 12px">
            <v-icon size="16" class="mr-1">mdi-wallet</v-icon>Available funds:
            <span class="green--text">7650,5555$</span>
          </div>
          <div class="d-flex align-center">
            <v-switch dense v-model="showDetails"></v-switch
            ><img style="width: 20px" src="/Terminal.ico" /> HOB Protector
          </div>
          <template v-if="showDetails">
            <div
              class="d-flex justify-space-between pa-1 background rounded-lg"
            >
              <div style="width: 50%">
                <v-btn
                  small
                  block
                  text
                  @click="otherChange = 'amount'"
                  :class="otherChange == 'amount' ? 'secondary' : ''"
                  >Amount
                </v-btn>
              </div>
              <div style="width: 50%">
                <v-btn
                  small
                  block
                  text
                  @click="otherChange = 'specefic_rate'"
                  :class="otherChange == 'specefic_rate' ? 'secondary' : ''"
                  >Specfic Price
                </v-btn>
              </div>
            </div>
            <div class="d-flex justify-space-between align-center mt-3">
              <div style="width: 48%">
                <v-text-field
                  type="number"
                  dense
                  hide-details
                  :prefix="otherChange == 'amount' ?'$':''"
                  :value="otherChange == 'amount' ? '-8.63' : '0.00'"
                >
                  <template v-slot:label>
                    <strong class="red--text body-1">Stop Loss</strong>
                  </template>
                </v-text-field>
              </div>
              <div style="width: 48%">
                <v-text-field
                  type="number"
                  dense
                  hide-details
                  :prefix="otherChange == 'amount' ?'$':''"
                  :value="otherChange == 'amount' ? '8.63' : '0.00'"
                >
                  <template v-slot:label>
                    <strong class="green--text body-1">Take Profit</strong>
                  </template>
                </v-text-field>
              </div>
            </div>
            <div class="d-flex justify-space-between align-center">
              <div>
                <template v-if="otherChange == 'amount'">181.27</template>
                <template v-else>$ 8.63</template>
              </div>
              <div>
                <template v-if="otherChange == 'amount'">164.01</template>
                <template v-else>$ -8.63</template>
              </div>
            </div>
          </template>
        </v-card-text>
        <v-alert class="mx-4 pa-1" color="warning" dense text>
          <div class="d-flex">
            <v-icon class="ml-0 pl-0" color="warning">mdi-exclamation</v-icon>
            <p style="font-size: 12px">
              Attention! The trade will be executed at market conditions,
              difference with requested price may be significant!
            </p>
          </div>
        </v-alert>
        <div class="d-flex my-5 mx-3">
          <template v-if="typeChip == 'cfd'">
            <div style="width: 50%">
              <v-btn text tile block class="red" to="/order?page=invest"
                >sell</v-btn
              >
            </div>
            <div style="width: 50%">
              <v-btn text tile block class="green" to="/order?page=invest"
                >buy</v-btn
              >
            </div>
          </template>
          <template v-else>
            <div style="width: 100%">
              <v-btn text tile block class="green" to="/order?page=invest"
                >buy</v-btn
              >
            </div>
          </template>
        </div>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    dialog: {
      required: true,
      type: Boolean,
    },
    type: {
      required: true,
      type: String,
    },
  },
  data() {
    return {
      valuePrefix: "$",
      wordValue: "Value",
      priceInEuru: 100,
      typeChip: "cfd",
      showDetails: false,
      orderedDialog: false,
      action: "buy",
      topChange: "current_price",
      otherChange: "amount",
      toggle_none: null,
    };
  },
  mounted() {
    this.action = this.type;
  },
  methods: {
    autoFocus() {
      document.getElementById("simplePrice").focus();
    },
  },
};
</script>

<style>
</style>
