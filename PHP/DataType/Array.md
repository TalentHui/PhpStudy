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

###### 13、array_replace — 使用传递的数组替换第一个数组的元素
```php
<?php
// array array_replace ( array $array1 , array $array2 [, array $... ] )
// array_replace() 函数使用后面数组元素相同 key 的值替换 array1 数组的值。
// 如果一个键存在于第一个数组同时也存在于第二个数组，它的值将被第二个数组中的值替换。
// 如果一个键存在于第二个数组，但是不存在于第一个数组，则会在第一个数组中创建这个元素。
// 如果一个键仅存在于第一个数组，它将保持不变。如果传递了多个替换数组，它们将被按顺序依次处理，后面的数组将覆盖之前的值。
// array_replace() 是非递归的：它将第一个数组的值进行替换而不管第二个数组中是什么类型。
// 返回值 - 返回一个数组。如果发生错误，将返回 NULL。

$base = array("orange", "banana", "apple", "raspberry");
$replacements = array(0 => "pineapple", 4 => "cherry");
$replacements2 = array(0 => "grape");

$basket = array_replace($base, $replacements, $replacements2);
print_r($basket);

// Array
// (
//     [0] => grape
//     [1] => banana
//     [2] => apple
//     [3] => raspberry
//     [4] => cherry
// )
?>
```

###### 14、向数组中压入元素 - array_unshift()  array_push() 
```php
<?php
// array_unshift() - 在数组开头插入一个或多个单元
// int array_unshift ( array &$array , mixed $value1 [, mixed $... ] )
// array_unshift() 将传入的单元插入到 array 数组的开头。注意单元是作为整体被插入的，因此传入单元将保持同样的顺序。所有的数值键名将修改为从零开始重新计数，所有的文字键名保持不变。

// array_push() - 将一个或多个单元压入数组的末尾（入栈）
// int array_push ( array &$array , mixed $value1 [, mixed $... ] )
// array_push() 将 array 当成一个栈，并将传入的变量压入 array 的末尾。array 的长度将根据入栈变量的数目增加。和如下效果相同：
?>
```

###### 15、向数组中弹出元素 - array_shift() array_pop()
```php
<?php
// array_shift — 将数组开头的单元移出数组
// mixed array_shift ( array &$array )
// array_shift() 将 array 的第一个单元移出并作为结果返回，将 array 的长度减一并将所有其它单元向前移动一位。所有的数字键名将改为从零开始计数，文字键名将不变。
// Note: 使用此函数后会重置（reset()）array 指针。

// array_pop — 弹出数组最后一个单元（出栈）
// mixed array_pop ( array &$array )
// array_pop() 弹出并返回 array 数组的最后一个单元，并将数组 array 的长度减一。
// Note: 使用此函数后会重置（reset()）array 指针。
?>
```

###### 16、array_map — 为数组的每个元素应用回调函数
```php
<?php
// array array_map ( callable $callback , array $array1 [, array $... ] )
// array_map()：返回数组，是为 array1 每个元素应用 callback函数之后的数组。 callback 函数形参的数量和传给 array_map() 数组数量，两者必须一样。

function cube($n)
{
    return($n * $n * $n);
}

$a = array(1, 2, 3, 4, 5);
$b = array_map("cube", $a);
print_r($b);

// 这使得 $b 成为：
// 
// Array
// (
//     [0] => 1
//     [1] => 8
//     [2] => 27
//     [3] => 64
//     [4] => 125
// )
?>
```

###### 17、array_pad — 以指定长度将一个值填充进数组
```php
<?php
// array array_pad ( array $array , int $size , mixed $value )
// array_pad() 返回 array 的一个拷贝，并用 value 将其填补到 size 指定的长度。如果 size 为正，则填补到数组的右侧，如果为负则从左侧开始填补。
// 如果 size 的绝对值小于或等于 array 数组的长度则没有任何填补。有可能一次最多填补 1048576 个单元。

$input = array(12, 10, 9);

$result = array_pad($input, 5, 0);
// result is array(12, 10, 9, 0, 0)

$result = array_pad($input, -7, -1);
// result is array(-1, -1, -1, -1, 12, 10, 9)

$result = array_pad($input, 2, "noop");
// not padded
?>
```

