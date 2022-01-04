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
    name: 'PersoSelector'
}
</script>

<style>

</style>