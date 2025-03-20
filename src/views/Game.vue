<template>
    <div class="game-container">
      <div class="game-header">
        <h2>玩家: {{ playerName }}</h2>
        <div class="score-board">
          <span>得分: {{ currentScore }}</span>
          <span>时间: {{ formattedTime }}</span>
        </div>
        <router-link to="/ranking" class="btn">查看排行榜</router-link>
      </div>
      
      <GameBoard 
        :boardSize="boardSize"
        @score-update="handleScoreUpdate"
      />
      
      <div class="game-controls">
        <button @click="pauseGame" class="btn">暂停</button>
        <router-link to="/" class="btn">返回首页</router-link>
      </div>
    </div>
  </template>
  
  <script>
  import GameBoard from '@/components/GameBoard.vue'
  
  export default {
    components: { GameBoard },
    data() {
      return {
        boardSize: 8,
        currentScore: 0,
        playerName: localStorage.getItem('playerName') || 'Guest',
        timer: 0,
        intervalId: null
      }
    },
    computed: {
      formattedTime() {
        const mins = Math.floor(this.timer / 60)
        const secs = this.timer % 60
        return `${mins}:${secs.toString().padStart(2, '0')}`
      }
    },
    mounted() {
      this.intervalId = setInterval(() => {
        this.timer++
      }, 1000)
    },
    beforeDestroy() {
      clearInterval(this.intervalId)
    },
    methods: {
      handleScoreUpdate(points) {
        this.currentScore += points
      },
      pauseGame() {
        if (this.intervalId) {
          clearInterval(this.intervalId)
          this.intervalId = null
        } else {
          this.intervalId = setInterval(() => {
            this.timer++
          }, 1000)
        }
      },
      saveGame() {
        // 保存游戏状态到localStorage
        const gameState = {
          score: this.currentScore,
          timer: this.timer,
          board: this.$refs.gameBoard.getBoardState()
        }
        localStorage.setItem('savedGame', JSON.stringify(gameState))
      }
    }
  }
  </script>