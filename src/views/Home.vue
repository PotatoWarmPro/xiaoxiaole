<template>
    <div class="home-container">
      <h1>欢迎来到消消乐游戏</h1>
      <div class="start-form">
        <input 
          v-model="playerName" 
          placeholder="请输入玩家名称"
          class="name-input"
        >
        <button 
          @click="startGame" 
          class="btn start-btn"
          :disabled="!playerName"
        >
          开始游戏
        </button>
        <button
          v-if="hasSavedGame"
          @click="continueGame"
          class="btn continue-btn"
        >
          继续游戏
        </button>
      </div>
      <router-link to="/ranking" class="btn ranking-btn">查看排行榜</router-link>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        playerName: '',
        hasSavedGame: false
      }
    },
    mounted() {
      this.checkSavedGame();
    },
    methods: {
      checkSavedGame() {
        this.hasSavedGame = !!localStorage.getItem('savedGame');
      },
      startGame() {
        localStorage.setItem('playerName', this.playerName);
        localStorage.removeItem('savedGame');
        this.$router.push('/game');
      },
      continueGame() {
  const savedGame = JSON.parse(localStorage.getItem('savedGame'));
  if (savedGame) {
    localStorage.setItem('playerName', this.playerName);
    this.$router.push({ 
      path: '/game',
      query: { continue: true } // 添加继续游戏标识
    });
  }
}
    }
  }
  </script>
  
  <style>
  .home-container {
    padding: 2rem;
    max-width: 600px;
    margin: 0 auto;
  }
  
  .start-form {
    margin: 2rem 0;
  }
  
  .name-input {
    padding: 0.8rem;
    margin-bottom: 1rem;
    width: 100%;
    max-width: 300px;
    display: block;
    margin: 0 auto 1rem;
  }
  
  .btn {
    display: inline-block;
    padding: 0.8rem 1.5rem;
    margin: 0.5rem;
    background: #4ECDC4;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    text-decoration: none;
  }
  
  .btn:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  
  .continue-btn {
    background: #45B7D1;
  }
  </style>