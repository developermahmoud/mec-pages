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
      <v-btn class="secondaryBackground"> الرئيسيه </v-btn>
      <v-btn class="secondaryBackground"> الاسعار </v-btn>
      <v-btn class="secondaryBackground"> التوزيعات </v-btn>
      <v-btn class="secondaryBackground text-truncate"> التقويم<br />الشهرى</v-btn>
    </v-bottom-navigation>
  </div>
</template>

<script>
export default {
  data: () => ({ value: 0 }),
};
</script>

<style></style>
