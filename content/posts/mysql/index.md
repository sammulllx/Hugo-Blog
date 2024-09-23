---
title: "mysql基本操作"
date: 2024-05-07T09:46:46+08:00
# weight: 1
# aliases: ["/first"]
tags: ["mysql"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## 创建数据库

指定字符集和排序规则：

```mysql
CREATE DATABASE IF NOT EXISTS RUNOOB
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_general_ci;
```



## 删除数据库

```mysql
DROP DATABASE IF EXISTS RUNOOB;
```

## 选择数据库

```mysql
use RUNOOB;
```



## 创建数据表

```mysql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    birthdate DATE,
    is_active BOOLEAN DEFAULT TRUE
);
```

- `id`: 用户 id，整数类型，自增长，作为主键。
- `username`: 用户名，变长字符串，不允许为空。
- `email`: 用户邮箱，变长字符串，不允许为空。
- `birthdate`: 用户的生日，日期类型。
- `is_active`: 用户是否已经激活，布尔类型，默认值为 true。

以上只是一个简单的实例，用到了一些常见的数据类型包括 INT, VARCHAR, DATE, BOOLEAN，你可以根据实际需要选择不同的数据类型。AUTO_INCREMENT 关键字用于创建一个自增长的列，PRIMARY KEY 用于定义主键。

如果你希望在创建表时指定数据引擎，字符集和排序规则等，可以使用 **CHARACTER SET** 和 **COLLATE** 子句

```mysql
CREATE TABLE mytable (
    id INT PRIMARY KEY,
    name VARCHAR(50)
) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

以下例子中我们将在 RUNOOB 数据库中创建数据表 runoob_tbl：

```mysql
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

- 如果你不想字段为**空**可以设置字段的属性为 **NOT NULL**，如上实例中的 runoob_title 与 runoob_author 字段， 在操作数据库时如果输入该字段的数据为空，就会报错。
- **AUTO_INCREMENT** 定义列为自增的属性，一般用于主键，数值会自动加 1。
- **PRIMARY KEY** 关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号 **,** 分隔。
- **ENGINE** 设置存储引擎，**CHARSET** 设置编码。

## 删除数据表

```mysql
DROP TABLE IF EXISTS runoob_tbl;
```

## 插入数据

```mysql
INSERT INTO users (username, email, birthdate, is_active)
VALUES
    ('test1', 'test1@runoob.com', '1985-07-10', true),
    ('test2', 'test2@runoob.com', '1988-11-25', false),
    ('test3', 'test3@runoob.com', '1993-05-03', true);
```

```mysql
INSERT INTO runoob_tbl  (runoob_title, runoob_author, submission_date)
VALUES ("学习 PHP", "菜鸟教程", NOW());


INSERT INTO runoob_tbl (runoob_title, runoob_author, submission_date) VALUE ("学习 MySQL", "菜鸟教程", NOW());

INSERT INTO runoob_tbl
(runoob_title, runoob_author, submission_date)
VALUES ("JAVA 教程", "RUNOOB.COM", '2016-05-06');

```