###### 18、in_array — 检查数组中是否存在某个值
```php
<?php
// bool in_array ( mixed $needle , array $haystack [, bool $strict = FALSE ] )
// 大海捞针，在大海（haystack）中搜索针（ needle），如果没有设置 strict 则使用宽松的比较。
?>
```

###### 19、array_search — 在数组中搜索给定的值，如果成功则返回首个相应的键名
```php
<?php
// mixed array_search ( mixed $needle , array $haystack [, bool $strict = false ] )
// 大海捞针，在大海（haystack）中搜索针（ needle 参数）。
// strict - 如果可选的第三个参数 strict 为 TRUE，则 array_search() 将在 haystack 中检查完全相同的元素。 这意味着同样严格比较 haystack 里 needle 的 类型，并且对象需是同一个实例。
// return - 如果找到了 needle 则返回它的键，否则返回 FALSE。
//        - 如果 needle 在 haystack 中出现不止一次，则返回第一个匹配的键。要返回所有匹配值的键

$array = array(0 => 'blue', 1 => 'red', 2 => 'green', 3 => 'red');

$key = array_search('green', $array); // $key = 2;
$key = array_search('red', $array);   // $key = 1;
?>
```

###### 20、字符串 和 数组转换
```php
<?php
// implode — 将一个一维数组的值转化为字符串
// join — 将一个一维数组的值转化为字符串
// string implode ( string $glue , array $pieces )
// glue   英 [glu:]  美 [ɡlu] n.胶水； 胶粘物； 粘聚力；
// pieces 英 ['pi:sɪz]  美 ['pisɪz] n.（尤指一套中的）一件( piece的名词复数 )； 片； 条
// 返回一个字符串，其内容为由 glue 分割开的数组的值。
$array = array('lastname', 'email', 'phone');
$comma_separated = implode(",", $array);

echo $comma_separated; // lastname,email,phone
// explode — 使用一个字符串分割另一个字符串
// array explode ( string $delimiter , string $string [, int $limit ] )
// delimiter 英 [dɪ'lɪmɪtə]  美 [dɪ'lɪmɪtə] n.定界符，分隔符；
// 此函数返回由字符串组成的数组，每个元素都是 string 的一个子串，它们被字符串 delimiter 作为边界点分割出来。
$input1 = "hello";
$input2 = "hello,there";
var_dump( explode( ',', $input1 ) );
var_dump( explode( ',', $input2 ) );

// 以上例程会输出：
// 
// array(1)
// (
//     [0] => string(5) "hello"
// )
// array(2)
// (
//     [0] => string(5) "hello"
//     [1] => string(5) "there"
// )
?>
```

###### 21、array_filter — 用回调函数过滤数组中的单元
```php
<?php
//array array_filter ( array $array [, callable $callback [, int $flag = 0 ]] )
//依次将 array 数组中的每个值传递到 callback 函数。如果 callback 函数返回 true，则 array 数组的当前值会被包含在返回的结果数组中。数组的键名保留不变。

function odd($var)
{
    // returns whether the input integer is odd
    return($var & 1);
}

function even($var)
{
    // returns whether the input integer is even
    return(!($var & 1));
}

$array1 = array("a"=>1, "b"=>2, "c"=>3, "d"=>4, "e"=>5);
$array2 = array(6, 7, 8, 9, 10, 11, 12);

echo "Odd :\n";
print_r(array_filter($array1, "odd"));
echo "Even:\n";
print_r(array_filter($array2, "even"));

//以上例程会输出：
//
// Odd :
// Array
// (
//     [a] => 1
//     [c] => 3
//     [e] => 5
// )
// Even:
// Array
// (
//     [0] => 6
//     [2] => 8
//     [4] => 10
//     [6] => 12
// )
?>
```

