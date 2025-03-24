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
  // 初始化组件数据
  data() {
    return {
      rankingList: []
    }
  },
  // 组件挂载后加载排行榜数据
  mounted() {
    this.loadRanking()
  },
  methods: {
    // 从 localStorage 加载排行榜数据
    loadRanking() {
      const ranking = localStorage.getItem('ranking')
      this.rankingList = ranking ? JSON.parse(ranking) : []
    },
    // 将新的记录保存到排行榜并更新到 localStorage
    saveRanking(record) {
      this.rankingList.push(record)
      this.rankingList.sort((a, b) => b.score - a.score)
      localStorage.setItem('ranking', JSON.stringify(this.rankingList))
    }
  }
}
</script>