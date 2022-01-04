<template>
  <div>
    
    <select @change="selectPlayer($event)">
      <option value="null" disabled selected="selected">Please Select a Player</option>
      <option v-for="(el, i) in team" :key="i" :value="i">
        {{ el.name }}
      </option>
    </select>
    <slot :player="currentPlayer"></slot>

  </div>
</template>

<script>
export default {
  name: "PersoSelector",
  props: {
    team: Array,
  },
  data: () => {
    return {
      currentPlayer:""
    };
  },
  computed: {},
  methods: {
    selectPlayer(event) {
      console.log();
      this.currentPlayer = this.$props.team[event.target.value].name;
      this.$emit("update:selectPlayer",event);
    }
  },
};
</script>

<style>
</style>