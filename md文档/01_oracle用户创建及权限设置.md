# [oracle用户创建及权限设置](http://www.cnblogs.com/shlcn/archive/2011/07/21/2112879.html)

权限：

　　create session

　　create table

　　unlimited tablespace

　　connect

　　resource

　　dba

　　例：

　　#sqlplus /nolog

　　SQL> conn / as sysdba;

　　SQL>create user username identified by password

　　SQL> grant dba to username;

　　SQL> conn username/password

　　SQL> select * from user_sys_privs;

　　我们将从创建Oracle用户权限表开始谈起，然后讲解登陆等一般性动作，使大家对Oracle用户权限表有个深入的了解。

　　一、创建

　　sys;//系统管理员，拥有最高权限

　　system;//本地管理员，次高权限

　　scott;//普通用户，密码默认为tiger,默认未解锁

　　二、登陆

　　sqlplus / as sysdba;//登陆sys帐户

　　sqlplus sys as sysdba;//同上

　　sqlplus scott/tiger;//登陆普通用户scott

　　三、管理用户

　　create user zhangsan;//在管理员帐户下，创建用户zhangsan

　　alert user scott identified by tiger;//修改密码

　　四，授予权限

　　1、默认的普通用户scott默认未解锁，不能进行那个使用，新建的用户也没有任何权限，必须授予权限

　　

　　grant create session to zhangsan;//授予zhangsan用户创建session的权限，即登陆权限

　　grant unlimited tablespace to zhangsan;//授予zhangsan用户使用表空间的权限

　　grant create table to zhangsan;//授予创建表的权限

　　grante drop table to zhangsan;//授予删除表的权限

　　grant insert table to zhangsan;//插入表的权限

　　grant update table to zhangsan;//修改表的权限

　　grant all to public;//这条比较重要，授予所有权限(all)给所有用户(public)

　　2、oralce对权限管理比较严谨，普通用户之间也是默认不能互相访问的，需要互相授权

　　

　　grant select on tablename to zhangsan;//授予zhangsan用户查看指定表的权限

　　grant drop on tablename to zhangsan;//授予删除表的权限

　　grant insert on tablename to zhangsan;//授予插入的权限

　　grant update on tablename to zhangsan;//授予修改表的权限

　　grant insert(id) on tablename to zhangsan;

　　grant update(id) on tablename to zhangsan;//授予对指定表特定字段的插入和修改权限，注意，只能是insert和update

　　grant alert all table to zhangsan;//授予zhangsan用户alert任意表的权限

　　五、撤销权限

　　基本语法同grant,关键字为revoke

　　六、查看权限

　　select * from user_sys_privs;//查看当前用户所有权限

　　select * from user_tab_privs;//查看所用用户对表的权限

　　七、操作表的用户的表

　　

　　select * from zhangsan.tablename

　　八、权限传递

　　即用户A将权限授予B，B可以将操作的权限再授予C，命令如下：

　　grant alert table on tablename to zhangsan with admin option;//关键字 with admin option

　　grant alert table on tablename to zhangsan with grant option;//关键字 with grant option效果和admin类似

　　九、角色

　　角色即权限的集合，可以把一个角色授予给用户

　　create role myrole;//创建角色

　　grant create session to myrole;//将创建session的权限授予myrole

　　grant myrole to zhangsan;//授予zhangsan用户myrole的角色

　　drop role myrole;删除角色