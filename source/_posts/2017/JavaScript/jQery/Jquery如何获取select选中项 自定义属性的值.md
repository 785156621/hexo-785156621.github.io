---
title: Jquery如何获取select选中项 自定义属性的值
tags:
  - jQuery
url: 87.html
id: 87
categories:
  - jQuery
date: 2017-07-31 16:30:10
---

html:

<select id="status">
   <option value="1" data-type="1">启用</option>
   <option value="2" data-type="2">禁用</option>
<select>

jquery:

$("#status").on("change",function(e,o){
   var type = **$(this).find("option:selected").data("type");**
   alert(type)
});