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
        <game-tile :name="i" v-for="i in listTile" :key="i"></game-tile>
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
      listTile: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,0],
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
      this.listTile = this.listTile.sort(() => Math.random() - 0.5);
    }
  }
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
