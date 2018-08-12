# 常用的检测函数注意点

---
###### 本文函数列表
- isset
- empty

###### 1、isset() - 检测变量是否已设置并且非 NULL
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

###### 2、empty() - 检查一个变量是否为空
```php
<?php 
// bool empty ( mixed $var )
// 判断一个变量是否被认为是空的。当一个变量并不存在，或者它的值等同于FALSE，那么它会被认为不存在。如果变量不存在的话，empty()并不会产生警告。
//
// 返回值 - 当var存在，并且是一个非空非零的值时返回 FALSE 否则返回 TRUE. 以下的东西被认为是空的：
// >> "" (空字符串)
// >> 0 (作为整数的0)
// >> 0.0 (作为浮点数的0)
// >> "0" (作为字符串的0)
// >> NULL
// >> FALSE
// >> array() (一个空数组)
// >> $var; (一个声明了，但是没有值的变量)

?>
```