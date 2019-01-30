---
title: foreach 中 &的用法
tags:
  - PHP
url: 287.html
id: 287
categories:
  - PHP
date: 2019-01-30 15:25:39
---

例如有这样一个需求，要给数组添加一个新的元素。
这里的需求是统计商品的收入多少。就可以用到&。

```php
$pro_arr = array(
    array('price' =>10 , 'count' => 100),
    array('price' =>20 , 'count' => 90 )
);
```

1、第一种办法：

```php
foreach ($pro_arr as $key=>$val) {
    $pro_arr[$key]['total'] = $val['price']*$val['count'];
}
```

2、第二种办法：

```php
foreach ($pro_arr as &$val) {
    $val['total']=$val['price']*$val['count'];
}
```

```php
echo '<pre>';
print_r($pro_arr);
echo '</pre>';

Array
(
    [0] => Array
        (
            [price] => 10
            [count] => 100
            [total] => 1000
        )

    [1] => Array
        (
            [price] => 20
            [count] => 90
            [total] => 1800
        )

)
```
打印出来的效果是一样的。


本文转载自 https://blog.csdn.net/qq_38287952/article/details/79468321 