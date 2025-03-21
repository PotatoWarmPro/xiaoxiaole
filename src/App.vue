<!-- App.vue -->
<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  errorCaptured(err, vm, info) {
    console.error('Error:', err, 'in:', info)
    return false
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
}
.btn {
  margin: 5px;
  padding: 8px 15px;
  border-radius: 4px;
  cursor: pointer;
}
</style>