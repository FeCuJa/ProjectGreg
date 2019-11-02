<script>
import Vue from "vue";
import { DateTime } from "luxon";
import DayCell from "./DayCell.vue";

export default Vue.extend({
  name: "CalendarMonth",
  props: {
    month: DateTime
  },
  data: () => ({
    selectedDay: null
  }),
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

      for (; i < dayCount; i++) {
        days.push(this.month.plus({ days: i }));
      }
      return days;
    }
  },
  methods: {
    selectDay(day) {
      this.selectedDay = day;
      this.$emit("selectDay", this.selectDay);
      console.log("Selected day:", day);
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
    <ol class="day-list">
      <li class="day-cell" v-for="day of daysOfMonth" :key="day.toISODate()">
        <DayCell :month="month" :day="day" :tasks="[]" @selectDay="selectDay"/>
      </li>
    </ol>
  </div>
</template>

<style scoped>
.calendar-month {
  background: rgba(0, 0, 255, 0.25);
  height: 100%;
}

.month-name {
  height: 2rem;
  font-size: 2rem;
}

.day-list {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  align-content: stretch;
  list-style: none;
  margin: 0;
  padding: 0;
  height: calc(100% - 2rem);
}
.day-cell {
}
</style>