###### 22、获取数组中 最大值 和 最小值
```php
<?php
// max — 找出最大值
// mixed max ( array $values )
// mixed max ( mixed $value1 , mixed $value2 [, mixed $... ] )
// 如果仅有一个参数且为数组，max() 返回该数组中最大的值。如果第一个参数是整数、字符串或浮点数，则至少需要两个参数而 max() 会返回这些值中最大的一个。可以比较无限多个值。
// Note:
// PHP 会将非数值的 string 当成 0，但如果这个正是最大的数值则仍然会返回一个字符串。
// 如果多个参数都求值为 0 且是最大值，max() 会返回其中数值的 0，如果参数中没有数值的 0，则返回按字母表顺序最大的字符串。
echo max(1, 3, 5, 6, 7);  // 7
echo max(array(2, 4, 5)); // 5

// When 'hello' is cast as integer it will be 0. Both the parameters are equally
// long, so the order they are given in determines the result
echo max(0, 'hello');     // 0
echo max('hello', 0);     // hello

echo max('42', 3); // '42'

// min — 找出最小值
// mixed min ( array $values )
// mixed min ( mixed $value1 , mixed $value2 [, mixed $... ] )
// 如果仅有一个参数且为数组，min() 返回该数组中最小的值。如果给出了两个或更多参数, min() 会返回这些值中最小的一个。
// Note:
// PHP 会将非数值的 string 当成 0，但如果这个正是最小的数值则仍然会返回一个字符串。
// 如果多个参数都求值为 0 且是最小值，min() 会返回按字母表顺序最小的字符串，如果其中没有字符串的话，则返回数值的 0。
echo min(2, 3, 1, 6, 7);  // 1
echo min(array(2, 4, 5)); // 2

echo min(0, 'hello');     // 0
echo min('hello', 0);     // hello
echo min('hello', -1);    // -1
?>
```

###### 23、排序
| Type                  | Desc
|:----------------------|:---------------------------------------------------------------------------------------
| SORT_REGULAR          | 正常比较单元（不改变类型）
| SORT_NUMERIC          | 单元被作为数字来比较
| SORT_STRING           | 单元被作为字符串来比较
| SORT_LOCALE_STRING    | 根据当前的区域（locale）设置来把单元当作字符串比较，可以用 setlocale() 来改变。
| SORT_NATURAL          | 和 natsort() 类似对每个单元以“自然的顺序”对字符串进行排序。 PHP 5.4.0 中新增的。
| SORT_FLAG_CASE        | 能够与 SORT_STRING 或 SORT_NATURAL 合并（OR 位运算），不区分大小写排序字符串。

|函数名称	            |排序依据	    |数组索引键保持	                |排序的顺序	
|:------------------|:----------|:------------------------------|:-----------
|sort()	            |值	        |否	                             |由低到高
|rsort()	        |值	        |否	                             |由高到低
|asort()           	|值	        |是	                             |由低到高	                
|arsort()	        |值	        |是	                             |由高到低	                
|ksort()	        |键	        |是	                             |由低到高
|krsort()	        |键	        |是	                             |由高到低
|uasort()	        |值	        |是	                             |由用户定义
|usort()	        |值	        |否	                             |由用户定义
|uksort()	        |键	        |是	                             |由用户定义
|natsort()	        |值	        |是	                             |自然排序
|natcasesort()	    |值	        |是	                             |自然排序，大小写不敏感
|array_multisort()	|值	        |键值关联的保持，数字类型的不保持    |第一个数组或者由选项指定
|shuffle()	        |值	        |否	                             |随机	   

