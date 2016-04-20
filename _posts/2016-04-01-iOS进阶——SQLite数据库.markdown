---
layout: post
title: "iOS进阶——SQLite数据库"
date: 2016-04-01 10:08:13 + 08:00
image: '/assets/img/'
description: 'SQLite'
tags:
- iOS
- Objective-C
categories:
- iOS_Objective-C
twitter_text:
---

# 一、数据库管理系统

SQL语言概念
SQL是一种**结构化查询语言**，TA是专为数据库建立的操作命令集，是一种功能齐全的**数据库语言**

* 常见的数据库语言：
**MySQL、Oracle**

***

数据库管理系统

> 数据库的特征：

 * 以一定方式存储在一起
 * 能为多个用户共享
 * 具有尽可能少的冗余代码
 * 与程序彼此独立的数据集合

讲了这么多数据库相关的知识，那么到底什么是数据库呢
* **数据库**（Database）是按照数据结构来组织、存储和管理数据的仓库

数据库的分类
**关系型数据库（主流）**、对象数据库、层次式数据库

常用关系型数据库
PC端：Oracle、MySQL、SQL Server、Access、DB2、Sybase
**嵌入式\移动客户端：SQLite**

SQLite是一个轻量级的**关系数据库**。SQLite最初的设计目标是用于嵌入式系统，TA占用资源非常少，在嵌入式设备中，只需要几百K的内存就够了，目前应用于Android、iOS、Windows Phone等智能手机。iOS使用时SQLite，只需要加入libsqlite3.0.tbd依赖以及引入sqlite3.h头文件即可

***

**数据库中有几个很重要的概念**

>表：是数据库中一个非常重要的对象，是其他对象的基础。根据信息的分类情况，一个数据库中可能包含若干个数据表

>字段：表的“列”称为“字段”，每个字段包含某一专题的信息

>记录：是指对应于数据表中一行信息的一组完整的相关信息

***

> SQL中很重要的一点，一定要记住，***SQL对大小写不敏感***

***

SQL语句后面的分号

在数据库系统中分号是作为分隔每条SQL语句的标准方法，这样就可以在对服务器的相同请求中执行一条以上的语句
需要我们注意的是，某些数据库会有要求在每条SQL命令的末尾加上分号，而SQLite则属于另一类，TA的语句末尾**不使用分号**

* PS：在我们学习Objective-C时每段语句的末尾都要求加上分号，但是SQLite不需要我们要区分开来

*** 

SQLite数据库数据类型
SQLite是无类型的数据库，可以保存任何类型的数据，对于SQLite来说对字段不指定类型是完全有效的
为了使SQLite和其他数据库间的兼容性最大化，SQLite支持“类型近似”的观点，列的类型近似指的是存储列上数据的推荐类型。

**SQLite近似类型规则**


> 1. 如果类型字符串中包含“int”，那么该字段的亲缘类型是INTEGER
> 2. 如果类型字符串中包含“char”、“clob”或“text”，那么该字段的亲缘类型是TEXT，如VARCHAR
> 3. 如果类型字符串中包含“blob”，那么该字段的亲缘类型是none
> 4. 如果类型字符串中包含“real”、“floa”或“doub”，那么该字段的亲缘类型是real
> 5. 其余情况下，字段的亲缘类型为NUMERIC

***

SQLite字段约束条件

 * not null - 非空
 * unique - 唯一
 * primary key - 主键
 * foreign key - 外键
 * check - 条件检查，确保一列中的所有值满足一定条件
 * default - 默认
 * autoincreatement - 自增型变量

***

SQL语句

* SQL的语句我们可以分成两个部分来看，分别是：数据操作语言（DML）和数据定义语言（DDL）

> 查询和更新指令构成了SQL的DML部分：

 * 数据插入命令——insert
 * 数据库更新命令——update
 * 数据库删除命令——delete
 * 数据库检索命令——select

> DDL部分是我们有能力创建活删除表格，我们也可以定义索引，规定表之间的链接，以及施加表间的约束

* 创建数据库命令——create database
* 修改数据库命令——alter database
* 创建新表的命令——create table
* 变更数据库中的表——alter table
* 删除表——drop table
* 创建索引——create index
* 删除索引——drop index


*** 

三、iOS的数据库技术的实现

开始使用SQLite所需要的几个步骤

>需要的框架：libsqlite3.0.tbd

