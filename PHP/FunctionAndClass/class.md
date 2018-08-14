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

###### 3、创建抽象的基类