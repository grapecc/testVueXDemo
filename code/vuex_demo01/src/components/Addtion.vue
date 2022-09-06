<template>
  <div>
<!--    <h3>当前count的值为:{{$store.state.count}}</h3>-->
    <h3>{{$store.getters.showNum}}</h3>
    <button @click="addNum">+1</button>
    <button @click="addNum2(3)">+3</button>
    <button @click="addNum1">Async +1</button>
    <button @click="addNum3(3)">Async +3</button>
  </div>
</template>

<script>
export default {
  name: "Addtion",
  data () {
    return {}
  },
  methods: {
    addNum(){ //count ++
      // this.$store.state.count++  // 完全不合法
      //触发 mutations的第一种方式
      this.$store.commit('add')
    },
    addNum2(step){
      this.$store.commit('addN',step)
    },
    addNum1(){
      this.$store.dispatch('addAsync')
    },
    addNum3(step){
      this.$store.dispatch('addAsync3',step)
    },
  }
}
</script>

<style scoped>

</style>
