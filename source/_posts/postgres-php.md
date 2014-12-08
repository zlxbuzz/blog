title: postgres-php
date: 2014-12-08 17:59:40
categories: postgresql
tags: [php,postgresql]
---
##自己写的一个postgresql和php的类
<!--more-->
```php
//连接pg数据库的参数
$pg_host="127.0.0.1";
$pg_port="5432";
$pg_db="abc";
$pg_name="postgres";
$pg_password="postgres";

class pgsql {  
private $linkid; // Postgresql连接标识符  
private $host; // PostgreSQL服务器主机  
private $port; // PostgreSQL服务器主机端口  
private $user; // PostgreSQL用户  
private $passwd; // PostgreSQL密码  
private $db; // Postgresql数据库  
private $result; // 查询的结果  
private $querycount; // 已执行的查询总数  
function __construct($host, $port ,$db, $user, $passwd) {  
$this->host = $host;  
$this->port = $port;  
$this->user = $user;  
$this->passwd = $passwd;  
$this->db = $db;  
}  
/* 连接Postgresql数据库 */  
function connect(){  
try{  
$this->linkid = @pg_connect("host=$this->host port=$this->port dbname=$this->db  
user=$this->user password=$this->passwd");  
if (! $this->linkid)  
throw new Exception("Could not connect to PostgreSQL server.");  
}  
catch (Exception $e) {  
die($e->getMessage());  
}  
}  
/* 执行数据库查询。 */  
function query($query){  
try{  
$this->result = @pg_query($this->linkid,$query);  
if(! $this->result)  
throw new Exception("The database query failed.");  
}  
catch (Exception $e){  
echo $e->getMessage();  
}  
$this->querycount++;  
return $this->result;  
}  
/* 确定受查询所影响的行的总计。 */  
function affected_rows(){  
$count = @pg_affected_rows($this->linkid);  
return $count;  
}  
/* 确定查询返回的行的总计。 */  
function num_rows(){  
$count = @pg_num_rows($this->result);  
return $count;  
}  
/* 将查询的结果行作为一个对象返回。 */  
function fetchObject(){  
$row = @pg_fetch_object($this->result);  
return $row;  
}  
/* 将查询的结果行作为一个索引数组返回。 */  
function fetchRow(){  
$row = @pg_fetch_row($this->result);  
return $row;  
}  
/* 将查询的结果行作为一个关联数组返回。 */  
function fetch_assoc(){  
$row = @pg_fetch_assoc($this->result);  
return $row;  
} 
/* 将查询的结果行作为一个数组返回。 */  
function fetch_array(){  
$row = @pg_fetch_array($this->result);  
return $row;  
}  
/* 返回在这个对象的生存期内执行的查询总数。这不是必须的，但是您也许会感兴趣。 */  
function numQueries(){  
return $this->querycount;  
}  
} 

//连接pg
$pg = new pgsql($pg_host,$pg_port,$pg_db,$pg_name,$pg_password);  
$pg->connect();  
      
    if(!$pg)  
    {  
        $db_error = "无法连接到PostGreSQL数据库！";  
        echo $db_error;   
    }  
```
