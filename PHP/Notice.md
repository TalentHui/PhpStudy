# 常用的检测函数注意点

---
###### 本文函数列表
- [isset] {#1}

###### [isset() - 检测变量是否已设置并且非 NULL](#1)
```php
<?php
// bool isset ( mixed $var [, mixed $... ] )
// 返回值 - 如果 var 存在并且值不是 NULL 则返回 TRUE，否则返回 FALSE。

$a = "test";
$b = "name";

var_dump(isset($a));      // TRUE
var_dump(isset($a, $b));  // TRUE

unset ($a);

var_dump(isset($a));     // FALSE
var_dump(isset($a, $b)); // FALSE

$foo = NULL;
var_dump(isset($foo));   // FALSE
?>
```