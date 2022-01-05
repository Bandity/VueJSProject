<template>
  <div>
    <select @change="eventPlayerEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Player</option>
      <option v-for="(el, i) in team" :key="i" :value="i">
        {{ el.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Shop",
  props: {
    team: Array,
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    eventPlayerEmmiter(event) {
      this.$emit("update:selectPlayer",event);
    }
  },
};
</script>

<style>
</style>