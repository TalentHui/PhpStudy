# 变量

----
###### 1、不适用额外变量实现变量值交换
```php
<?php
list($a, $b) = array($b = 1, $a = 2);
?>
```

###### 2、动态创建变量名
```php
<?php
$animal = 'wabbit';
$wabbit = 'like';

// $animal = wabbit; $$animal == $wabbit
echo $$animal;   // like

?>
```

###### 3、在进程间共享变量
- 方案：
   1. [shmop](http://php.net/manual/zh/book.shmop.php)
   2. [System V](http://php.net/manual/zh/book.sem.php)
   
- shmop 示例
```php
<?php
function save_cache($data, $name, $timeout) {
    // delete cache
    $id=shmop_open(get_cache_id($name), "a", 0, 0);
    shmop_delete($id);
    shmop_close($id);
    
    // get id for name of cache
    $id=shmop_open(get_cache_id($name), "c", 0644, strlen(serialize($data)));
    
    // return int for data size or boolean false for fail
    if ($id) {
        set_timeout($name, $timeout);
        return shmop_write($id, serialize($data), 0);
    }
    else return false;
}

function get_cache($name) {
    if (!check_timeout($name)) {
        $id=shmop_open(get_cache_id($name), "a", 0, 0);

        if ($id) $data=unserialize(shmop_read($id, 0, shmop_size($id)));
        else return false;          // failed to load data

        if ($data) {                // array retrieved
            shmop_close();
            return $data;
        }
        else return false;          // failed to load data
    }
    else return false;              // data was expired
}

function get_cache_id($name) {
    // maintain list of caches here
    $id=array(  'test1' => 1
                'test2' => 2
                );

    return $id[$name];
}

function set_timeout($name, $int) {
    $timeout=new DateTime(date('Y-m-d H:i:s'));
    date_add($timeout, date_interval_create_from_date_string("$int seconds"));
    $timeout=date_format($timeout, 'YmdHis');

    $id=shmop_open(100, "a", 0, 0);
    if ($id) $tl=unserialize(shmop_read($id, 0, shmop_size($id)));
    else $tl=array();
    shmop_delete($id);
    shmop_close($id);

    $tl[$name]=$timeout;
    $id=shmop_open(100, "c", 0644, strlen(serialize($tl)));
    shmop_write($id, serialize($tl), 0);
}

function check_timeout($name) {
    $now=new DateTime(date('Y-m-d H:i:s'));
    $now=date_format($now, 'YmdHis');

    $id=shmop_open(100, "a", 0, 0);
    if ($id) $tl=unserialize(shmop_read($id, 0, shmop_size($id)));
    else return true;
    shmop_close($id);

    $timeout=$tl[$name];
    return (intval($now)>intval($timeout));
}
?>
```  

###### 4、把复杂的数据类型压缩到一个字符串中
```php
<?php
# serialize — 产生一个可存储的值的表示
# 保存时必须经过 addslashes() 的处理，主要是转义

# unserialize — 从已存储的表示中创建 PHP 的值
# 获取时必须经过 stripslashes() 的处理，主要是去除转义

# isSerialized  检查是否为序列化数据
?>
```

###### 5、将变量内容转为字符串
- 3种方式
   1. print_r($arr, true)
   2. var_export($arr, true)
   3. 缓冲区保存
```php
# 缓冲区保存
ob_start();
var_dump($arr = array);
$dump = ob_get_content;
ob_end_clean();
```      

###### 6、页面静态化
```php
<?php
$file_name = 'index.html';
if(file_exists( $file_name ) &&  filemtime( $file_name ) - time() < 10 ){//如果文件是存在并且最后修改时间小于设定时间 10s
    //filemtime( $file_name );//得到文件最后修改时间
    //time();//当前时间
    require_once( $file_name );//引入文件
}else{
    ob_start( );
    file_put_contents( $file_name,  ob_get_contents() );//输出到浏览器
}
?>
```