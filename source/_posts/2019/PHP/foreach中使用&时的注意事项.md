---
title: foreach中使用&时的注意事项
tags:
  - PHP
url: 287.html
id: 287
categories:
  - PHP
date: 2019-01-30 18:25:39
---

先来看看下面这段代码：

```php
$arr = [111, 222, 333];
foreach ( $arr as &$value ) {
    var_dump($value);
}
foreach ( $arr as $value ) {
    var_dump($value);
}
```

运行结果：

```php
111
222
333
111
222
222
```

出现这种情况是因为在第一个foreach中，每次的循环都相当于：

`$value = &$arr[$i]; // $i 是$arr的索引`

第一个foreach完成后，$value并没有注销掉，到第二个foreach时，每次的循环都相当于：

`$value = $arr[$i]; // $i 是$arr的索引`

但`$value`在第一个foreach中被定义为了一个引用值`$value = &$arr[2]`，所以第二个foreach会更新`$arr[2]`的值。

所以，再次使用`$value`前需要`unset($value)`;

### 手册说明

可以很容易地通过在 $value 之前加上 & 来修改数组的元素。此方法将以引用赋值而不是拷贝一个值。

```php
$arr = array(1, 2, 3, 4);
foreach ($arr as &$value) {
    $value = $value * 2;
}
// $arr is now array(2, 4, 6, 8) 
unset($value); // 最后取消掉引用
```

$value 的引用仅在被遍历的数组可以被引用时才可用（例如是个变量）。以下代码则无法运行：

```php
foreach (array(1, 2, 3, 4) as &$value) {
    $value = $value * 2;
}
```

<div class="tip">
Warning
数组最后一个元素的 $value 引用在 foreach 循环之后仍会保留。建议使用 unset() 来将其销毁。
</div>

> Note:foreach 不支持用“@”来抑制错误信息的能力。