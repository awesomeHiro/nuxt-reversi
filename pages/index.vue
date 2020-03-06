<template>
  <div class="container">
    <template v-for="x in board.length">
      <div
        v-for="y in board[x - 1].length"
        :key="`${y}-${x}`"
        class="cell"
        @click="putStone(x, y)"
      >
        <div
          v-if="isStone(x, y)"
          :class="['stone', isBlack(x, y) ? 'black' : 'white']"
        />
      </div>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component
export default class extends Vue {
  currentColor = 1 // 1: black, 2:white

  get isStone() {
    return (x: number, y: number) => this.board[x - 1][y - 1] !== 0
  }

  get isBlack() {
    return (x: number, y: number) => this.board[x - 1][y - 1] === 1
  }

  get putStone() {
    return (x: number, y: number) => {
      if (this.isStone(x, y)) {
        return false
      }
      this.board[x - 1][y - 1] = this.currentColor
      this.reRenderBoard()
      this.currentColor = 3 - this.currentColor
    }
  }

  get reRenderBoard() {
    return () => {
      this.board = JSON.parse(JSON.stringify(this.board))
    }
  }

  board = [
    [0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 1, 2, 0, 0, 0],
    [0, 0, 0, 2, 1, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 0]
  ]
}
</script>

<style scoped>
/* autoprefixer grid: no-autoplace */
.container {
  width: 640px;
  height: 640px;
  margin: 20px auto;
  background: #050;
}
.cell {
  float: left;
  width: 12.5%;
  height: 12.5%;
  border: #000 solid;
}

.stone {
  width: 70%;
  height: 70%;
  margin: 15%;
  border-radius: 50%;
}

.black {
  background: #000;
}
.white {
  background: #fff;
}
</style>