1. 引入sqlite3.h头文件
2. 打开数据库
3. 执行SQL命令——创建表，增删改查等操作
4. 关闭数据库

***

打开与关闭数据库
* 需要注意的是我们的iOS程序中,一般情况下只有一个数据库,我们可以在数据库中创建多张表来保存不同的信息,但是千万不要创建多个数据库,每个数据库中只有一张表,因为不断的连接,关闭数据库是很耗性能的


创建一个DB类用来进行对数据库的操作

打开数据库

{% highlight ruby %}
#import "DB.h"

@implementation DB

// 创建数据库指针
static sqlite3 *db = nil;

// 打开数据库
+ (sqlite3 *)open {
    
    // 此方法的主要作用是打开数据库
    // 返回值是一个数据库指针
    // 因为这个数据库在很多的SQLite API（函数）中都会用到，我们声明一个类方法来获取，更加方便

    // 懒加载
    if (db != nil) {
        return db;
    }
    
    // 获取Documents路径
    NSString *docPath = [NSSearchPathForDirectoriesInDomains(NSDocumentationDirectory, NSUserDomainMask, YES) lastObject];
    
    // 生成数据库文件在沙盒中的路径
    NSString *sqlPath = [docPath stringByAppendingPathComponent:@"studentDB.sqlite"];
    
    // 创建文件管理对象
    NSFileManager *fileManager = [NSFileManager defaultManager];
    
    // 判断沙盒路径中是否存在数据库文件，如果不存在才执行拷贝操作，如果存在不在执行拷贝操作
    if ([fileManager fileExistsAtPath:sqlPath] == NO) {
        // 获取数据库文件在包中的路径
        NSString *filePath = [[NSBundle mainBundle] pathForResource:@"studentDB" ofType:@"sqlite"];
        
        // 使用文件管理对象进行拷贝操作
        // 第一个参数是拷贝文件的路径
        // 第二个参数是将拷贝文件进行拷贝的目标路径
        [fileManager copyItemAtPath:filePath toPath:sqlPath error:nil];
        
    }
    
    // 打开数据库需要使用一下函数
    // 第一个参数是数据库的路径（因为需要的是C语言的字符串，而不是NSString所以必须进行转换）
    // 第二个参数是指向指针的指针
    sqlite3_open([sqlPath UTF8String], &db);
    
    return db;
}
{% endhighlight %}

关闭数据库

{% highlight ruby %}
// 关闭数据库
+ (void)close {
    
    // 关闭数据库
    sqlite3_close(db);
    
    // 将数据库的指针置空
    db = nil;
    
}
{% endhighlight %}

***

创建一个学生类

创建表的方法

{% highlight ruby %}
// 创建表方法
- (void)createTable {
    
    // 将建表的sql语句放入NSString对象中
    NSString *sql = @"create table if not exists stu (ID integer primary key, name text not null, gender text default '男')";
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    // 执行sql语句
    int result = sqlite3_exec(db, sql.UTF8String, nil, nil, nil);
    
    if (result == SQLITE_OK) {
        NSLog(@"建表成功");
    } else {
        NSLog(@"建表失败");
    }
    
    // 关闭数据库
    [DB close];

}
{% endhighlight %}

***

获取表中所有的学生

{% highlight ruby %}
// 获取表中保存的所有学生
+ (NSArray *)allStudents {
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    // 创建一个语句对象
    sqlite3_stmt *stmt = nil;
    
    // 声明数组对象
    NSMutableArray *mArr = nil;
    
    // 此函数的作用是生成一个语句对象，此时sql语句并没有执行，创建的语句对象，保存了关联的数据库，执行的sql语句，sql语句的长度等信息
    int result = sqlite3_prepare_v2(db, "select * from Students", -1, &stmt, nil);
    if (result == SQLITE_OK) {
        
        // 为数组开辟空间
        mArr = [NSMutableArray arrayWithCapacity:0];
        
        // SQLite_ROW仅用于查询语句，sqlite3_step()函数执行后的结果如果是SQLite_ROW，说明结果集里面还有数据，会自动跳到下一条结果，如果已经是最后一条数据，再次执行sqlite3_step()，会返回SQLite_DONE，结束整个查询
        while (sqlite3_step(stmt) == SQLITE_ROW) {
            
            // 获取记录中的字段值
            // 第一个参数是语句对象，第二个参数是字段的下标，从0开始
            int ID = sqlite3_column_int(stmt, 0);
            const unsigned char *cName = sqlite3_column_text(stmt, 1);
            const unsigned char *cGender = sqlite3_column_text(stmt, 2);
            
            // 将获取到的C语言字符串转换成OC字符串
            NSString *name = [NSString stringWithUTF8String:(const char *)cName];
            NSString *gender = [NSString stringWithUTF8String:(const char *)cGender];
            Student *student = [Student studentWithID:ID name:name gender:gender];
            
            // 添加学生信息到数组中
            [mArr addObject:student];
        }
    }
    
    // 关闭数据库
    sqlite3_finalize(stmt);
    
    return mArr;
    
}
{% endhighlight %}

