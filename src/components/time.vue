<template>
    <div id="app">
       
        <h1>  {{ date | formatDate }}</h1>
    </div>
</template>
 
<script>
export default {
  name: "Time",
  data() {
    return {
      date: ""
    };
  },
  
  //实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载，$el 还不可用。需要初始化处理一些数据时会比较有用
  created: function() {},
  //el挂载到实例上后调用，一般我们的第一个业务逻辑会在这里开始
  mounted: function() {
    var _this = this; //声明一个变量指向Vue实例this，保证作用域一致
    this.timer = setInterval(function() {
      _this.date = new Date(); //修改数据date
      /* alert(_this.date) */
    }, 1000);
  },
  //实例销毁之前调用。主要解绑一些使用addEventListener监听的事件等
  beforeDestroy: function() {
    if (this.timer) {
      clearInterval(this.timer); //在Vue实例销毁前，清除我们的定时器
    }
  },
  filters: {
    formatDate: function(value) {
      //在月份、日期、小时等小于10前面补0
      var padDate = function(value) {
        return value < 10 ? "0" + value : value;
      };
      var date = new Date(value);
      var hours = padDate(date.getHours());
      var minutes = padDate(date.getMinutes());
      var seconds = padDate(date.getSeconds());
      return hours + ":" + minutes + ":" + seconds;
    }
  },
};
</script>


