<script>
import Vue from "vue";
import { DateTime } from "luxon";
import DayCell from "./DayCell.vue";

export default Vue.extend({
  name: "CalendarMonth",
  props: {
    month: DateTime
  },
  data: () => ({}),
  computed: {
    daysOfMonth() {
      const days = [];

      const monthEnd = this.month.endOf("month");
      const calendarMonthEnd = monthEnd.endOf("week");
      let extraDays = calendarMonthEnd.diff(monthEnd, "days").days - 1;
      if (extraDays === 0) extraDays = 7;

      const dayCount = this.month.daysInMonth + extraDays;
      const calendarMonthStart = this.month.startOf("week");
      let i = calendarMonthStart.diff(this.month, "days").days - 1;

      console.log(i);
      for (; i < dayCount; i++) {
        days.push(this.month.plus({ days: i }));
      }
      return days;
    }
  },
  components: {
    DayCell
  }
});
</script>

<template>
  <div class="calendar-month">
    <div class="month-name">{{ month.monthLong }}</div>
    <ul class="day-list">
      <li v-for="day of daysOfMonth" :key="day.toISODate()">
        <DayCell :month="month" :day="day" :tasks="[]"/>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.calendar-month {
  background: rgba(0, 0, 255, 0.25);
}
</style>