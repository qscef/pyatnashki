<template>
  <div class="main">
    <div class="game-win" v-if="isWin">
      <h2>Поздравляем!</h2>
      <div>Вы справились за</div>
      <div> {{ convertTime.min ? convertTime.min + 'м и ': '' }} {{ convertTime.sec }} с</div>
      <div>сделав {{step}} ходов</div>
      <div class="menu menu_modal">
        <div class="menu__element menu__element_restart" @click="restart()">Заново</div>
      </div>
    </div>
    <div class="header">Пятнашки</div>
    <div class="menu">
      <div class="menu__element">Время
        <div> {{ convertTime.min ? convertTime.min + 'м ': '' }} {{ convertTime.sec }} с</div>
      </div>
      <div class="menu__element menu__element_restart" @click="restart()">Заново</div>
      <div class="menu__element">Ходов
        <div>{{step}}</div>
      </div>   
    </div>
    <div class="game-field">
      <game-tile v-for="tile in listTiles"
        :name="tile.name" 
        :positionCorrect="tile.position === tile.name" 
        :positionUseful="tile.positionUseful" 
        :key="tile.position"
        @move="move($event)"
      />
    </div>
  </div>
</template>

<script>
import gameTile from '../components/gameTile'

export default {
  components: { gameTile },
  data() {
    return {
      convertTime: {min: 0, sec: 0},
      step: 0,
      positionZeroTile: 16,
      listTiles: [
        { name: 1, position: 1 },
        { name: 2, position: 2 },
        { name: 3, position: 3 },
        { name: 4, position: 4 },
        { name: 5, position: 5 },
        { name: 6, position: 6 },
        { name: 7, position: 7 },
        { name: 8, position: 8 },
        { name: 9, position: 9 },
        { name: 10, position: 10 },
        { name: 11, position: 11 },
        { name: 12, position: 12 },
        { name: 13, position: 13 },
        { name: 14, position: 14 },
        { name: 15, position: 15 },
        { name: 0, position: 16 },
      ], 
    }
  },
  created() {
    this.createBoard();
    this.timer();
  },
  methods: {
    restart() {
      this.convertTime.sec = 0;
      this.convertTime.min = 0;
      this.step = 0;
      this.createBoard();
    },
    createBoard() {
      //алгоритм «Тасование Фишера — Йетса»
      for (let i = this.listTiles.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1))
        let t = this.listTiles[i].name
        this.listTiles[i].name = this.listTiles[j].name
        this.listTiles[j].name = t
      }
      this.canMove();
    },
    canMove() { // поиск возможных перемещений
      for (let i = 0; i < this.listTiles.length; i++) {
        this.listTiles[i].positionUseful = false
        if (this.listTiles[i].name === 0) {
          this.positionZeroTile = this.listTiles[i].position - 1  // т.к. нумерация начинается с 1
        }
      }
      //соседи справа
      if ([3,7,11,15].indexOf(this.positionZeroTile) === -1) { // если 0 не в правой колонке
        this.listTiles[this.positionZeroTile + 1].positionUseful = true
      }
      //соседи слева
      if ([0,4,8,12].indexOf(this.positionZeroTile) === -1) { // если 0 не в левой колонке
        this.listTiles[this.positionZeroTile - 1].positionUseful = true
      }
      //соседи сверху
      if ([0,1,2,3].indexOf(this.positionZeroTile) === -1) { // если 0 не в верхней строке
        this.listTiles[this.positionZeroTile - 4].positionUseful = true
      }
      //соседи снизу
      if ([12,13,14,15].indexOf(this.positionZeroTile) === -1) { // если 0 не в нижней строке
        this.listTiles[this.positionZeroTile + 4].positionUseful = true
      }
    },
    move(moveTile) {
      for (let i = 0; i < this.listTiles.length; i++) {
        if (this.listTiles[i].name === moveTile) {
          this.listTiles[this.positionZeroTile].name = this.listTiles[i].name // на позицию старого "0" ставим новый блок
          this.positionZeroTile = this.listTiles[i].position - 1 // обновляем позицию нового "0" т.к. нумерация начинается с 1
          this.listTiles[this.positionZeroTile].name = 0 // присваеваем новому "0" -> 0
          break
        }
      }
      this.step += 1
      this.canMove()
    },
    timer() {
      setInterval(() => {
        if (this.isWin) {
          return
        }
        if (this.convertTime.sec == 59) {
          this.convertTime.min += 1
          this.convertTime.sec = 0
        } else {
          this.convertTime.sec += 1
        }
      }, 1000)
    }
  }, 
  computed: {
    isWin() {
      for (let i = 0; i < this.listTiles.length; i++) {
        if (this.listTiles[i].name !== 0 && this.listTiles[i].name !== this.listTiles[i].position) {
          return false
        }
      }
      return true
    }
  },
}
</script>

<style lang="scss">
  @import '../assets/scss/styles.scss';
</style>