```php
<?php
//  usort() 例子
function cmp($a, $b)
{
    if ($a == $b) {
        return 0;
    }
    return ($a < $b) ? -1 : 1;
}

$a = array(3, 2, 5, 6, 1);

usort($a, "cmp");

foreach ($a as $key => $value) {
    echo "$key: $value\n";
}

// 以上例子输出：
//0: 1
//1: 2
//2: 3
//3: 5
//4: 6

// array_multisort — 对多个数组或多维数组进行排序
// bool array_multisort ( array &$array1 [, mixed $array1_sort_order = SORT_ASC [, mixed $array1_sort_flags = SORT_REGULAR [, mixed $... ]]] )
// array1             - 要排序的 array。
// array1_sort_order  - 之前 array 参数要排列的顺序。 SORT_ASC 按照上升顺序排序， SORT_DESC 按照下降顺序排序。
// 此参数可以和 array1_sort_flags 互换，也可以完全删除，默认是 SORT_ASC 。
// array1_sort_flags  - 为 array 参数设定选项：
// 
// array_multisort() 可以用来一次对多个数组进行排序，或者根据某一维或多维对多维数组进行排序。
// 关联（string）键名保持不变，但数字键名会被重新索引。
// 返回值 - 成功时返回 TRUE， 或者在失败时返回 FALSE。

$data[] = array('volume' => 67, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 1);
$data[] = array('volume' => 85, 'edition' => 6);
$data[] = array('volume' => 98, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 6);
$data[] = array('volume' => 67, 'edition' => 7);

// 取得列的列表
foreach ($data as $key => $row) {
    $volume[$key]  = $row['volume'];
    $edition[$key] = $row['edition'];
}

// 将数据根据 volume 降序排列，根据 edition 升序排列
// 把 $data 作为最后一个参数，以通用键排序
array_multisort($volume, SORT_DESC, $edition, SORT_ASC, $data);

//volume | edition
//-------+--------
//    98 |       2
//    86 |       1
//    86 |       6
//    85 |       6
//    67 |       2
//    67 |       7
?>
```

###### 24、array_reverse — 返回单元顺序相反的数组
```php
<?php
// array array_reverse ( array $array [, bool $preserve_keys = false ] )
// array        - 输入的数组。
//preserve_keys - 如果设置为 TRUE 会保留数字的键。 非数字的键则不受这个设置的影响，总是会被保留。
// array_reverse() 接受数组 array 作为输入并返回一个单元为相反顺序的新数组。

$input  = array("php", 4.0, array("green", "red"));
$reversed = array_reverse($input);
$preserved = array_reverse($input, true);

print_r($input);
print_r($reversed);
print_r($preserved);

//Array
//(
//    [0] => php
//    [1] => 4
//    [2] => Array
//        (
//            [0] => green
//            [1] => red
//        )
//
//)
//Array
//(
//    [0] => Array
//        (
//            [0] => green
//            [1] => red
//        )
//
//    [1] => 4
//    [2] => php
//)
//Array
//(
//    [2] => Array
//        (
//            [0] => green
//            [1] => red
//        )
//
//    [1] => 4
//    [0] => php
//)
?>
```

###### 25、array_unique — 移除数组中重复的值
```php
<?php
// array array_unique ( array $array [, int $sort_flags = SORT_STRING ] )
// array      - 输入的数组。
// sort_flags - 第二个可选参数sort_flags 可用于修改排序行为： 排序类型标记：
//     SORT_REGULAR - 按照通常方法比较（不修改类型）
//     SORT_NUMERIC - 按照数字形式比较
//     SORT_STRING - 按照字符串形式比较
//     SORT_LOCALE_STRING - 根据当前的本地化设置，按照字符串比较。
//
// array_unique() 接受 array 作为输入并返回没有重复值的新数组。
// 注意键名保留不变。array_unique() 先将值作为字符串排序，然后对每个值只保留第一个遇到的键名，接着忽略所有后面的键名。
// 这并不意味着在未排序的 array 中同一个值的第一个出现的键名会被保留。
// Note: 当且仅当 (string) $elem1 === (string) $elem2 时两个单元被认为相同。 例如，字符串表达一样时，会使用首个元素。

input = array(4, "4", "3", 4, 3, "3");
$result = array_unique($input);
var_dump($result);

// array(2) {
//   [0] => int(4)
//   [2] => string(1) "3"
// }
?>
```

