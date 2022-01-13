<template>
  <div v-if="townsNames !== null" class="main">
    <div style="display: flex">
      <img
        class="image-container"
        v-for="(el, i) in townsNames"
        :key="i"
        :src="getImgUrl(i)"
      />
    </div>
    <div style="display: flex;" >
      <p v-for="(el, id) in townsNames" :key="id" class="text" @click="eventTownSelectorEmmiter(id)">
        {{ el }}
      </p>
    </div>
    <slot />
  </div>
</template>

<script>
export default {
  name: "TownSelector",
  props: {
    townsNames: Array,
  },
  data: () => {
    return {};
  },
  computed: {},
  methods: {
    eventTownSelectorEmmiter(id) {
      this.$emit("change:selectedTown", id);
    },
    getImgUrl(i) {
      var images = require.context("../../../assets/Town", false, /\.png$/);
      return images("./" + (1 + i) + ".png");
    },
  },
};
</script>

<style  scoped>
.image-container {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  max-width: 100px;
  padding: 0px 0px 10px 10px;
  flex: 8;
  text-align: center;
}
.main {
  display: flex;
  flex: 9;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  align-content: center;
}
.text {
  display: flex;
  padding-left: 20px; 
  padding-right:20px;
  transition: opacity color 0.3s ease-in-out;
}
.text:hover{
  opacity: 0.5;
  color: red;
}
</style>