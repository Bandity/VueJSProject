<template>
  <div v-if="townsNames.length > 0 ">
    <select @change="eventTownSelectorEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Town</option>
      <option v-for="(el, i) in townsNames" :key="i" :value="i">
        {{ el }}
      </option>
    </select>
    <slot/>
  </div>
</template>

<script>
export default {
  name: "TownSelector",
  props: {
    townsNames: Array,
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    eventTownSelectorEmmiter(event) {
      this.$emit("update:selectedTown",event);
    }
  },
};
</script>

<style>
</style>