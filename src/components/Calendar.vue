<script>
import Vue from "vue";
import { DateTime } from "luxon";
import CalendarMonth from "./CalendarMonth.vue";

export default Vue.extend({
  name: "Calendar",
  props: {},
  data: () => ({
    selectedMonth: DateTime.local().startOf("month"),
    selectedDay: null
  }),
  computed: {},
  components: {
    CalendarMonth
  }
});
</script>

<template>
  <div class="calendar">This is the calendar
    <CalendarMonth :month="selectedMonth"/>
  </div>
</template>

<style scoped>
.calendar {
  background: cyan;
}
</style>