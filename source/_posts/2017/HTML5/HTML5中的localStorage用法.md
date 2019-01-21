---
title: HTML5中的localStorage用法
tags:
  - HTML5
url: 60.html
id: 60
categories:
  - HTML
date: 2017-07-20 22:28:01
---

存储数据的方法就是直接给window.localStorage添加一个属性，例如：window.localStorage.name 或者 window.localStorage\["name"\]。 1.设置setItem 2.读取getItem 3.删除removeItem 4.全部清除clear

        localStorage.name = 'jack';
        localStorage.getItem('name'); // jack
        localStorage.setItem('name','tom'); // 重新覆盖，变为了tom了
        localStorage.setItem('age','18');
        localStorage.getItem('name'); // tom
        localStorage.getItem('age');  // 18
        localStorage.removeItem('name');
        localStorage.getItem('name'); // 已经被清除了null
        localStorage.getItem('age');  // 18
        localStorage.clear();         // 清除了所有
        localStorage.getItem('age'); // null

需要注意的是：这里的存储不同意cookie，没有时间限制。