***

查找对应ID的学生

{% highlight ruby %}
// 根据指定的ID，查找相对应的学生
+ (Student *)findStudentByID:(int)ID {
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    // 创建一个语句对象
    sqlite3_stmt *stmt = nil;
    
    Student *student = nil;
    
    // 生成语句对象
    int result = sqlite3_prepare_v2(db, "select * from Students where ID = ?", -1, &stmt, nil);
    
    if (result == SQLITE_OK) {
        
        // 如果查询语句或者其他sql语句有条件，在准备语句对象的函数内部，sql语句中用？来代替条件，那么在执行语句之前，一定要绑定
        // 1代表sql语句中的第一个问号，问号的下标是从1开始的
        sqlite3_bind_int(stmt, 1, ID);
        
        if (sqlite3_step(stmt) == SQLITE_ROW) {
            
            // 获取记录中的字段信息
            const unsigned char *cName = sqlite3_column_text(stmt, 1);
            const unsigned char *cGender = sqlite3_column_text(stmt, 2);
            
            // 将C语言字符串转换成OC字符串
            NSString *name = [NSString stringWithUTF8String:(const char *)cName];
            NSString *gender = [NSString stringWithUTF8String:(const char *)cGender];
            
            student = [Student studentWithID:ID name:name gender:gender];
            
        }
    }
    
    // 先释放语句对象
    sqlite3_finalize(stmt);
    return student;
    
}
{% endhighlight %}

***

向表中添加一条记录

{% highlight ruby %}
// 插入一条记录
+ (void)insertStudentWithID:(int)ID name:(NSString *)name gender:(NSString *)gender {
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    sqlite3_stmt *stmt = nil;
    
    int result = sqlite3_prepare_v2(db, "insert into Students values(?,?,?)", -1, &stmt, nil);
    
    if (result == SQLITE_OK) {
        // 绑定
        sqlite3_bind_int(stmt, 1, ID);
        sqlite3_bind_text(stmt, 2, [name UTF8String], -1, nil);
        sqlite3_bind_text(stmt, 3, [gender UTF8String], -1, nil);
        
        // 插入与查询不一样，执行结果没有返回值
        sqlite3_step(stmt);
        
    }
    
    // 释放语句对象
    sqlite3_finalize(stmt);
    
}
{% endhighlight %}

***

更新记录

{% highlight ruby %}
// 更新指定ID下的姓名和性别
+ (void)updateStudentName:(NSString *)name gender:(NSString *)gender forID:(int)ID {
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    sqlite3_stmt *stmt = nil;
    
    int result = sqlite3_prepare_v2(db, "update Student set name = ?, gender = ? where ID = ?", -1, &stmt, nil);
    if (result == SQLITE_OK) {
        sqlite3_bind_text(stmt, 1, [name UTF8String], -1, nil);
        sqlite3_bind_text(stmt, 2, [gender UTF8String], -1, nil);
        sqlite3_bind_int(stmt, 3, ID);
        
        sqlite3_step(stmt);
    }
    sqlite3_finalize(stmt);
}
{% endhighlight %}

***

删除记录

{% highlight ruby %}
// 根据指定ID删除学生
+ (void)deleteStudentByID:(int)ID {
    
    // 打开数据库
    sqlite3 *db = [DB open];
    
    sqlite3_stmt *stmt = nil;
    
    int result = sqlite3_prepare_v2(db, "delete from Students where ID = ?", -1, &stmt, nil);
    
    if (result == SQLITE_OK) {
        sqlite3_bind_int(stmt, 1, ID);
        sqlite3_step(stmt);
    }
    
    sqlite3_finalize(stmt); 
    
}
{% endhighlight %}

* 最后的PS:这个数据库我是实现存有预留的数据库数据的,如果有同学要用上面的代码要先将数据库内事先添加数据
