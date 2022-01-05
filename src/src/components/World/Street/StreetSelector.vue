<template>
  <div v-if="townName !== null">
    <select @change="eventStreetEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Street</option>
      <option v-for="(el, i) in streets" :key="i" :value="i">
        {{ el }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "StreetSelector",
  props: {
    streets: Array,
    townName : String
  },
  data: () => {
    return {
    };
  },
  computed: {},
  mounted:()=> {
  },
  methods: {
    eventStreetEmmiter(event) {
      this.$emit("update:streets",event);
    }
  },
};
</script>

<style>
</style>