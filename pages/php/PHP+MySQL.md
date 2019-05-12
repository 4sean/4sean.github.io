## PHP连接MySQL
PHP5以及以上版本建议使用以下方式连接MySQL：
- MySQLi extension("i"意为improved)
- PDO(PHP Data Objects)

### 我是该用 MySQLi ，还是 PDO?
==习惯哪个就用哪个==

PDO 应用在 12 种不同数据库中， MySQLi 只针对 MySQL 数据库。

所以，如果你的项目需要在多种数据库中切换，建议使用 PDO ，这样你只需要修改连接字符串和部分查询语句即可。 使用 MySQLi, 如果不同数据库，你需要重新编写所有代码，包括查询。

### MySQLi 和 PDO 连接 MySQL 实例

- MySQLi (面向对象)
- PDO

通过==phpinfo()== 查看是否安装成功

### 连接 MySQL
在我们访问 MySQL 数据库前，我们需要先连接到数据库服务器：
##### 实例 (MySQLi - 面向对象)

```
<?php
$servername = "localhost";
$username = "username";
$password = "password";
 
// 创建连接
$conn = new mysqli($servername, $username, $password);
 
// 检测连接
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
} 
echo "连接成功";
?>
```

####  实例 (PDO)

```
<?php
$servername = "localhost";
$username = "username";
$password = "password";
 
try {
    $conn = new PDO("mysql:host=$servername;", $username, $password);
    echo "连接成功"; 
}
catch(PDOException $e)
{
    echo $e->getMessage();
}
?>
```
*注意在以上 PDO 实例中我们已经指定了数据库 (myDB)。PDO 在连接过程需要设置数据库名。如果没有指定，则会抛出异常。*

### 关闭连接
连接在脚本执行完后会自动关闭。你也可以使用以下代码来关闭连接：

```
//实例 (MySQLi - 面向对象)
$conn->close();
```

```
实例 (PDO)
$conn = null;
```



