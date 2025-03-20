<template>
  <div class="game-board-container">
    <div class="game-board">
      <div 
        v-for="(row, rowIndex) in board" 
        :key="rowIndex" 
        class="row"
      >
        <Tile
          v-for="(tile, colIndex) in row"
          :key="colIndex"
          :tile-data="tile"
          @tile-select="handleTileSelect"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Tile from './TileItem.vue'

export default {
  components: { Tile },
  props: ['boardSize'],
  data() {
    return {
      board: [],
      selectedTiles: [],
      colors: ['#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FFEEAD'],
      gameState: null
    }
  },
  created() {
    this.initializeBoard()
    this.loadSavedGame()
  },
  methods: {
    areAdjacent(tile1, tile2) {
  const dx = Math.abs(tile1.x - tile2.x)
  const dy = Math.abs(tile1.y - tile2.y)
  return (dx === 1 && dy === 0) || (dx === 0 && dy === 1)
},

removeTiles(tile1, tile2) {
  this.board[tile1.x][tile1.y] = null
  this.board[tile2.x][tile2.y] = null
},

applyGravity() {
  // 实现下落逻辑
  for (let col = 0; col < this.boardSize; col++) {
    let emptyRow = this.boardSize - 1
    for (let row = this.boardSize - 1; row >= 0; row--) {
      if (this.board[row][col]) {
        [this.board[emptyRow][col], this.board[row][col]] = 
          [this.board[row][col], this.board[emptyRow][col]]
        emptyRow--
      }
    }
  }
},
getBoardState() {
  return JSON.parse(JSON.stringify(this.board))
},
fillEmptyTiles() {
  // 填充新方块
  for (let i = 0; i < this.boardSize; i++) {
    for (let j = 0; j < this.boardSize; j++) {
      if (!this.board[i][j]) {
        this.board[i][j] = this.createTile(i, j)
      }
    }
  }
}
  }
}
</script>