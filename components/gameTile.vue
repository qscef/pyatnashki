<template>
  <button class="game-tile" 
    :class="{'empty': name === 0, 'correct': positionCorrect, 'useful' : positionUseful}"
    :disabled="!positionUseful"
    @click="$emit('move', name)">
    {{ name }}
  </button>
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