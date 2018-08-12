# ARRAY

---
###### 1、用一个整数范围来初始化数据
````php
<?php
$range = range($start = 1, $end = 5);
var_dump($range);

array(
    1,
    2,
    3,
    4,
    5,
);
?>
````

###### 2、指针操作 - 数组的内部指针是数组内部的组织机制，指向一个数组中的某个元素。
| Function             | DESC
|:---------------------|:------------------
|current()             | 取得目前指针位置的内容资料。
|key()                 | 读取目前指针所指向资料的索引值（键值）。
|next()                | 将数组中的内部指针移动到下一个单元。
|prev()                | 将数组的内部指针倒回一位。
|end()                 | 将数组的内部指针指向最后一个元素。
|reset()               | 将目前指针无条件移至第一个索引位置。

###### 3、each() - 返回当前元素的键名和键值，并将内部指针向前移动， 如果内部指针越过了数组的末端，则 each() 返回 FALSE。
```php
<?php
$people = array("Bill", "Steve", "Mark", "David");
print_r (each($people));

// 输出结果
// Array ( [1] => Bill [value] => Bill [0] => 0 [key] => 0 )

// 可以用来循环输出数组
$people = array("Bill", "Steve", "Mark", "David");

reset($people);

while (list($key, $val) = each($people))
{
  echo "$key => $val<br>";
}
// 在执行 each() 之后，数组指针将停留在数组中的下一个单元或者当碰到数组结尾时停留在最后一个单元。如果要再用 each 遍历数组，必须使用 reset()。
?>
```

###### 4、list() - 把数组中的值赋给一组变量
```php
<?php
// Warning: PHP 5 里，list() 从最右边的参数开始赋值； PHP 7 里，list() 从最左边的参数开始赋值。
// Notice：  list() 仅能用于数字索引的数组，并假定数字索引从 0 开始。
// 个人测试, 5.3版本以上输出无差别, 这里的 PHP5 可能是更早的版本
$info = array('coffee', 'brown', 'caffeine');

// 列出所有变量
list($drink, $color, $power) = $info;
echo "$drink is $color and $power makes it special.\n";
// coffee is brown and caffeine makes it special.  - php 5.3
// coffee is brown and caffeine makes it special.  - php 7.0
?>
```

###### 5、从数组中删除元素
```php
<?php
$array = array('3' => 1, 'foo' => 'apple', '5' => 'Fri', 'bar' => 'pro');

// 删除一个元素, 用 unset()
unset($array['3']);
unset($array['foo']);

// 删除多个不连续的元素，也使用 unset()
unset($array['3'], $array['bar']);

// 删除多个连续的元素, 使用 array_splice()
// splice 英 [splaɪs] n 胶接处，粘接处，铰接处；
array_splice($array, $offset = 0, $length = 4);

// 如果你想在数组中保留某个键值，并将值设为空 - 这意味着该元素任然存在，只是值设为空
$array['2'] = '';
?>
```

###### 6、array_splice() - 去掉数组中的某一部分并用其它值取代
```php
<?php
// array array_splice ( array &$input , int $offset [, int $length = count($input) [, mixed $replacement = array() ]] )
// 把 input 数组中由 offset 和 length 指定的单元去掉，如果提供了 replacement 参数，则用其中的单元取代。
// 注意 input 中的数字键名不被保留。
// Note: 如果 replacement 不是数组，会被 类型转换 成数组 (例如： (array) $replacement)。 当传入的 replacement 是个对象或者 NULL，会导致未知的行为出现。

$input = array("red", "green", "blue", "yellow");
array_splice($input, 2);
// $input is now array("red", "green")

$input = array("red", "green", "blue", "yellow");
array_splice($input, 1, -1);
// $input is now array("red", "yellow")

$input = array("red", "green", "blue", "yellow");
array_splice($input, 1, count($input), "orange");
// $input is now array("red", "orange")

$input = array("red", "green", "blue", "yellow");
array_splice($input, -1, 1, array("black", "maroon"));
// $input is now array("red", "green", "blue", "black", "maroon")

$input = array("red", "green", "blue", "yellow");
array_splice($input, 3, 0, "purple");
// $input is now array("red", "green", "blue", "purple", "yellow");
?>
```

###### 7、array_values() - 返回数组中所有的值
```php
<?php
// array array_values ( array $array )
// array_values() 返回 input 数组中所有的值并给其建立数字索引。

$array = array("size" => "XL", "color" => "gold");
print_r(array_values($array));

//输出：
//Array
//(
//    [0] => XL
//    [1] => gold
//)
?>
```

###### 8、array_keys() - 返回数组中部分的或所有的键名
```php
<?php
// array array_keys ( array $array [, mixed $search_value = null [, bool $strict = false ]] )
// array_keys() 返回 input 数组中的数字或者字符串的键名。
// 如果指定了可选参数 search_value，则只返回该值的键名。否则 input 数组中的所有键名都会被返回。

$array = array(0 => 100, "color" => "red");
print_r(array_keys($array));

$array = array("blue", "red", "green", "blue", "blue");
print_r(array_keys($array, "blue"));

$array = array("color" => array("blue", "red", "green"),
               "size"  => array("small", "medium", "large"));
print_r(array_keys($array));

// 输出：
// Array
// (
//     [0] => 0
//     [1] => color
// Array
// (
//     [0] => 0
//     [1] => 3
//     [2] => 4
// )
// Array
// (
//     [0] => color
//     [1] => size
// )
?>
```

