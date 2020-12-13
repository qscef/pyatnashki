<template>
  <div class="main">
    <div class="header">
      Пятнашки
    </div>
    <div class="menu">
      <div class="menu__element">Время
        <div>{{time}}</div>
      </div>
      <div class="menu__element menu__element_restart" @click="restart()">Рестарт</div>
      <div class="menu__element">Ходов
        <div>{{step}}</div>
      </div>   
    </div>
    <div class="game-field">
      <game-tile v-for="tile in listTiles"
        :name="tile.currentPosition" 
        :positionCorrect="tile.finishPosition === tile.currentPosition" 
        :positionUseful="canMove(tile)" 
        :key="tile.finishPosition">
      </game-tile>
    </div>
  </div>
</template>

<script>
import gameTile from '../components/gameTile'

export default {
  components: { gameTile },
  data() {
    return {
      time: 0,
      step: 0,
      listTiles: [
        // { finishPosition: 1, currentPosition: 1 },
        // { finishPosition: 2, currentPosition: 2 },
        // { finishPosition: 3, currentPosition: 3 },
        // { finishPosition: 4, currentPosition: 4 },
        // { finishPosition: 5, currentPosition: 5 },
        // { finishPosition: 6, currentPosition: 6 },
        // { finishPosition: 7, currentPosition: 7 },
        // { finishPosition: 8, currentPosition: 8 },
        // { finishPosition: 9, currentPosition: 9 },
        // { finishPosition: 10, currentPosition: 10 },
        // { finishPosition: 11, currentPosition: 11 },
        // { finishPosition: 12, currentPosition: 12 },
        // { finishPosition: 13, currentPosition: 13 },
        // { finishPosition: 14, currentPosition: 14 },
        // { finishPosition: 15, currentPosition: 15 },
        // { finishPosition: 0, currentPosition: 0 },

        { currentPosition: 1, finishPosition: 1 },
        { currentPosition: 2, finishPosition: 2 },
        { currentPosition: 3, finishPosition: 3 },
        { currentPosition: 4, finishPosition: 4 },
        { currentPosition: 5, finishPosition: 5 },
        { currentPosition: 6, finishPosition: 6 },
        { currentPosition: 7, finishPosition: 7 },
        { currentPosition: 8, finishPosition: 8 },
        { currentPosition: 9, finishPosition: 9 },
        { currentPosition: 10, finishPosition: 10 },
        { currentPosition: 11, finishPosition: 11 },
        { currentPosition: 12, finishPosition: 12 },
        { currentPosition: 13, finishPosition: 13 },
        { currentPosition: 14, finishPosition: 14 },
        { currentPosition: 15, finishPosition: 15 },
        { currentPosition: 0, finishPosition: 0 },
      ], 
    }
  },
  created() {
    this.createBoard();
  },
  methods: {
    restart() {
      this.time= 0;
      this.step = 0;
      this.createBoard();
    },
    createBoard() {
      //алгоритм «Тасование Фишера — Йетса»
      for (let i = this.listTiles.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1))
        let t = this.listTiles[i].currentPosition
        this.listTiles[i].currentPosition = this.listTiles[j].currentPosition
        this.listTiles[j].currentPosition = t
      }
    },
    canMove(tile) {
      const tempTilePosition = tile.finishPosition - 1 //т.к. нумерация начинается с 1 и дальше удобнее понять алгоритм решил создать переменную
      if (this.listTiles[tempTilePosition + 1] && this.listTiles[tempTilePosition + 1].currentPosition === 0) {
        return true
      }
      if (this.listTiles[tempTilePosition - 1] && this.listTiles[tempTilePosition - 1].currentPosition === 0) {
        return true
      }
    }
  }, 
}
</script>

<style lang="scss">
  @import '../assets/scss/styles.scss';
  .main {
    margin: 0 auto;
    width: 400px;
    background: $background-color;
    border-radius: 10px;

    .header {
      text-align: center;
      font-size: 32px;
      color: $text-main-color;
      padding-top: 20px;
      margin-bottom: 20px;
    }

    .menu {
      display: flex;
      justify-content: space-around;
      margin-bottom: 10px;

      .menu__element {
        width: 100px;
        text-align: center;
        line-height: 20px;
        border-radius: 10px;
        background: $background-field-color;
        cursor: pointer;

        &.menu__element_restart {
          display: flex;
          align-items: center;
          justify-content: center;
        }
      }
    }

    .game-field {
      margin: 5px;
      padding: 10px;
      border-radius: 5px;
      background: $background-field-color;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-gap: 5px;
    }
  }
</style>
