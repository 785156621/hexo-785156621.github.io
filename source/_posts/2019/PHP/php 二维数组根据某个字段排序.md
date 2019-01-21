---
title: php 二维数组根据某个字段排序
tags:
  - PHP
url: 287.html
id: 287
categories:
  - PHP
date: 2019-01-17 17:22:39
---

```php
/**
 * 二维数组根据某个字段排序
 * @param array $array 要排序的数组
 * @param string $keys   要排序的键字段
 * @param string $sort  排序类型  SORT_ASC     SORT_DESC
 * @return array 排序后的数组
 */
if (function_exists('array_sorting') === false) {

    function array_sorting($array, $keys, $sort = SORT_DESC)
    {
        $keysValue = [];
        foreach ($array as $k => $v) {
            $keysValue[$k] = $v[$keys];
        }
        array_multisort($keysValue, $sort, $array);
        return $array;
    }
}
```

相关链接：[https://www.cnblogs.com/dcb3688/p/4608004.html](https://www.cnblogs.com/dcb3688/p/4608004.html)
&emsp;&emsp;&emsp;&emsp;&emsp;[https://www.cnblogs.com/M-D-Luffy/p/4224127.html](https://www.cnblogs.com/M-D-Luffy/p/4224127.html)