<template>
    <div class="ranking-container">
      <h2>排行榜</h2>
      <div class="ranking-list">
        <div v-for="(record, index) in rankingList" :key="index" class="ranking-item">
          <span class="rank">{{ index + 1 }}</span>
          <span class="name">{{ record.name }}</span>
          <span class="score">{{ record.score }}</span>
          <span class="time">{{ record.time }}</span>
        </div>
      </div>
      <router-link to="/" class="btn">返回首页</router-link>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        rankingList: []
      }
    },
    mounted() {
      this.loadRanking()
    },
    methods: {
      loadRanking() {
        const ranking = localStorage.getItem('ranking')
        this.rankingList = ranking ? JSON.parse(ranking) : []
      },
      saveRanking(record) {
        this.rankingList.push(record)
        this.rankingList.sort((a, b) => b.score - a.score)
        localStorage.setItem('ranking', JSON.stringify(this.rankingList))
      }
    }
  }
  </script>