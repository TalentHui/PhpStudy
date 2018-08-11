# String

---
###### 1、什么是字符串
PHP中的字符串指的是字符的序列。是二进制安全的而且可以随意加长或者缩短，大小的唯一限制就是PHP可用的内存数量。

###### 2、单引号为什么速度快
因为PHP不会检查单引号字符串中的插入变量及任何转义序列

###### 3、双引号字符串转义序列
| 转义序列   | 字符 
|:----------|:---------------------
|\n         | 换行符 (ASCII码10)
|\r         | 回车符 (ASCII码13)
|\t         | 制表符 (ASCII码9)
|\\         | 反斜杠
|\$         | 美元符号
|\"         | 双引号
|\0至\777   | 八进制数值
|\x0至\xFF  | 十六进制数值

###### 4、heredoc 可以识别所有的插入变量以及双引号字符串能够识别的转义序列
```php
$divClass = 'class1';
$ulClass = 'class2';
$listItem = ' The List Item ';

$html = <<< END
<div class="$divClass">
    <ul class="$ulClass">
    <li>$listItem</li>
</div>
END;

print $html;
```

###### 5、检查字符串中是否包含某个特定的子字符串 - strops()
```php
// 例如：确定字符串是否包含 WuHui

if (strpos($_POST['name'], 'WuHui') !== false) {
    echo 'yes';
}

// strpos 返回值为 bool|int
// 已找到 返回 false, 说明字符串中不包含你所要查找的字符串.
// 未找到 返回 下标(下标从0开始), int 类型, 如果你说要查找的字符串位于这个字符串的开始位置返回 0. 
```

###### 6、从字符串的一个特定位置开始，提取字符串的一部分 - substr() - return string
```php
// 例如：想获取表单中用户名的前八个字符

substr($string = $_POST['username'], $start = 0, $length = 8);

// $string 要查找的目标字符串 
// $start  开始的位置, 下标从 0 开始, 正数 从左向右 查, 负数 从右向左 查, abs($start) > (strlen($string) - 1) 返回 false
// $length 获取的长度, 正数 取右边的数, 负数 取左边的数
```

###### 7、替换子字符串 - substr_replace() - return string
```php
// 把字符串 $old_string 从 $start 开始到结尾处的所有字符串替换成 $new_substring
$new_string = substr_replace($old_string, $new_substring, $start);

// 把字符串 $old_string 从 $start 开始的 $length 个字符 替换成 $new_substring
$new_string = substr_replace($old_string, $new_string, $start, $length);
```

###### 8、按字或按字节来反转字符串
```php
// 按字节来反转字符串
print strrev('This is not a palindrome.');   // .emordnilap a ton si sihT

// 按字反转字符串
$s = "Once upon a time there was a turtle";
// 将字符串分解为独立的字
$words = explode(' ', $s);
// 反转这个字数组
$words = array_reverse($words);
// 重建反转后的字符串
$s = implode(' ', $words);
print $s;                                    // turtle. a was there time a upon Once
```

###### 逗号分隔的数据 - fputcsv() - fgetcav()
```php
$sales_data = array(
    array('2018-08-11', 12),
    array('2018-08-11', 13),
    array('2018-08-11', 14),
    array('2018-08-11', 15),
);

// 将数据写入文件
$fh = fopen('sales.csv', 'w') or die("can't open sales.csv");

foreach ($sales as $sales_line) {
    if (fputcsv($fh, $sales_line) === false) {
        die("Can't write CSV line");
    }
}

fclose($fh) or die("Can't close sales.csv");

// 输出CSV格式的数据，使用特殊的输出流 - php://output
$fh = fopen('php://output', 'w');

foreach ($sales as $sales_line) {
    if (fputcsv($fh, $sales_line) === false) {
        die("Can't write CSV line");
    }
}

fclose($fh);

// 把 CSV 格式的数据放到一个字符串
ob_start();
$fh = fopen('php://output', 'w') or die("can't open php://output");

foreach ($sales as $sales_line) {
    if (fputcsv($fh, $sales_line) === false) {
        die("Can't write CSV line");
    }
}

fclose($fh) or die("Can't close php://output");
$output = ob_get_contents();
$ob_end_clean();
```

###### 生成字段宽度固定的数据记录 - pack() or str_pad()
```php
$book1 = 'Elmer Gantry';
$book2 = 'Sinclair Lewis';
$book3 = 1927;

// A25 把其后的参数分别转换成一个25个字符长的以空格填充的字符串
pack('A25A15A4', $book1, $book2, $book3);

// 先截取 25 个长度的字符串, 然后用 . 把不足的用字符补全
str_pad(sub_str($book1, 0, 25), 25, '.');
```

###### 文本在特定长度处自动换行
```php
// 每行50个字符来自动将文本换行, 默认 \n 做分隔符
prit wordwrap($s, $line_length = 50, $sign = "\n");
```

###### 格式化字符 - pack() 和 unpack()
```php
// 把2进制数据保存到一个字符串中 - return string
$packed = pack('S4', 1974, 106, 28225, 32725);

// 使用unpack()从一个字符串中抽取二进制数据 - return array
$nums = unpack('S4', $packed);
```
| 格式化字符 | 数据类型 
|:----------|:---------------------
|a          | 无填充的字符串
|A          | 空格填充的字符串
|h          | 带符号的字符
|H          | 无符号的字符
|c          | 带符号的字符
|C          | 无符号的字符
|s          | 带符号的短整型类型 （16位，计算机字节序列）
|S          | 无符号的短整型类型 （16位，计算机字节序列）
|n          | 无符号的短整型类型 （16位，big endian字节序列）
|v          | 无符号的短整型类型 （16位，little endian字节序列）
|i          | 带符号的整数 （大小与字节序列同计算机相关）
|I          | 无符号的整数 （大小与字节序列同计算机相关）
|l          | 带符号的长整型数 （32位，计算机字节序列）
|L          | 无符号的长整型数 （32位，计算机字节序列）
|N          | 无符号的长整型数 （32位，big endian字节序列）
|V          | 无符号的长整型数 （32位，little endian字节序列）
|f          | 浮点类型 （大小和表示法同计算机相关）
|d          | 双精度型数 （大小和表示法同计算机相关）
|x          | 空字节
|X          | 倒退一个字节
|@          | 绝对位置以空值填充

###### 可下载的CSV
```php
$sales_data = array(
    array('2018-08-11', 12),
    array('2018-08-11', 13),
    array('2018-08-11', 14),
    array('2018-08-11', 15),
);

// 为 fputcsv 函数打开文件句柄
$output = fopen("php://output", 'w') or die("not open php://output");

// 告诉浏览器发送的是一个 CSV 文件
header('Content-Type: application/csv');
header('Content-Disposition: attachment; filename="sales.csv"');

// 输出表头
fputcsv($output, array('date', 'clock'));

// 输出每一行数据
foreach ($sales_data as $sales_line) {
        fputcsv($output, $sales_line);
}

fclose($output) or die("not close php://output");
```