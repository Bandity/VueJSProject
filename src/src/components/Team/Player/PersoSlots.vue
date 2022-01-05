<template>
  <div>
    <table border="1">
      <tr v-for="(el, i) in currentPlayer.slots" :key="i">
        <td>{{ el.name }}</td>
        <td v-for="(item, index) in el.items" :key="index">
          [ {{ index }} ] - {{ item.name }}
        </td>
      </tr>
    </table>
    <input readonly="readonly" :value="boughtItems" /><br />
  </div>
</template>

<script>
export default {
  name: "PersoSlots",
  props: {
    currentPlayer: Object,
  },
  data: () => {
    return {};
  },
};
</script>

<style>
</style>