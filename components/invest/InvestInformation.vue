<template>
  <div>
    <v-dialog v-model="dialog" fullscreen hide-overlay>
      <v-card class="secondary">
        <v-toolbar flat class="secondary">
          <v-btn icon @click="$emit('close-dialog')">
            <v-icon>mdi-arrow-left</v-icon>
          </v-btn>
          <v-toolbar-title>Apple info</v-toolbar-title>
        </v-toolbar>
        <v-divider></v-divider>
        <v-card-text class="px-2">
          <v-simple-table class="secondary">
            <template v-slot:default>
              <thead>
                <tr>
                  <th colspan="2">QUOTES SESSIONS</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>Sunday</td>
                  <td></td>
                </tr>
                 <tr>
                  <td>Monday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Tuesday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Wednesday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Thurasday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Friday</td>
                 <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Saturday</td>
                  <td>14:30-21:00</td>
                </tr>
              </tbody>
              <thead>
                <tr>
                  <th colspan="2">TRADES SESSIONS</th>
                </tr>
              </thead>
               <tbody>
                <tr>
                  <td>Sunday</td>
                  <td></td>
                </tr>
                 <tr>
                  <td>Monday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Tuesday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Wednesday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Thurasday</td>
                  <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Friday</td>
                 <td>14:30-21:00</td>
                </tr>
                 <tr>
                  <td>Saturday</td>
                  <td>14:30-21:00</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card-text>
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
  },
};
</script>

<style>
</style>