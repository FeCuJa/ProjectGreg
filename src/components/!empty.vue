<script>
import Vue from "vue";

export default Vue.extend({
  name: "ComponentName",
  props: {
    something: String
  },
  data: () => ({
    someData: "asdf"
  }),
  computed: {
    someComputedData: () => this.someData.toUpper()
    //someComputedData: function() { return this.someData.toUpper(); }
  },
  methods: {
    someMethod(args) {}
  },
  components: {}
});
</script>

<template>
  <div class="asdf">Example</div>
</template>

<style scoped>
.asdf {
  background: red;
}
</style>