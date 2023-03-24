<template>
<div class="stopwatch__container">
  <stopwatch v-for="stopwatch in stopwatchCount" :key="stopwatch"></stopwatch>
  <button @click="stopwatchCount += 1;" class="add-wtopwatch__btn">+</button>
</div>
</template>

<script>
import stopwatch from './components/stopwatch.vue'

export default {
  data() {
    return {
      stopwatchCount: 1,
    }
  },
  methods: {

  },
  components: {
    stopwatch
  }
}
</script>

<style>
@import url('https://fonts.cdnfonts.com/css/gotham-pro');

body{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #353638;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 10%;
}
#app {
  font-family: 'Gotham Pro', sans-serif;
  color: white;
}
.stopwatch__container{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}
.add-wtopwatch__btn{
  background: #696969;
  border: 0;
  width: 225px;
  height: 120px;
  position: relative;
  font-size: 60px;
  color: #9E9E9E;
  transition: 0.1s;
  margin: 15px 15px;
}
.add-wtopwatch__btn:hover{
  background: #747474;
  color: #bdbdbd;
}
</style>
