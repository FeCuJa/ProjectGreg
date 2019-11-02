<script>
import Vue from "vue";
import { DateTime } from "luxon";

export default Vue.extend({
  name: "DayCell",
  props: {
    month: DateTime,
    day: DateTime,
    tasks: Array
  },
  computed: {
    isInMonth() {
      return this.day.hasSame(this.month, "month");
    },
    isToday() {
      return this.day.hasSame(DateTime.local(), "day");
    }
  }
});
</script>

<template>
  <div class="day" :class="{today: isToday, outsideMonth: !isInMonth}">
    <span>{{ day.day }}</span>
  </div>
</template>

<style scoped>
.day {
  border: 1px solid blue;
  margin: 1px;
}
.day.outsideMonth {
  border-color: silver;
}
.day.today {
  border: 1px solid yellow;
}
.day:hover {
  background: rgba(200, 230, 255, 0.8);
}
</style>