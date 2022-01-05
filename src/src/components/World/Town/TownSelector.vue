<template>
  <div>
    <select @change="eventTownEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Town</option>
      <option v-for="(el, i) in townNames" :key="i" :value="i">
        {{ el }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "TownSelector",
  props: {
    townNames: Array,
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    eventTownEmmiter(event) {
      this.$emit("update:selectedTown",event);
    }
  },
};
</script>

<style>
</style>