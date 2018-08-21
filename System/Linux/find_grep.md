# grep

---
###### 1、选项
| 选项  | 解释 
|:-----|:--------
|-a    |  * 不要忽略二进制数据。
|-A    |  <显示列数> 除了显示符合范本样式的那一行之外，并显示该行之后的内容。
|-b    |  在显示符合范本样式的那一行之外，并显示该行之前的内容。
|-c    |  只显示有多少行匹配，而不具体显示匹配的行。
|-C    |  * <显示列数>或-<显示列数>  除了显示符合范本样式的那一列之外，并显示该列之前后的内容。
|-d    |  * <进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作。
|-e    |  * <范本样式> 指定字符串作为查找文件内容的范本样式。
|-E    |  将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式。
|-f    |  <范本文件> 指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每一列的范本样式。
|-F    |  将范本样式视为固定字符串的列表。
|-G    |  将范本样式视为普通的表示法来使用。
|-h    |  不显示文件名。
|-H    |  在显示符合范本样式的那一列之前，标示该列的文件名称。
|-i    |  * 在字符串比较的时候忽略大小写。
|-l    |  只显示包含匹配模板的行的文件名清单。
|-L    |  列出文件内容不符合指定的范本样式的文件名称。
|-n    |  * 在每一行前面打印该行在文件中的行数。
|-q    |  不显示任何信息。
|-R    |  * /-r 如果文件参数是目录，该选项将递归搜索该目录下的所有子目录和文件。
|-s    |  不显示错误信息（不显示关于不存在或者无法读取文件的错误信息）。
|-v    |  * 反向检索，只显示不匹配的行。
|-w    |  只显示完整单词的匹配。
|-x    |  只显示完整行的匹配。
|-y    |  此参数效果跟“-i”相同。
|-o    |  只输出文件中匹配到的部分。

###### 2、退出状态
```text
grep退出状态：
0: 表示成功；
1: 表示在所提供的文件无法找到匹配的pattern；
2: 表示参数中提供的文件不存在。

见如下示例：
/> grep 'root' /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
/> echo $?
0

/> grep 'root1' /etc/passwd  #用户root1并不存在
/> echo $?
1

/> grep 'root' /etc/passwd1  #这里的/etc/passwd1文件并不存在
grep: /etc/passwd1: No such file or directory
/> echo $?
2
```

###### 3、实例
```text
1. grep最简单的用法，匹配一个词：grep word filename

2. 能够从多个文件里匹配：grep word filename1 filename2 filename3

3. 能够使用正則表達式匹配：grep -E pattern f1 f2 f3...

4. 假设须要显示行号，能够打开-n，例如以下：
www@ubuntu:command$ echo -e "1111\n2222\n33333\n44444" | grep -n -E "3"
3:33333

5. 打开递归搜索功能
www@ubuntu:command$ grep -n -R linux . 
./test2.txt:5:linux
./test1.txt:1:linux

6. 忽略大写和小写：-i
www@ubuntu:command$ echo "HELLO WORLD" | grep -i "hello"
HELLO WORLD

7. 匹配多个字符串模式
www@ubuntu:command$ echo "This is a line." | grep -e "This" -e "is" -e "line" -o
This
is
line
```

###### 4、--include and --exclude and --exclude-from
```text
#只在目录中所有的.php和.html文件中递归搜索字符"main()"

grep"main()" . -r --include *.{php,html}

#在搜索结果中排除所有README文件

grep"main()" . -r --exclude "README"

#在搜索结果中排除file_list文件列表里的文件

grep"main()" . -r --exclude-from file_list
```