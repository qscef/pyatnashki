<template>
  <div class="game-tile" :class="{'empty': name === 0, 'correct': positionCorrect, 'useful':positionUseful}">
    {{ name }}
  </div>
</template>

<script>
export default {
  props: {
    name: {type: Number, default: 0},
    positionCorrect: {type: Boolean, default: false},
    positionUseful: {type: Boolean, default: false},
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

    &.empty {
      opacity: 0;
    }

    &.correct {
      background: $accept-color;
    }

    &.useful {
      cursor: pointer;
      width: 81px;
      height: 81px;
      border: 2px solid $accept-color;

      &:hover {
        animation: upTile 1s ease-in-out forwards;
      }
    }
  }

  @keyframes upTile {
    from {
    background: $background-tile-color ;
    }
    to {
    background: $accept-color ;
    }
  }
</style>