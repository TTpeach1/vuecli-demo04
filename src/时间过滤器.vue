<template>
  <div>
    <h2>国内网站：粉丝数量:{{num|isNum('万')}}</h2>
    <h2>外国网站：粉丝数量:{{num|isNum('千')}}</h2>
    <hr>
    <h2>时间：{{time|isTime('-')}}</h2>
    <h2>时间：{{time|isTime('/')}}</h2>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  data(){
    return{
      num:1876986,
      time:1636450540055,
    }
  },
  filters:{
    isNum(num,a){
      if(a=='万'){return num/10000+a}
      else if(a=='千'){return num/1000+a}
    },
    isTime(time,b){
      if(b=='-'){return moment(time).format('yyyy-MM-DD')}
      else if(b=='/'){return moment(time).format('yyyy/MM/DD')}
    }
  }
}
</script>

<style>

</style>