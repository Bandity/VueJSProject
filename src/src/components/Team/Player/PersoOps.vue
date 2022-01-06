<template>
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
</template>

<script>
export default {
  name: "PersoOps",
  props: {
    currentPlayer: Object,
  },
  data: () => {
    return {
      idxItemBuy: 1, // la valeur du champ de saisie pour acheter un item
      idxItemOrder: 1, // la valeur du champ de saisie pour commander un item
      idxItemBought: 1, // la valeur du champ de saisie "index item" pour assigner un item
      idxSlotAssign: 1, // la valeur du champ de saisie "index slot" pour assigner un item
      idxItemSell: 1, // la valeur du champ de saisie "index item" pour vendre un item
      idxSlotSell: 1, // la valeur du champ de saisie "index slot" pour vendre un item
    };
  },
  methods: {
    assign() {
      let item = this.$props.currentPlayer.boughtItems[this.idxItemBought];
      // find which limits corresponds to the target slot
      let lim = this.itemLimits.find(
        (e) => e.slot === this.currentPlayer.slots[this.idxSlotAssign].name
      );
      // check if item number is already reached
      if (
        this.currentPlayer.slots[this.idxSlotAssign].items.length === lim.limit
      )
        return (
          "slot " +
          this.currentPlayer.slots[this.idxSlotAssign].name +
          " is full"
        );
      // check if item type is allowed
      if (!lim.types.includes(item.type))
        return (
          "wrong item type [" +
          item.type +
          "] for slot " +
          this.currentPlayer.slots[this.idxSlotAssign].name
        );
      this.currentPlayer.boughtItems.splice(this.idxItemBought, 1);
      this.currentPlayer.slots[this.idxSlotAssign].items.push(item);
      return "";
    },
    buy() {
      if (
        this.currentShop.itemStock[this.idxItemBuy].price >
        this.currentPlayer.gold
      )
        return "not enough gold";
      this.currentPlayer.boughtItems.push(
        this.currentShop.itemStock[this.idxItemBuy]
      );
      this.currentPlayer.gold -=
        this.currentShop.itemStock[this.idxItemBuy].price;
      return "";
    },
    async order() {
      await this.currentShop.itemStock.push(
        this.currentShop.itemOrder[this.idxItemOrder]
      );
    },
    sell() {
      this.currentPlayer.slots[this.idxSlotSell].items.splice(
        this.idxItemSell,
        1
      );
      this.gold += this.idxItemSell.price;
    },
  },
};
</script>

<style>

</style>