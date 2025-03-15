<template>
  <div id="app">
    <header>
      <h1>中国近代高等院校分布与关系图</h1>
    </header>
    <main>
      <UniversityMap />
    </main>
  </div>
</template>

<script>
import UniversityMap from './components/UniversityMap.vue'

export default {
  name: 'App',
  components: {
    UniversityMap
  }
}
</script>

<style>
#app {
  font-family: "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 20px;
}

header {
  margin-bottom: 30px;
}

h1 {
  color: #34495e;
  font-size: 2em;
}

main {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
