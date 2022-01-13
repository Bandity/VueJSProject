<template>
  <div style="display: flex; padding-top: 20px;">
    <div class="form-select">
    <select @change="eventPlayerEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Player</option>
      <option v-for="(el, i) in team" :key="i" :value="i">
        {{ el.name }}
      </option>
    </select>
    <br/>
    </div>
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
    };
  },
  computed: {},
  methods: {
    eventPlayerEmmiter(event) {
      let id = event.target.value;
      this.$emit("change:selectPlayer",id);
    }
  },
};
</script>

<style>
</style>