# Class

---
###### 1、class
```php
<?php
class user
{
    // 使用访问控制的目的是: OO编程的数据封装
    
    public $name_public;         // 在任何地方访问
    
    private $name_private;       // 当前类访问
    
    protected $name_protected;   // 在类和子类中访问
    
    /**
     * 对象构造器 
     * user constructor.
     */
    function __construct() {}
    
    /**
     * @desc   print new user; 时调用本方法，输出字符串 
     * @return string
     */
    public function __toString(){
        // TODO: Implement __toString() method.
        return '';
    } 
    
    /**
     * 对象解造器 
     * user constructor.
     */
    function __destruct() {}
}

// 实例化对象
$object = new user();

// 销毁对象
unset($object);
?>
```

###### 2、interface
```php
// 一个类实现了一个接口的所有方法，可以说它实现了这个接口
// 一个类未能实现接口中定义的所有方法，或者已不同的原型实现了这些方法，会导致PHP报出致命错误
<?php
interface Nameable
{
    public function getName();
    public function setName($name);
}

class Book implements Nameable
{
    private $name;
    
    public function getName()
    {
        return $this->name;
    }
    
    public function setName($name)
    {
        $this->namee = $name;
    }
}

// 接口中定义方法的原型，而不要去实现
// 继承接口的类需要实现这些方法

// 一个类是否实现了一个接口 - 函数检查
$interfaces = class_implements('Nameable');

if (isset($interfaces['Nameable'])) {
    echo 'yes';
}


// 一个类是否实现了一个接口 - 用反射类检查
$rc = new ReflectionClass('Book');

if ($rc->implementsInterface('Nameable')) {
    echo 'yes';
}
?>
```

###### 3、abstract - 创建抽象的基类
```php
抽象类可以作为子类公共基准的类

将类标记为 abstract

抽象类中必须定义一个方法(一个类中包含一个抽象方法，那么这个类必须声明为抽象类)。

和接口中方法相同，抽象方法不在抽象类中实现，而是在扩展这个抽象父类的子类中实现

抽象方法也是通过 abstract 定义

抽象方法的必要条件：
1、抽象方法不能定义为私有方法，因为他们需要被继承
2、抽象方法不能定义为最终方法，因为他们需要被覆盖
<?PHP
// 定义一个抽象类
abstract  class Databases
{
    abstract public function connect();
}

// 实现一个类
class MySQL extends Databases
{
    public function connect($host, $user, $pass, $db_name)
    {
        mysqli_connect($host, $user, $pass, $db_name);
    }
}
?>
```

###### 4、魔术方法
```php
<?php
class magic
{
    protected $object_current_class;
    
    public function __construct() {
        $this->object_current_class = new self();
    }
    
    /**
     * @desc  获取一个不存在的属性值时处罚   
     * @param $attr_name
     */
    public function __get($attr_name){
        // TODO: Implement __get() method.
    }

    /**
     * @desc  当给一个不存在的属性复赋值时触发 
     * @param $attr_name
     * @param $attr_value
     */
    public function __set($attr_name, $attr_value){
        // TODO: Implement __set() method.
    }


    /**
     * 当序列化一个类对象时调用此函数 - serialize()    
     */
    public function __wakeup(){
        // TODO: Implement __wakeup() method.
    }
    
    /**
     * f反序列化一个类对象时调用此函数 - unserialize
     */
    public function __sleep(){
        // TODO: Implement __sleep() method.
    }
    
    /**
     * #desc  当调用一个本类中不存在的方法时会调用次函数 
     * @param $function_name
     * @param $arguments
     * @return mixed
     */
    public function __call($function_name, $arguments)
    {
        if (method_exists($this->object_current_class, $function_name)) {
            return call_user_func_array(array($this->object_current_class, $function_name), $arguments);
        } else {
            echo "您所调用的方法不存在{$function_name}" . PHP_EOL;
        }
    }
}
?>
```

###### 5、分析一个对象
```php
使用反射 Reflaction 类来查明对象的信息如：

Reflection::export(new ReflectionClass('car'));

检测类方法如:
$car = new ReflectionClass('car');
if ($car->hasMehod('top')) {
    echo '存在';
}

<?php
    
?>
```

###### 6、动态类加载
```php
使用 _autoload() 魔术方法:
function __autolad($class_name) {
    include "{$class_name}.php";
}

$person = new_Persion;

Notice: 多次实例化一个类，不会多次调用 __autoload()
```

###### 7、判断类是否存在
```php
// return boolean

class_exists($class_name);
```

###### 8、返回由当前脚本中已定义类的名字组成的数组。
```php
get_declared_classes — 返回由已定义类的名字所组成的数组

array get_declared_classes ( void )

返回由当前脚本中已定义类的名字组成的数组。

<?php
    print_r(get_declared_classes());
?>


以上例程的输出类似于：

Array
(
    [0] => stdClass
    [1] => __PHP_Incomplete_Class
    [2] => Directory
)

----------------------------------------------------------------

如何判断类是用户定义还是系统定义
ReflectionClass::isUserDefined — 检查是否由用户定义的
public bool ReflectionClass::isUserDefined ( void )
检查一个类是否由用户定义，和内置相对。
返回值 - 成功时返回 TRUE， 或者在失败时返回 FALSE。

$internalclass = new ReflectionClass('ReflectionClass');

class Apple {}
$userclass = new ReflectionClass('Apple');

var_dump($internalclass->isUserDefined());
var_dump($userclass->isUserDefined());
```