<template>
  <div class="game-tile" :class="{'empty': name === 0}">
    {{ name }}
  </div>
</template>

<script>
export default {
  props: {
    name: {type: Number, default: 0},
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/styles.scss';
  .game-tile {
    background: $background-tile-color;
    border-radius: 5px;
    height: 85px;
    width: 85px;
    line-height: 80px;
    font-size: 32px;
    color: $text-main-color;
    text-align: center;
    cursor: pointer;

    &.empty {
      opacity: 0;
    }
  }
</style>