<template>
  <div v-if="currentPlayer !== null">
    <div style="display: flex; text-align: center">
      <p>
        Name :
        <span style="font-weight: bolder">{{ currentPlayer.name }} </span>
      </p>

      <slot name="level" :level="currentPlayer.level"></slot>
    </div>
    <p style="font-weight: bolder; padding-left: 50px">Player Stats</p>
    <div style="display: flex; flex: 8; border">
      <div style="flex-grow: 0.1">
        <p>
          Life : <span style="color: red"> {{ currentPlayer.life }}</span>
        </p>
        <p>
          Armor :<span style="color: gray"> {{ currentPlayer.armor }}</span>
        </p>
      </div>
      <div style="flex-grow: 1">
        <p>
          Vitality :
          <span style="color: orange"> {{ currentPlayer.vitality }}</span>
        </p>
        <p>
          Strength :
          <span style="color: rgb(0, 158, 243)">
            {{ currentPlayer.strength }}</span
          >
        </p>
      </div>
    </div>
    <slot name="gold" :gold="currentPlayer.gold"></slot>
    <br />
  </div>
</template>

<script>
export default {
  name: "PersoCaracs",
  props: {
    currentPlayer: Object,
  },
  data: () => {
    return {};
  },
};
</script>

<style>
text {
  margin: 10px 10 10 10;
}
</style>