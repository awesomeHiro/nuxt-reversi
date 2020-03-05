<template>
  <div class="container">
    <template v-for="x in board.length">
      <div v-for="y in board[x - 1].length" :key="`${y}-${x}`" class="cell">
        <div v-if="isStone(x, y)" :class="['stone', isBlack(x, y) ? 'black' : 'white']" />
      </div>
    </template>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component
export default class extends Vue {
  isPuttable(x: number, y: number) {
    return false
  }

  get isStone() {
    return (x: number, y: number) => this.board[x - 1][y - 1] !== 0
  }

  get isBlack() {
    return (x: number, y: number) => this.board[x - 1][y - 1] === 1
  }

  get flippableStones() {
    return []
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
