# Function

---
###### 1、传递引用
```php
// Action: 把一个变量传递给函数，并希望保留在函数内部对该变量的修改

<?php
function wrap_html_tag(&$string, $tag = 'b')
{
    $string = "<$tag>$string</$tag>";
}
?>
```

###### 2、使用命名的参数
```php
// Action: 让函数只接受一个参数，但该参数是一个关联数组
<?php
function image($img)
{
    // 为参数指定默认值
    if (!isset($img['src'])) $img['src'] = 'cow.png';
}

// 也可以先指定好默认值，走替换路线
function image_default($img, $defaults)
{
    $pack_img = array();
    
    foreach ($defaults as $key => $val) {
        $pack_img[$key] = isset($img[$key]) ? $img[$key] : $val;
    }
    
    return $pack_img;
}
?>
```

###### 3、接受个数可变的参数的函数
```php
<?php
function mean()
{
    // 传递到函数的参数个数
    $size = func_num_args();
    
    // 迭代便利所有参数
    for ($index = 0; $index < $size; $index++) {
        print func_get_arg($index);
    }
}
?>
```

###### 4、跳跃选择返回，最有效的方法
```php
<?php
$fh = fopen('./text.csv', 'r');
while (list(,,$rank,,) = fgetcsv($fh, 4096)) {
    print "$rank\n";
}
?>
```

###### 5、call_user_func和call_user_func_array
```php
<?php
function a($b,$c)   
{  
echo $b;  
echo $c;  
}  

call_user_func('a', "111","222");

class a {  
    function b($c)   
    {  
        echo $c;  
    }  
}  

call_user_func(array("a", "b"),"111");

// 将多个命令映射到同一个函数，用长短命名来调用函数
$dispatch = array(
   'add' => 'do_add',
   'commit' => 'do_commit',
   'ci' => 'do_commit' 
);

call_user_func_array($dispatch['add'], array());
?>
```

###### 6、函数内部访问全局变量
```php
<?php
$new_count = 'globals';

function globals_1 ()
{
    global $new_count;
    echo $new_count;
}

function globals_2 ()
{
    echo $GLOBALS['new_count'];
}
?>
```

###### 7、创建动态函数
```php
<?php
$add = create_function('$i,$j', 'return $i + $j;');
$add(1, 1);
?>
```