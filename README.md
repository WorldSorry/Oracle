# Oracle
    登陆
        connect [用户名]/[密码]
    开启scott用户
	    alter user scott account unlock;
	表空间 数据库
	    表空间由多个数据文件组成
	    永久表空间 表 视图 存储过程
	    临时表空间 数据库操作过程中间过程
	    UNDO表空间 保存事物修改的旧值
	    设置用户默认或临时表空间
	        ALTER USER username DEFAULT|TEMPORARY TABLESPACE tablespace_name
	数据类型
	    CHAR NCHAR 不可变
	    VARCHAR NVARCHAR 可变
	    NUMBER(P,S) p有效数字  s范围  number(5,2)  123.45
	    FLOAT(N)
	    DATE   默认系统时间default sysdate
	    TIMESTAMP 时间戳
	    BLOB 二进制存放  4GB
 	    CLOB 字符串存放  4GB
 	    
 	创建表 同一用户下表名唯一
 	    create table table_name(，，，，);
 	添加字段
 	    alter table [table_name] add [column_name datatype]
 	更改数据类型
 	    alter table [table_name] modify [column_name datatype]
 	删除字段
 	    alter table [table_name] drop column [column_name]
 	修改字段名
 	    alter table  [table_name] rename column [column_name] to [new_column_name]
 	修改表名字
 	    rename [table_name] to [new_table_name]
 	    
 	    
 	删除表
 	    清空数据 效率较高
 	    truncate table [table_name]   
 	    删除表结构
 	    drop table [table_name]  
 	    
 	添加数据
 	    insert into [table_name] ( ,,,) values (,,,)
 	修改数据
 	    update [table_name] set column1=value1,... [where confitions]
 	删除数据
 	    delete from table_name [where confitions]； 删除表全部数据 
 	    
 	复制表数据
 	    在建表时复制
 	        create table [table_new] as select [column1,...|* from] [table_old]
 	    在添加数据时复制 表结构相同
 	        insert into [table_new] [(column1,,,,)] select column1,,,,|* from table_old;
 	        
 	 