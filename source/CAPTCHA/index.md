---
layout: page # 必须
title: 验证码 # 必须，页面名称
description: TR管理系统验证码 # 页面二级标题，描述性文字
comments: false # 禁用评论，可选，默认开启
reward: false # 禁用打赏，可选，默认开启
date: 2022-07-22 13:46:44
---

<div id="shortHash" style="font-size:50px;text-align:center;"></div>
<script src="/js/object_hash.js" type="text/javascript"></script>
<script src="/js/moment.min.js" type="text/javascript"></script>
<script>
    setInterval(() => {
        const str = moment().format('YYYY-MM-DD HH')
        const hash = objectHash.sha1(str);
        const shortHash = hash.slice(0,7).toLocaleUpperCase()
        document.getElementById('shortHash').innerText = shortHash;
    }, 1000)
</script>
