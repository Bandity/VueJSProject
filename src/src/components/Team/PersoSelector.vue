<template>
  <div>
    <select @change="selectPlayer($event)">
      <option v-for="(el, i) in team" :key="i" :value="i">
        {{ el.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "PersoSelector",
  props: {
    team: Array,
    currentPlayer: String
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    selectPlayer(event) {
      let id = event.target.value;
      this.$props.currentPlayer = this.$props.team[id].name
    }
  },
};
</script>

<style>
</style>