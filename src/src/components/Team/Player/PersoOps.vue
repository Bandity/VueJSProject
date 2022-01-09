<template >
  <div v-if="currentPlayer !== null">
    <div style="flex-direction: column; display: flex; flex: 8 auto">
      <div>
        <h2 style="align-items: center; text-align: center">
          Player Operations
        </h2>
      </div>
      <div>
        <div>
          <label for="boughtItem">Item to assign: </label>
          <input type="text" id="boughtItem" v-model="idxItemBought" />
          <label>Slot number to assign the item to: </label>
          <input type="text" v-model="idxSlotAssign" /><br />
          <div class="btn">
            <button @click="assign">Assign Item</button><br /><br />
          </div>
          <p
            v-if="this.error !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.error }}
          </p>
        </div>
        <div style="padding-top: 40px">
          <label for="boughtItem">Item to desassign: </label>
          <input
            type="text"
            id="boughtItem"
            v-model="idxItemDesassign"
            v-required
          />

          <label>Slot number to desassign the item to: </label>
          <input type="text" v-model="idxSlotDeassign" /><br />
          <div class="btn">
            <button @click="desassign">Desassign Item</button><br /><br />
          </div>
          <p
            v-if="this.error2 !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.error2 }}
          </p>
        </div>
      </div>
      <div v-if="currentShop !== null" class="store-operations">
        <h2 style="align-items: center; text-align: center">
          Store Operations
        </h2>
        <div>
          <label for="items_to__buy">Number of item you want to buy: </label>
          <input id="items_to_buy" type="text" v-model="idxItemBuy" />
          <button @click="buy">Buy</button><br /><br />
          <p
            v-if="this.errorbuy !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.errorbuy }}
          </p>
        </div>
        <div>
          <label>Object to order: </label>
          <input type="text" v-model="idxItemOrder" />
          <button @click="order()">Order</button><br /><br />
          <p
            v-if="this.errororder !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.errororder }}
          </p>
        </div>

        <div>
          <label>Object to sell: </label>
          <input type="text" value="1" v-model="idxItemSell" /><br /><br />
        </div>
        <div>
          <label>Slot to sell: </label>
          <input type="text" value="1" v-model="idxSlotSell" />
          <button @click="sell()">Sell</button>
          <p
            v-if="this.errorsell !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.errorsell }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { itemLimits } from "./../../../model/model";
export default {
  name: "PersoOps",
  props: {
    currentPlayer: Object,
    currentShop: Object,
  },
  data: () => {
    return {
      idxItemBuy: 1, // la valeur du champ de saisie pour acheter un item
      idxItemOrder: 1, // la valeur du champ de saisie pour commander un item
      idxItemBought: 1, // la valeur du champ de saisie "index item" pour assigner un item
      idxSlotAssign: 1, // la valeur du champ de saisie "index slot" pour assigner un item
      idxItemSell: 1, // la valeur du champ de saisie "index item" pour vendre un item
      idxSlotSell: 1, // la valeur du champ de saisie "index slot" pour vendre un item
      idxSlotDeassign: 1,
      idxItemDesassign: 1, // la valeur du champ de saisie "index to desassign" pour désequiper le item
      itemLimits,
      error: null,
      error2: null,
      errorbuy: null,
      errordeassing: null,
      errordeassing2: null,
      errorsell: null,
      errororder: null,
    };
  },
  methods: {
    assign() {
      if (isNaN(this.idxItemBought) || isNaN(this.idxItemBought) < 0) {
        this.error =
          "This is not a valid number id from Bought Items. Please try again";
        return;
      } else if (isNaN(this.idxSlotAssign) || isNaN(this.idxSlotAssign) < 0) {
        this.error =
          "This is not a valid number id from Slots Items. Please try again";
        return;
      }
      this.error = null;
      this.error2 = null;
      let item = this.currentPlayer.boughtItems[this.idxItemBought - 1];
      // find which limits corresponds to the target slot
      let lim = this.itemLimits.find(
        (e) => e.slot === this.currentPlayer.slots[this.idxSlotAssign - 1].name
      );
      // check if item number is already reached
      if (
        this.currentPlayer.slots[this.idxSlotAssign - 1].items.length ===
        lim.limit
      ) {
        this.error =
          "slot " +
          this.currentPlayer.slots[this.idxSlotAssign - 1].name +
          " is full";
        return;
      }
      // check if item type is allowed
      if (!lim.types.includes(item.type)) {
        this.error =
          "wrong item type [" +
          item.type +
          "] for slot " +
          this.currentPlayer.slots[this.idxSlotAssign - 1].name;
        return;
      }
      this.currentPlayer.boughtItems.splice(this.idxItemBought - 1, 1);
      this.currentPlayer.slots[this.idxSlotAssign - 1].items.push(item);
      return "";
    },
    buy() {
      if (
        this.currentShop.itemStock[this.idxItemBuy - 1].price >
        this.currentPlayer.gold
      ) {
        this.errorbuy = "not enough gold";
        return;
      }
      this.currentPlayer.boughtItems.push(
        this.currentShop.itemStock[this.idxItemBuy - 1]
      );
      this.currentPlayer.gold -=
        this.currentShop.itemStock[this.idxItemBuy - 1].price;
      this.currentShop.itemStock.splice(this.idxItemBuy - 1, 1);
      this.errorbuy = null;
      return "";
    },
    async order() {
            if (isNaN(this.idxItemOrder) || isNaN(this.idxItemOrder) < 0 || isNaN(this.idxItemOrder) > this.currentShop.itemOrder.length) {
        this.errororder =
          "This is not a valid number id from item to order. Please try again";
        return;
      } 
      this.errororder = null;
      await this.currentShop.itemStock.push(
        this.currentShop.itemOrder[this.idxItemOrder - 1]
      );
      this.currentShop.itemOrder.splice(this.idxItemOrder - 1, 1);
    },
    sell() {
      if (isNaN(this.idxItemSell) || isNaN(this.idxItemSell) < 0) {
        this.errorsell =
          "This is not a valid number id from item to sell. Please try again";
        return;
      } 
      this.errorsell = null;
      let item = this.currentPlayer.boughtItems[this.idxItemSell - 1];
      this.currentPlayer.boughtItems.splice(this.idxItem -1,1)
      this.currentPlayer.gold += item.price;
    },
    desassign() {
      if (isNaN(this.idxItemDesassign) || isNaN(this.idxItemDesassign) < 0) {
        this.errordeassing =
          "This is not a valid number id from item to desassign. Please try again";
        return;
      } else if (
        isNaN(this.idxSlotDeassign) ||
        isNaN(this.idxSlotDeassign) < 0
      ) {
        this.errordeassing2 =
          "This is not a valid number id from Slots Items. Please try again";
        return;
      }
      this.errordeassing = null;
      this.errordeassing2 = null;
      let item = this.currentPlayer.slots[this.idxSlotDeassign - 1].items[this.idxItemDesassign-1];
      if(item !== undefined){
        this.currentPlayer.slots[this.idxSlotDeassign - 1].items.splice(this.idxItemDesassign-1, 1);
        this.currentPlayer.boughtItems.push(item);
      }
    },
  },
};
</script>

<style scoped>
.btn {
  justify-content: center;
  display: flex;
  flex-direction: center;
  align-items: center;
}
.store-operations {
  padding-top: 10px;
}
.store-operations > h1,
input {
  align-items: center;
  text-align: center;

  width: 20px;
  text-align: center;
}
</style>
