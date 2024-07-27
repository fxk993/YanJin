创建前先查看有无支持的数据库类型
**QSqlDatabase::drivers静态方法**
```cpp
/*
@params: void
@return: QStringList
*/
QStringList drivers();

```
# 1.创建QSqlDatabase
**QSqlDatabse静态方法addDatabase**
```cpp
/*
@params:
_1 数据库类型
-2 实例名称，用于创建多个实例时区别，有默认
@return：QSqlDatabase实例
*/
 QSqlDatabase addDatabase(const QString &type, const QString &connectionName = QLatin1StringView(defaultConnection));
/*
@params:
_1 
-2 实例名称，用于创建多个实例时区别
@return：QSqlDatabase实例
*/
 QSqlDatabase addDatabase(QSqlDriver *driver, const QString &connectionName = QLatin1StringView(defaultConnection))
 ```
 # 2.设置用户名，密码，域名，端口，数据库名
 ```cpp
 setUserName,setPassWord,setHostName,setPort,setDatabaseName;
 ```
 # 3.连接数据库
 open方法
 ```cpp
 /*
@params: void
@return: bool 连接成功返回true，失败返回false
*/
 bool open();
 ```
 打印错误
 ```cpp
 qDebug()<<db.lastError().text();
 ```
# 4.query操作
```cpp
/*
@params: 
_1 sql语句，有默认参数
_2 QSqlDatabase,有默认参数
@return: bool 连接成功返回true，失败返回false
*/
 QSqlQuery(const QString &query = QString(), const QSqlDatabase &db = QSqlDatabase());
 //第一种方法
 QSqlQuery query();
 query.exec("sql语句");
 //第二种方法
 QSQLQuery query("sql语句");
 query.exec();
 # 5.关闭数据库
 db.close();
