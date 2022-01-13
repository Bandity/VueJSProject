<template >
  <div v-if="currentPlayer !== null">
    <div style="flex-direction: column; display: flex; flex: 8 auto">
      <div>
        <h3 style="align-items: center; text-align: center">
          Player Operations
        </h3>
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
            v-if="this.errordeassing !== null"
            style="color: red; text-align: center; font-size: x-small"
          >
            {{ this.errordeassing }}
          </p>
        </div>
      </div>
      <div v-if="currentShop !== null" class="store-operations">
        <h3 style="align-items: center; text-align: center">
          Store Operations
        </h3>
        <div style="display: flex">
          <label for="items_to__buy">Number of item you want to buy: </label>
           <input id="items_to_buy" type="text" v-model="idxItemBuy" style="height: 20px;"/>
          <img
            @click="buy"
            src="../../../assets/Player/buy.png"
            width="40px"
            height="40px"
            style="
              display: flex;
              flex-direction: column;
              flex: 8;
              justify-content: center;
              align-items: center;
              text-align: center;
              align-content: center;
              flex-grow:0;
              height: 30px;
            "
          />
        </div>
        <p
          v-if="this.errorbuy !== null"
          style="color: red; text-align: center; font-size: x-small"
        >
          {{ this.errorbuy }}
        </p>
        <br /><br />

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
        <div style="display: flex">
          <div>
            <label>Object to sell: </label>
            <input type="text" value="1" v-model="idxItemSell" />
          </div>
          <div>
            <label>Slot to sell: </label>
            <input type="text" value="1" v-model="idxSlotSell" />
            <div style="padding-top: 10px">
              <p class="sell" @click="sell()">Sell</p>
            </div>
          </div>
        </div>
        <p
          v-if="this.errorsell !== null"
          style="color: red; text-align: center; font-size: x-small"
        >
          {{ this.errorsell }}
        </p>
        <div style="display: flex">
          <div>
            <label>Item to sell from bought items: </label>
            <input type="text" value="1" v-model="idxFromBought" />
            <div style="padding-top: 10px">
              <p class="sell" @click="sellfromBought()">Sell</p>
            </div>
          </div>
                  <p
          v-if="this.errorsellfromBought !== null"
          style="color: red; text-align: center; font-size: x-small"
        >
          {{ this.errorsellfromBought }}
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
      idxFromBought: 1,
      itemLimits,
      error: null,
      error2: null,
      errorbuy: null,
      errordeassing: null,
      errordeassing2: null,
      errorsell: null,
      errororder: null,
      errorsellfromBought : null,
    };
  },
  methods: {
    assign() {
      if (isNaN(this.idxItemBought)) {
        this.error =
          "This is not a valid number or id from Bought Items. Please try again";
        return;
      } else if (isNaN(this.idxSlotAssign)) {
        this.error =
          "This is not a valid number or id from Slots Items. Please try again";
        return;
      } else if (
        this.idxSlotAssign <= 0 ||
        this.idxSlotAssign > this.currentPlayer.slots.length
      ) {
        this.error =
          "This is not a valid number because the slot length = " +
          this.currentPlayer.slots.length +
          " and you typed " +
          this.idxSlotAssign;
        return;
      } else if (
        this.idxItemBought <= 0 ||
        this.idxItemBought > this.currentPlayer.boughtItems.length
      ) {
        this.error =
          "This is not a valid number because the bought items length = " +
          this.currentPlayer.boughtItems.length +
          " and you typed " +
          this.idxItemBought;
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
      let number = "";
      for (let i = 2; i < item.effect.length; i++) {
        number += item.effect[i];
      }

      //Effects
      if (item.effect[0] === "S") {
        if (item.effect[1] === "+") {
          this.currentPlayer.strength += parseInt(number);
        } else {
          this.currentPlayer.strength -= parseInt(number);
        }
      } else if (item.effect[0] === "L") {
        if (item.effect[1] === "+") {
          this.currentPlayer.vitality += parseInt(number);
        } else {
          this.currentPlayer.vitality -= parseInt(number);
        }
      } else if (item.effect[0] === "A") {
        if (item.effect[1] === "+") {
          this.currentPlayer.armor += parseInt(number);
        } else {
          this.currentPlayer.armor -= parseInt(number);
        }
      }

      return;
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
    order() {
      if (isNaN(this.idxItemOrder)) {
        this.errororder =
          "This is not a valid number or id from item to order. Please try again";
        return;
      } else if (this.currentShop.itemOrder.length < this.idxItemOrder) {
        this.errororder =
          "There's no items with that id [ " +
          this.idxItemOrder +
          " ] to order!";
        return;
      } else if (this.currentShop.itemOrder.length === 0) {
        this.errororder = "There's no items to order!";
        return;
      }
      this.errororder = null;
      this.currentShop.itemStock.push(
        this.currentShop.itemOrder[this.idxItemOrder - 1]
      );
      this.currentShop.itemOrder.splice(this.idxItemOrder - 1, 1);
    },
    sell() {
      if (isNaN(this.idxItemSell)) {
        this.errorsell =
          "This is not a valid number or id from item to sell. Please try again";
        return;
      } else if (isNaN(this.idxSlotSell)) {
        this.errorsell =
          "This is not a valid number or id from slot to sell. Please try again";
        return;
      } else if (this.currentPlayer.slots.length < this.idxSlotSell - 1) {
        this.errorsell =
          "This is not a valid number [ " +
          this.idxSlotSell +
          " ] is out of range because the slot length = " +
          this.currentPlayer.slots.length;
        return;
      } else if (
        this.currentPlayer.slots[this.idxSlotSell - 1].items.length <=
        this.idxItemSell - 1
      ) {
        this.errorsell =
          "This is not a valid number [ " +
          this.idxItemSell +
          " ] is out of range because the items length = " +
          this.currentPlayer.slots[this.idxSlotSell - 1].items.length +
          " in the slot [ " +
          this.idxSlotSell +
          " ]";
        return;
      }
      this.errorsell = null;
      let item =
        this.currentPlayer.slots[this.idxSlotSell - 1].items[
          this.idxItemSell - 1
        ];
      this.currentPlayer.slots[this.idxSlotSell - 1].items.splice(
        this.idxItem - 1,
        1
      );
      this.currentShop.itemStock.push(item);
      this.currentPlayer.gold += item.price;
      //Effects
      let number = "";
      for (let i = 2; i < item.effect.length; i++) {
        number += item.effect[i];
      }

      if (item.effect[0] === "S") {
        if (item.effect[1] === "+") {
          this.currentPlayer.strength -= parseInt(number);
        } else {
          this.currentPlayer.strength += parseInt(number);
        }
      } else if (item.effect[0] === "L") {
        if (item.effect[1] === "+") {
          this.currentPlayer.vitality -= parseInt(number);
        } else {
          this.currentPlayer.vitality += parseInt(number);
        }
      } else if (item.effect[0] === "A") {
        if (item.effect[1] === "+") {
          this.currentPlayer.armor -= parseInt(number);
        } else {
          this.currentPlayer.armor += parseInt(number);
        }
      }
    },
    desassign() {
      if (isNaN(this.idxItemDesassign)) {
        this.errordeassing =
          "This is not a valid number id from item to desassign. Please try again";
        return;
      } else if (isNaN(this.idxSlotDeassign)) {
        this.errordeassing2 =
          "This is not a valid number or id from Slots Items. Please try again";
        return;
      } else if (this.idxSlotDeassign <= 0) {
        this.errordeassing =
          "This is not a valid number because the slot length = " +
          this.currentPlayer.slots.length +
          " and you typed " +
          this.idxSlotAssign;
        return;
      } else if (this.idxSlotDeassign > this.currentPlayer.slots.length) {
        this.errordeassing =
          "This is not a valid number because the slot length = " +
          this.currentPlayer.slots.length +
          " and you typed " +
          this.idxSlotAssign;
        return;
      } else if (this.idxItemDesassign <= 0) {
        this.errordeassing =
          "This is not a valid number because the slot " +
          this.idxSlotDeassign +
          " has  = " +
          this.currentPlayer.slots[this.idxSlotDeassign - 1].items.length +
          " items and you typed " +
          this.idxItemDesassign;
        return;
      } else if (
        this.idxItemDesassign >
        this.currentPlayer.slots[this.idxSlotDeassign - 1].items.length
      ) {
        this.errordeassing =
          "This is not a valid number because the slot " +
          this.idxSlotDeassign +
          " has  = " +
          this.currentPlayer.slots[this.idxSlotDeassign - 1].items.length +
          " items and you typed " +
          this.idxItemDesassign;
        return;
      }
      this.errordeassing = null;
      let item =
        this.currentPlayer.slots[this.idxSlotDeassign - 1].items[
          this.idxItemDesassign - 1
        ];
      if (item !== undefined) {
        this.currentPlayer.slots[this.idxSlotDeassign - 1].items.splice(
          this.idxItemDesassign - 1,
          1
        );
        this.currentPlayer.boughtItems.push(item);
      }
      //Effects
      let number = "";
      for (let i = 2; i < item.effect.length; i++) {
        number += item.effect[i];
      }

      if (item.effect[0] === "S") {
        if (item.effect[1] === "+") {
          this.currentPlayer.strength -= parseInt(number);
        } else {
          this.currentPlayer.strength += parseInt(number);
        }
      } else if (item.effect[0] === "L") {
        if (item.effect[1] === "+") {
          this.currentPlayer.vitality -= parseInt(number);
        } else {
          this.currentPlayer.vitality += parseInt(number);
        }
      } else if (item.effect[0] === "A") {
        if (item.effect[1] === "+") {
          this.currentPlayer.armor -= parseInt(number);
        } else {
          this.currentPlayer.armor += parseInt(number);
        }
      }
    },
    sellfromBought (){
      if(isNaN(this.idxFromBought)) {
        this.errorsellfromBought =
          "This is not a valid number id from boughtItems item to desassign. Please try again";
        return;
      }if(this.idxFromBought <= 0 || this.idxFromBought >= this.currentPlayer.boughtItems.length) {
        this.errorsellfromBought=
        "This is not a valid number because the bought items length is : " +
          this.currentPlayer.boughtItems.length+
          " and you typed " +
          this.idxFromBought;
      }
      this.errorsellfromBought = null;
      let item = this.currentPlayer.boughtItems[this.idxFromBought - 1];
      this.currentPlayer.boughtItems.splice(this.idxFromBought - 1,1);
      this.currentShop.itemStock.push(item);
      this.currentPlayer.gold += item.price;
      return
    }
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
input {
  align-items: center;
  text-align: center;

  width: 20px;
  text-align: center;
}
.sell {
  display: flex;
  padding-left: 20px;
  padding-right: 20px;
  transition: color 0.3s ease-in-out;
  color: green;
}
.sell:hover {
  color: rgb(0, 255, 136);
  
}
</style>
