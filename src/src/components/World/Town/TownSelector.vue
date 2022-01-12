<template>
  <div v-if="townsNames !== null">
    <select @change="eventTownSelectorEmmiter($event)" >
      <option value="null" disabled selected="selected">Please Select a Town</option>
      <option v-for="(el, i) in townsNames" :key="i" :value="i" >
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
      let id = event.target.value;
      this.$emit("change:selectedTown",id);
    },
  },
};
</script>

<style>
</style>