###### 26、数组的交集、差集、并集
```php
<?php
// 交集 - array_intersect — 计算数组的交集
// array array_intersect ( array $array1 , array $array2 [, array $... ] )
// array_intersect() 返回一个数组，该数组包含了所有在 array1 中也同时出现在所有其它参数数组中的值。注意键名保留不变。

$array1 = array("a" => "green", "red", "blue");
$array2 = array("b" => "green", "yellow", "red");
$result = array_intersect($array1, $array2);
print_r($result);

//Array
//(
//    [a] => green
//    [0] => red
//)

// 差集 - array_diff — 计算数组的差集
// array array_diff ( array $array1 , array $array2 [, array $... ] )
// 对比 array1 和其他一个或者多个数字，返回在 array1 中但是不在其他 array 里的值。

$array1 = array("a" => "green", "red", "blue", "red");
$array2 = array("b" => "green", "yellow", "red");
$result = array_diff($array1, $array2);

print_r($result);

//Array
//(
//    [1] => blue
//)

// 并集 array_unique(array_merge($arr1 = array, [$arr1 = array, ...]))
?>
```

###### 27、提供像访问数组一样访问对象的能力的接口。
```php
ArrayAccess {
    /* 方法 */
    abstract public boolean offsetExists ( mixed $offset )
    abstract public mixed offsetGet ( mixed $offset )
    abstract public void offsetSet ( mixed $offset , mixed $value )
    abstract public void offsetUnset ( mixed $offset )
}

ArrayAccess::offsetExists — 检查一个偏移位置是否存在
ArrayAccess::offsetGet    — 获取一个偏移位置的值
ArrayAccess::offsetSet    — 设置一个偏移位置的值
ArrayAccess::offsetUnset  — 复位一个偏移位置的值

<?php
class TestArrayAccess implements ArrayAccess
{
    # 存储数据
    private $data = [];

    /**
     * 以对象的方式访问数组中的数据
     *
     * @param $key
     * @return mixed
     */
    public function __get($key)
    {
        return $this->data[$key];
    }

    /**
     * 以对象方式添加一个数组元素
     *
     * @param $key
     * @param $val
     */
    public function __set($key, $val)
    {
        $this->data[$key] = $val;
    }

    /**
     * 以对象方式判断数组元素是否设置
     *
     * @param $key
     * @return bool
     */
    public function __isset($key)
    {
        return isset($this->data[$key]);
    }

    /**
     * 以对象方式删除一个数组元素
     *
     * @param $key
     */
    public function __unset($key)
    {
        unset($this->data[$key]);
    }

    /**
     * @param mixed $offset
     * @return mixed|null
     */
    public function offsetGet($offset)
    {
        return $this->offsetExists($offset) ? $this->data[$offset] : null;
    }

    /**
     * @param mixed $offset
     * @param mixed $value
     */
    public function offsetSet($offset, $value)
    {
        if (is_null($offset)) {
            $this->data[] = $value;
        } else {
            $this->data[$offset] = $value;
        }
    }

    /**
     * @param mixed $offset
     * @return bool
     */
    public function offsetExists($offset)
    {
        return isset($this->data[$offset]);
    }

    /**
     * @param mixed $offset
     */
    public function offsetUnset($offset)
    {
        if ($this->offsetExists($offset)) {
            unset($this->data[$offset]);
        }
    }

    /**
     * @return array
     */
    public function &__invoke()
    {
        return $this->data;
    }
}
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

###### 31、
```php
<?php

?>
```

###### 32、
```php
<?php

?>
```

###### 33、
```php
<?php

?>
```