###### 9、array_combine() - 创建一个数组，用一个数组的值作为其键名，另一个数组的值作为其值
```php
<?php
// array array_combine ( array $keys , array $values )
// 返回一个 array，用来自 keys 数组的值作为键名，来自 values 数组的值作为相应的值。
// 返回值 - 返回合并的 array，如果两个数组的单元数不同则返回 FALSE。

$a = array('green', 'red', 'yellow');
$b = array('avocado', 'apple', 'banana');
$c = array_combine($a, $b);

print_r($c);

//Array
//(
//    [green]  => avocado
//    [red]    => apple
//    [yellow] => banana
//)
?>
```

###### 10、array_merge() -  合并一个或多个数组
```php
<?php
// array array_merge ( array $array1 [, array $... ] )
// array_merge() 将一个或多个数组的单元合并起来，一个数组中的值附加在前一个数组的后面。返回作为结果的数组。
// 如果输入的数组中有相同的字符串键名，则该键名后面的值将覆盖前一个值。然而，如果数组包含数字键名，后面的值将不会覆盖原来的值，而是附加到后面。
// 如果只给了一个数组并且该数组是数字索引的，则键名会以连续方式重新索引。

$array1 = array("color" => "red", 2, 4);
$array2 = array("a", "b", "color" => "green", "shape" => "trapezoid", 4);
$result = array_merge($array1, $array2);
print_r($result);

//Array
//(
//    [color] => green
//    [0] => 2
//    [1] => 4
//    [2] => a
//    [3] => b
//    [shape] => trapezoid
//    [4] => 4
//)

$array1 = array();
$array2 = array(1 => "data");
$result = array_merge($array1, $array2);

// 别忘了数字键名将会被重新编号！
//
// Array
// (
//     [0] => data
// )
?>
```

###### 11、array_walk() - 使用用户自定义函数对数组中的每个元素做回调处理
```php
<?php
// bool array_walk ( array &$array , callable $callback [, mixed $userdata = NULL ] )
// 典型情况下 callback 接受两个参数。array 参数的值作为第一个，键名作为第二个。
// 将用户自定义函数 funcname 应用到 array 数组中的每个单元。
// array_walk() 不会受到 array 内部数组指针的影响。array_walk() 会遍历整个数组而不管指针的位置。
//
// 返回值    - 成功时返回 TRUE， 或者在失败时返回 FALSE。
// 错误／异常 - 如果 callback 函数需要的参数比给出的多，则每次 array_walk() 调用 callback 时都会产生一个 E_WARNING 级的错误。

$fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");

function test_alter(&$item1, $key, $prefix)
{
    $item1 = "$prefix: $item1";
}

function test_print($item2, $key)
{
    echo "$key. $item2<br />\n";
}

echo "Before ...:\n";
array_walk($fruits, 'test_print');

array_walk($fruits, 'test_alter', 'fruit');
echo "... and after:\n";

array_walk($fruits, 'test_print');

// Before ...:
// d. lemon
// a. orange
// b. banana
// c. apple
// ... and after:
// d. fruit: lemon
// a. fruit: orange
// b. fruit: banana
// c. fruit: apple
?>
```

###### 12、array_key_exists() - 检查数组里是否有指定的键名或索引
```php
<?php
// bool array_key_exists ( mixed $key , array $array )
// 数组里有键 key 时，array_key_exists() 返回 TRUE。 key 可以是任何能作为数组索引的值。

$search_array = array('first' => 1, 'second' => 4);
if (array_key_exists('first', $search_array)) {
    echo "The 'first' element is in the array";
}


//array_key_exists() 与 isset() 的对比
//isset() 对于数组中为 NULL 的值不会返回 TRUE，而 array_key_exists() 会。
$search_array = array('first' => null, 'second' => 4);

// returns false
isset($search_array['first']);

// returns true
array_key_exists('first', $search_array);

?>
```

###### 13、
```php
<?php

?>
```

###### 14、
```php
<?php

?>
```

###### 15、
```php
<?php

?>
```

###### 16、
```php
<?php

?>
```

###### 17、
```php
<?php

?>
```

###### 18、
```php
<?php

?>
```

###### 19、
```php
<?php

?>
```

###### 20、
```php
<?php

?>
```

###### 21、
```php
<?php

?>
```

###### 22、
```php
<?php

?>
```

###### 23、
```php
<?php

?>
```

###### 24、
```php
<?php

?>
```

###### 25、
```php
<?php

?>
```

###### 26、
```php
<?php

?>
```

###### 27、
```php
<?php

?>
```

###### 28、
```php
<?php

?>
```

###### 29、
```php
<?php

?>
```

###### 30、
```php
<?php

?>
```

###### 12、
```php
<?php

?>
```

###### 12、
```php
<?php

?>
```

###### 12、
```php
<?php

?>
```