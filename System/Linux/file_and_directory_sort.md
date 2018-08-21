# sort

---
| 选项  | 解释 
|:-----|:--------
|-b    | 忽略每行前面开始出的空格字符；
|-c    | 检查文件是否已经按照顺序排序；
|-d    | 排序时，处理英文字母、数字及空格字符外，忽略其他的字符；
|-f    | 排序时，将小写字母视为大写字母；
|-i    | 排序时，除了040至176之间的ASCII字符外，忽略其他的字符；
|-m    | 将几个排序号的文件进行合并；
|-M    | 将前面3个字母依照月份的缩写进行排序；
|-n    | * 依照数值的大小排序；
|-o    | <输出文件> 将排序后的结果存入制定的文件；
|-r    | * 以相反的顺序来排序；
|-t    | * <分隔字符> 指定排序时所用的栏位分隔字符；
|-k    | * 是指定需要爱排序的栏位
|+     | <起始栏位>-<结束栏位>：以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。

###### 实例
```text
sort将文件/文本的每一行作为一个单位，相互比较，比较原则是从首字符向后，依次按ASCII码值进行比较，最后将他们按升序输出。

[root@mail text]# cat sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5
eee:50:5.5

[root@mail text]# sort sort.txt
aaa:10:1.1
bbb:20:2.2
ccc:30:3.3
ddd:40:4.4
eee:50:5.5
eee:50:5.5

忽略相同行使用-u选项或者uniq：

[root@mail text]# cat sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5
eee:50:5.5

[root@mail text]# sort -u sort.txt
aaa:10:1.1
bbb:20:2.2
ccc:30:3.3
ddd:40:4.4
eee:50:5.5

或者

[root@mail text]# uniq sort.txt
aaa:10:1.1
ccc:30:3.3
ddd:40:4.4
bbb:20:2.2
eee:50:5.5

sort的-n、-r、-k、-t选项的使用：

[root@mail text]# cat sort.txt
AAA:BB:CC
aaa:30:1.6
ccc:50:3.3
ddd:20:4.2
bbb:10:2.5
eee:40:5.4
eee:60:5.1

#将BB列按照数字从小到大顺序排列：
[root@mail text]# sort -nk 2 -t: sort.txt
AAA:BB:CC
bbb:10:2.5
ddd:20:4.2
aaa:30:1.6
eee:40:5.4
ccc:50:3.3
eee:60:5.1

#将CC列数字从大到小顺序排列：
[root@mail text]# sort -nrk 3 -t: sort.txt
eee:40:5.4
eee:60:5.1
ddd:20:4.2
ccc:50:3.3
bbb:10:2.5
aaa:30:1.6
AAA:BB:CC

# -n是按照数字大小排序，-r是以相反顺序，-k是指定需要爱排序的栏位，-t指定栏位分隔符为冒号
```
