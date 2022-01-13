v-droppable.[groupname]="[droppable callback function]"

<template>
  <div>
    <table border="1" v-if="currentPlayer !== null">
      <tr v-for="(el, i) in currentPlayer.slots" :key="i">
        <td>{{ [i + 1] }} {{ el.name }}</td>
        <td v-for="(item, index) in el.items" :key="index">
          [ {{ index + 1 }} ] - {{ item.name }}
        </td>
      </tr>
    </table>

    <div v-if="currentPlayer != null">
          <br /><label>Bought Items: </label>
    <input readonly  v-if="currentPlayer !== null" :value="boughtItems"><!--
      <div v-for="(el, i) in currentPlayer.boughtItems" :key="i " @dragstart="startDrag($event,i)"  style="display:flex;">
        {{ el.name }}
      </div><br />-->
    </div>
    <br />
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
  computed: {
    boughtItems() {
      let txt = "";
      for (let i = 0; i < this.currentPlayer.boughtItems.length; i++) {
        txt +=
          "[ " + (i + 1) + " ] - " + this.currentPlayer.boughtItems[i].name+", ";
      }
      return txt;
    },
  },
  methods: {
    startDrag(event, i) {
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      event.dataTransfer.setData("itemID", i);

    },
  },
};
</script>
<style>
</style>