# 日期和时间

---
###### 1、month map
| China   |  English                     |
|:--------|:-----------------------------|
| 1       | January - Jan.
| 2       | February - Feb.
| 3       | March - Mar.
| 4       | April - Apr.
| 5       | May - May
| 6       | June - Jun.
| 7       | July - Jul.
| 8       | August - Aug.
| 9       | September - Sep. 或者 Sept.
| 10      | October - Oct.
| 11      | November - Nov.
| 12      | December - Dec.

###### 2、week map
| China   |  English                     |
|:--------|:-----------------------------|
| 周一    | Sunday  - Sun
| 周二    | Monday  - Mon
| 周三    | Tuesday  - Tue
| 周四    | Wednesday  - Wed
| 周五    | Thursday - Thur
| 周六    | Friday  - Fri
| 周日    | Saturday  - Sat

###### 3、获取当前日期和时间
```php
<?php
// 获取当前的时间和日期
print strftime('%c');  // Wed May 10 18:29:59 2006
print(date('r'));      // Wed, 10 May 2006 18:29:59 -0400

// 只要时间部分
var_dump(getdate());
array(
  'hours' => 18,           // 小时数            
  'minutes' => 23,         // 分钟数
  'seconds' => 45,         // 秒数
  'mon' => 1,              // 月份
  'year' => 2018,          // 年份, 数字(4位)
  'wday' => 0,             // 一周中的第几天, 数字值(周日是0, 周六是6)
  'mday' => 1,             // 一月中的第几天
  'yday' => 1,             // 一年中的第几天
  'weekday' => 'Friday',   // 文本
  'month' => 'january',    // 文本
);
var_dump(localtime());
array(
      '0' => 45,
      '1' => 23,
      '2' => 18,
);
?>
```

###### 4、验证日期
```php
<?php
checkdate($month = 12, $day = 3, $year = 2018); // 所有元素必须在当前时间之前
?>
```

###### 5、解析字符串获取时间戳
```php
<?php
strtotime('march 10');       // 今年3月10号0点时间戳

strtotime('last thursday');  // 上周三时间戳

strtotime('now + 3 months'); // 三个月后当前时间
?>
```

###### 6、解析日期
```php
<?php
// 设置默认时区
date_default_timezone_set('Asia/Shanghai');

$date_for = date('Y-m-d H:i:s');

preg_split('/[- :]/', $date_for);

array(
    "2018",
     "08",
     "12",
     "04",
     "00",
     "00"
);
?>
```