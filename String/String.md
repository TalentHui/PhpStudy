# String

---
###### 什么是字符串
PHP中的字符串指的是字符的序列。是二进制安全的而且可以随意加长或者缩短，大小的唯一限制就是PHP可用的内存数量。

###### 单引号为什么速度快
因为PHP不会检查单引号字符串中的插入变量及任何转义序列

###### 双引号字符串转义序列
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

###### heredoc 可以识别所有的插入变量以及双引号字符串能够识别的转义序列
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