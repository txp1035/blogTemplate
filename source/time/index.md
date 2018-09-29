---
layout: page # 必须
title: 倒计时 # 必须，页面名称
description: 一年倒计时 # 页面二级标题，描述性文字
comments: false # 禁用评论，可选，默认开启
reward: false # 禁用打赏，可选，默认开启
date: 2018-01-31 13:48:15
---

<div id="timeDiff" style="font-size:50px;text-align:center;"></div>
<script>
    function getTimeDiff(millisecond) {
        let day = millisecond / (1000 * 60 * 60 * 24)
        let hours = millisecond / (1000 * 60 * 60)
        let seconds = millisecond / (1000 * 60)
        let minutes = millisecond / 1000
        let str = Math.floor(day) + '天' + Math.floor(hours) % 24 + '小时' + Math.floor(seconds) % 60 + '分钟' + Math.floor(minutes) % 60 + '秒'
        return str;
    }
    setInterval(() => {
        let nowDate = new Date();
        let newDate = nowDate.getFullYear() + 1;
        let nextDate = new Date(newDate.toString() + '/1/1 0:0:0');
        let millisecond = nextDate.getTime() - nowDate.getTime();
        let timeDiff = getTimeDiff(millisecond);
        document.getElementById('timeDiff').innerText = timeDiff;
    }, 1000)
</script>
