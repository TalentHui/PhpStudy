# Number

---
###### 1、Float - 对浮点型数取整
```php
// 四舍五入
round(2.4);        // 2

// round() 可以接受一个可选的表示精度的参数
round(56.9415, 2); // 56.94

// 向上取整
ceil(2.4);         // 3

// 向下取整
floor(2.4);        // 2
```

###### 2、range — 根据范围创建数组，包含指定的元素
```php
/**
 * array range ( mixed $start , mixed $end [, number $step = 1 ] )
 *
 * 返回的数组中从 start 到 end （含 start 和 end）的单元。
 */
 
 <?php print_r( range( 24, 20 ) ); ?>
 Array
 (
     [0] => 24
     [1] => 23
     [2] => 22
     [3] => 21
     [4] => 20
 )
 
 <?php print_r( range( 20, 11, -3 ) ); ?>
 Array
 (
     [0] => 20
     [1] => 17
     [2] => 14
     [3] => 11
 )
```

###### 3、在一个范围内生成随机数
```php
// 生成一个大于等于 $lower 而 小于等于 $upper 的随机数
mt_rand($lower = 1, $upper = 10);
```

###### 4、生成有偏随机数
```php
/**
 * @desc 你想要根据每个广告活动未展示的剩余数目成比例地推出一系列网页横幅广告
 */
function pc_rand_weight(array $numbers = array())
{
    $total = 0;
    $distribution = array();
    
    foreach ($numbers as $number => $weight) {
        $total += $weight;
        $distribution[$number] = $total; 
    }
    
    $rand = mt_rand(0, $total - 1);
    
    foreach ($distribution as $number => $weights) {
            if ($rand < $weights) {
                return $number;
            }
    }
    
    return false;
}

$ads = array(
    'ford' => 12234,   // 广告客户 => 剩余展示数目 
    'att' => 33424,
    'ibm' => 16823,
);

$ad = pc_rand_weight($ads);
```

###### 5、取对数
```php
// 对于以 e 为底的对数 (自然log) , (使用 log() 函数)
$log = log(10);             // 2.30258092994

// 对于以 10 为底的对数 , (使用 log10() 函数)
$log10 = log10(10);         // 1

// 对于以 其他数 为底的对数 , 则将该底数作为第二个参数传递到log()函数中
$log2 = log(10, 2);         // 3.3219280948874
```

###### 6、指数计算
```php
// 你想计算一个数的幂，在计算某数的任何次方, 使用 pow()
$pow = pow(2, 10);             // 2 ^ 10 = 1024
```

###### 7、格式化数字
```php
number_format(float $number = 1234.56, int $decimals = 0 , string $dec_point = "." , string $thousands_sep = "," );
```

###### 8、格式化货币值
```php
$number = 1234.56;

// 国际化的货币格式
money_format('%i', $number);          // USD 1,234.56

// 本国货币
setlocale(LC_MONETARY, 'en_US');
money_format('%n', $number);          // $1,234.56
```

###### 9、不同进制间转换
```php
// base_convert() - 可以转换的进制在 2 ~ 36
$hex = 'a1';                             // 十六进制数 (base 16)
$decimal = base_convert($hex, 16, 10);   // 十六进制转十进制, $decimal 现在是十进制的 161

// 二进制 和 十进制相互转换
bindec(11011);
decbin(27);

// 八进制 和 十进制
octdec(33);
decoct(27);

// 十六进制 和 十进制
hexdec('1b');
dechex(27);
```