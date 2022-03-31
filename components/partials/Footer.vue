<template>
  <div>
    <v-bottom-navigation
      app
      fixed
      grow
      :value="value"
      height="58"
      color="primary"
      class="secondaryBackground"
    >
      <v-btn height="58" class="secondaryBackground" link to="/">
        <span style="font-size: 12px; line-height: 2">الرئيسية</span>
        <img
          style="width: 25px"
          src="/Golden-Logo.png"
        />
      </v-btn>
      <v-btn height="58" class="secondaryBackground" link to="/prices">
        <span style="font-size: 12px; line-height: 2">الحقيبة</span>
        <v-icon size="25">fa-chart-line</v-icon>
      </v-btn>

      <v-btn height="58" class="secondaryBackground" link to="/distribution">
        <span style="font-size: 12px; line-height: 2">التوزيعات</span>
        <v-icon size="25">mdi-table-network</v-icon>
      </v-btn>
      <v-btn height="58" class="secondaryBackground" link to="/calendar">
        <span style="font-size: 12px; line-height: 2">التقويم الشهري</span>
        <v-icon size="25">mdi-calendar</v-icon>
      </v-btn>
    </v-bottom-navigation>
  </div>
</template>

<script>
export default {
  data: () => ({ value: 0 }),
};
</script>

<style></style>
