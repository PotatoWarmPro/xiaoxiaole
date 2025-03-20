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
    props: {
      tileData: {
        type: Object,
        required: true
      }
    },
    methods: {
      handleClick() {
        this.$emit('tile-select', this.tileData);
      }
    }
  }
  </script>
  
  <style>
  .tile {
    display: inline-block;
    width: 50px;
    height: 50px;
    margin: 2px;
    cursor: pointer;
    transition: transform 0.2s;
    border-radius: 4px;
  }
  
  .tile.selected {
    transform: scale(0.9);
    box-shadow: 0 0 10px rgba(0,0,0,0.5);
  }
  </style>