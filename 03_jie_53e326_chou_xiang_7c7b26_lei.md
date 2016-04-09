# 03 接口&抽象类&类

###什么是接口？
    1.接口中所有的方法都是抽象方法，用Interface来声明，
    2.接口是用来建立类与类之间的协议，它所提供的只是一种形式，而没有具体的实现。
    3.同时实现该接口的实现类必须要实现该接口的所有方法，通过使用implements关键字，他表示该类在遵循某个或某组特定的接口，接口可以继承接口，实现接口扩展，用extends来实现接口的扩展。
    4.这种抽象类中只包含抽象方法和静态常量。
    
###使用场景？
    1.多数据库驱动的时候，接口方法
    2.IOS中Tableview的数据源接口
    3.JAVA中的 Runable接口 和 listView的Adapter等等

###如何正确使用？
        1.个Interface的方所有法访问权限自动被声明为public。确切的说只能为public，当然你可以显示的声明为protected、private，但是编译会出错！
         2.接口中可以定义“成员变量”，或者说是不可变的常量，因为接口中的“成员变量”会自动变为为public static final。可以通过类命名直接访问：ImplementClass.name。
         3.接口中不存在实现的方法。
         4.实现接口的非抽象类必须要实现该接口的所有方法。抽象类可以不用实现。
         5.不能使用new操作符实例化一个接口，但可以声明一个接口变量，该变量必须引用（refer to)一个实现该接口的类的对象。可以使用 instanceof 检查一个对象是否实现了某个特定的接口。例如：if(anObject instanceof Comparable){}。PHP中同样用instanceof IOS 使用isKindOf
         6.在实现多接口的时候一定要避免方法名的重复。
###写法
```
<?php
interface IDataBase
{
  const IPadress  = @"192.168.1.1"; //静态常量
  function connect(){};
  function query(){};
  static function getLinkID(){};
  function close(){};
}

/**
 * 扩展接口 IDataBase
 */
interface IEDataBase extends IDataBase
{
  function paraSql(){};
}

/*
*  实现接口
**/
class Mysqli implements IEDataBase
{
  function connect(){
    echo 'Mysqli connent';
  };
  function query(){
    echo 'Mysqli query';
  };
  static function getLinkID(){
     echo 'Mysqli getLinkID';
  };
  function close(){
     echo 'Mysqli close';
  };
  function paraSql(){
     echo 'Mysqli paraSql';
  };
}

/*
*  实现接口
**/
class PDO implements IEDataBase
{
  function connect(){
    echo 'PDO connent';
  };
  function query(){
    echo 'PDO query';
  };
  static function getLinkID(){
     echo 'PDO getLinkID';
  };
  function close(){
     echo 'PDO close';
  };
  function paraSql(){
     echo 'PDO paraSql';
  };
}

/**
 * 对外统一 操作的数据库方法
 * 比如TP 里面的 大U方法获取 用户数据我
 */
class DB
{
    static $db = null;
    public $sql = null;
    function  __construct($config)
    {
      switch ($config['DBConnectType']) {
        case 'mysqli':
            self::$db = new Mysqli();
          break;
        case 'pdo':
            self::$db = new PDO();
          break;
        default:
          break;
      }
      self::$db->connect();
    }

    fucntion where($where){
      echo 'do Where<br />';
      $this->sql .= 'do Where';
      return $this;
    }
    funtion order($order){
      echo 'do Order <br />';
      $this->sql.= 'do Order';
      return $this;
    }
    function  querySql($sql)
    {
      self::$db->query($this->sql);
    }
    function __destruct()
    {
        self::$db->close();
    }
}

//调用
$db  = new  DB();
$db->where('do where')->order('order desc')->querySql();

```
###是抽象类?
###使用场景？
###如何正确的使用？





参考链接
[java](http://blog.csdn.net/chenssy/article/details/12858267)
[PHP](http://blog.csdn.net/klinghr/article/details/5212976)
《细说PHP》
