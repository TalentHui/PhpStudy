# DataType

---
###### 1、PHP一共支持 8 种数据类型
- 四种标量
   1. boolean      - 布尔型 
   2. integer      - 整形
   3. float/double - 浮点型
   4. string       - 字符串类型
- 两种符合类型
   1. array        - 数组
   2. object       - 对象
- 两种特殊类型
   1. resource     - 资源
   2. null         - 空值
   
###### 2、PHP 检测数据类型的函数列表
| 函数                 | 检测类型                         | 举例                                  |
|:-------------------|:---------------------------------|:--------------------------------------|
| is_bool             | 检测变量是否为布尔类型            | is_bool(true), is_bool(false)          |
| is_string           | 检测变量是否为字符串类型           | is_string('string'), is_string(12324) |
| is_integer/is_int   | 检测变量是否为整数                | is_integer(12), is_integer('12')      |
| is_float/is_double  | 检测变量是否为浮点类型             | is_float(3.1415), is_float('3.1415')  |
| is_array            | 检测变量是否为数组类型             | is_array($arr)                        |
| is_object           | 检测变量是否为一个对象类型         | is_object($obj)                        |
| is_null             | 检测变量是否为NULL                | is_null(null)                         |
| is_numeric          | 检测变量是否为数字或数字组成的字符串 | is_numeric('5'), is_numeric('bc110')  |