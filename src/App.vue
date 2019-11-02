<template>
  <main id="app">
    <Calendar id="calendar"/>
    <Drawer id="drawer"/>
  </main>
</template>

<script>
import Calendar from "./components/Calendar";
import Drawer from "./components/Drawer";

export default {
  name: "App",
  components: {
    Calendar,
    Drawer
  }
};
</script>

<style>
#app {
  display: flex;
  flex-direction: row;
  min-height: 100vh;
}
#calendar {
  flex-basis: 75%;
}
#drawer {
  flex-basis: 25%;
}
</style>
