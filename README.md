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
 	        
 	约束
 	    非空 not null
 	    主键约束 
 	        PRIMARY KEY
 	        联合主键
 	        CONSTRAINT [constraint_name] PRIMARY KEY(column_name1,....)
             	    create table userinfo_p(id number(6,0),username varchar2(20),
                      userpsd varchar2(20),
                     constraint pk_id_username primary key(id,username));
            查找某个表的约束信息 user_constraints
                select [constraint_name] from user_constraints where table_name=[table_name]
            修改表时添加主键约束
                alter table [table_name] add constraint [constraint_name]  permary key(column_name1,,,)
            修改约束名字
                alter table [table_name] rename constraint [constraint_name_old] to [name_new];
            禁用约束
                alter table [table_name] disable constraint [constraint_name]
            删除约束
 	            alter table [table_name] drop constraint [constraint_name]
 	        删除主键约束
 	            alter table [table_name] drop primary key[CASCADE]
 	    外键约束
 	        创建表时设置外键约束
 	            CREATE TABLE table1[从表] (column_name datatype references table2[主表](column_name),....);
 	            主表的字段必须时主键
 	            外键约束
 	            CONSTRAINT constraint_name FOREIGN KEY(column_name) REFERENCES table_name(column_name) [ON DELETE CASCADE]
 	                （接连删除）on delete cascade
 	        修改表时添加外键约束
 	            alter table [table_name]
 	             add constraint [constraint_name] foreign key(column_name) 
 	               references table_name(column_name)[on delete cascade]
 	        禁用外键约束
 	            alter table [table_name] DISABLE|ENABLE CONSTRAINT constraint_name;  
 	            alter table [table_name] DROP CONSTRAINT constraint_name
 	    唯一约束  UNIQUE
 	        唯一约束与主键约束区别
 	            唯一约束：允许又一个空值，可以设置多个column
 	            主键：每张表中只能有一个，不能有空值
 	        创建表时设置唯一约束
 	            column_name datatype UNIQUE;
 	            CONSTRAINT contraint_name UNIQUE(column_name) 只能设置单列
 	                create table userinfo_u ( id number(6,0) primary key,
 	                 username varchar2(20),constraint un_username unique(username)); 
 	        修改表时添加唯一约束
 	            alter table [table_name] add constraint [constraint_name] inque(column_name)   
 	        删除唯一约束
 	            禁用
 	            disable|enable constraint constraint_name
 	            删除
 	            drop constraint constraint_name
 	    检查约束 
 	        create table userinfo_c1 (id varchar2(10) primary key, username varchar2(20),
 	        salary number(5,0) check(salary>0));
 	        
 	        create table userinfo_c1 (id varchar2(10) primary key, username varchar2(20),
 	        salary number(5,0),constraint ck_salary check(salary>0);
 	        
 	        alter table [table_name] add constraint [constraint_name] check(expressions) 
 	查询
 	    sql/plus中设置格式
            COLUMN column_name HEADING new_name; column username heading 用户名;不会真正该表列名
            col column_name format a10;   column_name 占用10个字符
            col column_name format ￥9999.99   数值性格式化
            col column_name clear
        基础语法
            select[distinct] * from table_name;  [distinct]去重
                select distinct username  from users;
        设置别名
            as
        运算符和表达式
            算数运算符+-*/
            比较运算符 > >= < <= = <>          <>不等于
            逻辑运算符 and与  or或 not非
        模糊查询 关键子like
            通配符 _ 代表一个字符   % 0到多个任意字符
            select * from users where username like '_a';
        范围查询  
            between [起始值] and [结束值]
                select * from users where salary between 500 and 1000;
            in ('','') 等价与or连接
                select * from users where username in('aaa','bbb');
        排序
            order by    DESC/ASC
                BODER BY column1 desc/asc,column2 desc/asc
            case..when  then [result]
                1. CASE column_name WHEN value1 THEN result1,...[else result] END
                 select username,salary,case username when 'aaaa' then '计算机部门'
                    2  when 'bbbb' then '市场部门' else '其他部门' end as 部门 from users;
                2.  select username,salary,case when salary>500 then '工资高'  when salary<500 
                    2 then '工资低' else '正好' end  as 状态 from users;
        decode 函数
            decode(column_name,value1,result1,value2,result2,....,defaultvalue) as 别名
            select username,decode(username,'aaaa','计算机部门','bbbb','业务部门','其他部门') as 部门 from users;
        
 	    
 	        
 	        
 	            
 	 