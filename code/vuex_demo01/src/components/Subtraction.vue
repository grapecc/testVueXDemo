<template>
  <div>
    <h3>当前count的值为:{{count}}</h3>
    <button @click="clickSub">-1</button>
    <button @click="clickSubN(3)">-3</button>
    <button @click="clickAsyncSub">async -1</button>
    <button @click="clickAsyncSubN(3)">async -3</button>
  </div>
</template>

<script>
import {mapState ,mapMutations,mapActions } from 'vuex'
export default {
  name: "Subtraction",
  data () {
    return {}
  },
  computed: {
    //count 第二种方法
    ...mapState(['count'])
  },
  methods: {
    //触发 mutations的第一种方式
    ...mapMutations(['sub','subN']),
    ...mapActions(['subAsync', 'subAsyncN']),
    clickSub(){
      this.sub()
    },
    clickSubN(step){
      this.subN(step)
    },
    clickAsyncSub(){
      this.subAsync()
    },
    clickAsyncSubN(step){
      this.subAsyncN(step)
    }
  }
}
</script>

<style scoped>

</style>
