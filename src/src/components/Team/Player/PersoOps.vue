<template >
<div v-if="currentPlayer !== null && currentShop !== null">
  <div style="flex-direction: column; display: flex; flex: 8 auto; ">
    <div>
      <label for="items_to__buy">Number of items to buy: </label>
      <input id="items_to_buy" type="text" v-model="idxItemBuy" />
      <button @click="buy">Buy</button><br /><br />
    </div>
    <div>
      <label for="boughtItem">bought number</label> 
      <input type="number" id="boughtItem" v-model="idxItemBought" /><br /><br />
      <label>slot number</label> 
      <input type="number" v-model="idxSlotAssign" />
      <button @click="assign">Assign</button><br /><br />
    </div>
    <div>
      <label>Objects to order</label> 
      <input type="text" v-model="idxItemOrder" />
      <button @click="order()">Order</button><br /><br />
    </div>

    <div>
      <label>Objects to sell</label> 
      <input type="text" value="1" v-model="idxItemSell" /><br /><br />
      <label>Slot to sell </label> 
      <input type="text" value="1" v-model="idxSlotSell" />
      <button @click="sell()">Sell</button>
    </div>
  </div>
</div>
</template>

<script>
import {itemLimits} from "./../../../model/model"
export default {
  name: "PersoOps",
  props: {
    currentPlayer: Object,
    currentShop: Object
  },
  data: () => {
    return {
      idxItemBuy: 1, // la valeur du champ de saisie pour acheter un item
      idxItemOrder: 1, // la valeur du champ de saisie pour commander un item
      idxItemBought: 1, // la valeur du champ de saisie "index item" pour assigner un item
      idxSlotAssign: 1, // la valeur du champ de saisie "index slot" pour assigner un item
      idxItemSell: 1, // la valeur du champ de saisie "index item" pour vendre un item
      idxSlotSell: 1, // la valeur du champ de saisie "index slot" pour vendre un item
      itemLimits,
    };
  },
  mounted (){
    console.log(this.$props)
  },
  methods: {
    assign() {
      let item = this.currentPlayer.boughtItems[this.idxItemBought-1];
      // find which limits corresponds to the target slot
      let lim = this.itemLimits.find(
        (e) => e.slot === this.currentPlayer.slots[this.idxSlotAssign-1].name
      );
      // check if item number is already reached
      if (
        this.currentPlayer.slots[this.idxSlotAssign-1].items.length === lim.limit
      )
        return (
          "slot " +
          this.currentPlayer.slots[this.idxSlotAssign-1].name +
          " is full"
        );
      // check if item type is allowed
      if (!lim.types.includes(item.type))
        return (
          "wrong item type [" +
          item.type +
          "] for slot " +
          this.currentPlayer.slots[this.idxSlotAssign-1].name
        );
      this.currentPlayer.boughtItems.splice(this.idxItemBought, 1);
      this.currentPlayer.slots[this.idxSlotAssign-1].items.push(item);
      return "";
    },
    buy() {
      if (
          this.currentShop.itemStock[this.idxItemBuy-1].price >
        this.currentPlayer.gold
      )
        return "not enough gold";
      this.currentPlayer.boughtItems.push(
          this.currentShop.itemStock[this.idxItemBuy-1]
      );
      this.currentPlayer.gold -=
          this.currentShop.itemStock[this.idxItemBuy-1].price;
      return "";
    },
    async order() {
      await  this.currentShop.itemStock.push(
          this.currentShop.itemOrder[this.idxItemOrder-1]
      );
    },
    sell() {
      this.currentPlayer.slots[this.idxSlotSell-1].items.splice(
        this.idxItemSell,
        1
      );
      this.currentPlayer.gold += this.idxItemSell.price;
    },
  },
};
</script>

<style>

</style>