<!-- demo.vue -->
<template>
  <!-- time为时间戳 -->
  <div>{{time | formatDate}}</div>
  
  <!-- 结果为 2018-01-23 18:31:35 -->
</template>
<script type="text/ecmascript-6">
  export default {
     name: 'HelloWorld',
    data() {
      return {
       
        time: new Date()
      };
    },

    filters: {
      formatDate: function (value) {
        let date = new Date(value);
        let y = date.getFullYear();
        let MM = date.getMonth() + 1;
        MM = MM < 10 ? ('0' + MM) : MM;
        let d = date.getDate();
        d = d < 10 ? ('0' + d) : d;
        let h = date.getHours();
        h = h < 10 ? ('0' + h) : h;
        let m = date.getMinutes();
        m = m < 10 ? ('0' + m) : m;
        let s = date.getSeconds();
        s = s < 10 ? ('0' + s) : s;
        return y + '-' + MM + '-' + d + ' ' + h + ':' + m + ':' + s;
      }
    },
     //实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载，$el 还不可用。需要初始化处理一些数据时会比较有用
    created: function () {},
    //el挂载到实例上后调用，一般我们的第一个业务逻辑会在这里开始
    mounted: function () {
      var _this = this; //声明一个变量指向Vue实例this，保证作用域一致
      this.timer = setInterval(function () {
        _this.date = new Date(); //修改数据date
      }, 1000)
    },
    //实例销毁之前调用。主要解绑一些使用addEventListener监听的事件等
    beforeDestroy: function () {
      if (this.timer) {
        clearInterval(this.timer); //在Vue实例销毁前，清除我们的定时器
      }
    }
  };
</script>
<style>
 
</style>

