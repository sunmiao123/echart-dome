<template>
  <div class="m-">
    <div class="left">
      <Left></Left>
    </div>
    <div class="right">
      <Right></Right>
    </div>
  </div>
</template>
<script>
import Left from '../components/left/index'
import Right from '../components/right/echarts'
export default {
  components:{
    Left,
    Right
  },
  data() {
    return {};
  },
  methods: {}
};
</script>
<style scoped>
* {
  padding: 0;
  margin: 0;
}
.m- {
  width: 100%;
  height: 100%;
  display: flex;
}
.left{
  flex: 1;
  height: 700px;
}
.right {
  flex: 9;
}
</style>