<template>
  <div id="app">
    <h1>消消乐游戏</h1>
    <GameBoard />
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue';

export default {
  components: {
    GameBoard
  },
  errorCaptured(err, vm, info) {
    console.error('捕获到错误：', err, '在：', info);
    return false;  // 返回 false 以阻止错误继续向上传播
  }
}
</script>

<style>
#app {
  text-align: center;
}
</style>
