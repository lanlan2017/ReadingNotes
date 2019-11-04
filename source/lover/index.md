---
title: sweetheart
date: 2019-10-16 10:49:05
type: "lover"
comments: false
---
## 纪念日 ##
2017-3-1
## 生日 ##
农历6月20日
## 备忘录 ##
- 12月26日 星期六 上午8点50学术交流中心第一会议室，佩戴党徽
- 12月26日 星球六 下午河海大学代替参见论坛
- 12月28日 星期一 图书馆续借,
- 12月28日 去西安和其他学校的支部交流.
- 12月27日 易烊千玺新电影(待定)

## 计算 ##
<div id='show' style="text-align:center"></div>
<script>function timeFn() {var dateBegin = Date.parse("2017-3-1");var dateEnd = new Date();var dateDiff = dateEnd.getTime() - dateBegin;var dayDiff = Math.floor(dateDiff / (24 * 3600 * 1000));var leave1 = dateDiff % (24 * 3600 * 1000);var hours = Math.floor(leave1 / (3600 * 1000));var leave2 = leave1 % (3600 * 1000);var minutes = Math.floor(leave2 / (60 * 1000));var leave3 = leave2 % (60 * 1000);var seconds = Math.round(leave3 / 1000);var leave4 = leave3 % (60 * 1000);var timeFn = "酸臭味持续了:" + dayDiff + "天" + hours + "小时" + minutes + "分钟" + seconds + "秒";document.getElementById('show').innerText = timeFn;}setInterval("timeFn();", 1000);</script>
<div style="display: none;">
## 源码 ##
```html
<div id='show' style="text-align:center"></div>
<script>
    // 计算两个时间差 dateBegin 开始时间
    function timeFn() {
        // 预制时间
        var dateBegin = Date.parse("2017-3-1");
        //获取当前时间
        var dateEnd = new Date();
        //时间差的毫秒数
        var dateDiff = dateEnd.getTime() - dateBegin;
        //计算出相差天数
        var dayDiff = Math.floor(dateDiff / (24 * 3600 * 1000));
        //计算天数后剩余的毫秒数
        var leave1 = dateDiff % (24 * 3600 * 1000)
        //计算出小时数
        var hours = Math.floor(leave1 / (3600 * 1000))
        //计算小时数后剩余的毫秒数
        var leave2 = leave1 % (3600 * 1000)
        //计算相差分钟数
        var minutes = Math.floor(leave2 / (60 * 1000))
        //计算分钟数后剩余的毫秒数
        var leave3 = leave2 % (60 * 1000)
        //计算相差秒数
        var seconds = Math.round(leave3 / 1000)
        //计算分钟数后剩余的毫秒数
        var leave4 = leave3 % (60 * 1000)
        // 毫秒数
        var minseconds = Math.round(leave4 / 1000)
        // 拼接字符串.
        var timeFn = "酸臭味持续了:" + dayDiff + "天" + hours + "小时" + minutes + "分钟" + seconds + "秒" + minseconds + "毫秒";
        // 更新dom
        document.getElementById('show').innerText = timeFn;
    }
    setInterval("timeFn();", 1000);
</script>
```
</div>