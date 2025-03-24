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
      // 返回组件的数据对象
      return {
        rankingList: []
      }
    },
    mounted() {
      // 组件挂载后加载排行榜数据
      this.loadRanking()
    },
    methods: {
      loadRanking() {
        // 从本地存储加载排行榜数据
        const ranking = localStorage.getItem('ranking')
        this.rankingList = ranking ? JSON.parse(ranking) : []
      },
      saveRanking(record) {
        // 保存新的排行榜记录并更新本地存储
        this.rankingList.push(record)
        this.rankingList.sort((a, b) => b.score - a.score)
        localStorage.setItem('ranking', JSON.stringify(this.rankingList))
      }
    }
  }
  </script>