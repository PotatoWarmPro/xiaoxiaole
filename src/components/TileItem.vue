<!-- TileItem.vue -->
<template>
    <div 
      class="tile"
      :style="{ backgroundColor: tileData.color }"
      @click="handleClick"
      :class="{ selected: tileData.selected }"
    ></div>
  </template>
   
  <script>
  export default {
    // 定义组件的属性，其中 tileData 是必需的对象类型属性
    props: {
      tileData: {
        type: Object,
        required: true
      }
    },
    // 定义组件的方法
    methods: {
      // 处理点击事件的方法，当点击时触发 'tile-select' 事件并将 tileData 作为参数传递
      handleClick() {
        this.$emit('tile-select', this.tileData);
      }
    }
  }
  </script>
   
  <style>
  // 定义 tile 类的样式，用于展示每个图块的基本样式信息
  .tile {
    display: inline-block;
    width: 50px;
    height: 50px;
    margin: 2px;
    cursor: pointer;
    transition: transform 0.2s;
    border-radius: 4px;
  }
   
  // 定义 tile 被选中时的样式，通过添加 selected 类来实现缩放和阴影效果
  .tile.selected {
    transform: scale(0.9);
    box-shadow: 0 0 10px rgba(0,0,0,0.5);
  }
  </style>