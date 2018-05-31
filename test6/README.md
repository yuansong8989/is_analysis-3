cC﻿<!-- markdownlint-disable MD033-->
<!-- 禁止MD033类型的警告 https://www.npmjs.com/package/markdownlint -->

# 基于GitHub的实验管理平台的分析与设计

### 成都大学信息科学与工程学院

|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414122|软件(本)15-1|吴川|![flow1](../myself.jpg)|

## 1. 概述
- 基于GitHub的实验管理平台的作用是在线管理实验成绩的Web应用系统。学生和老师的实验内容均存放在GitHUB页面上。
- 学生的功能主要有：一是设置自己的GitHub用户名，二是可以选择学期查询哪门课程，三是查询自己该课程的实验成绩。学生的GitHub用户名是公开的，但成绩不公开。
- 老师的功能主要有：一是批改每个学生的成绩，二是查看每个学生的成绩。
- 老师和学生都能通过本系统的链接方便地跳转到学生的每个GitHUB实验目录，以便批改实验或者查看实验情况。
- 实验成绩按数字分数计算，每项实验含有多个评分项，评分项之和为100分，最低为0分。
- 系统自动计算每个学生的所有实验的平均分。
    
## 2. 系统总体结构
![](系统总体结构.png)
界面设计参见：https://wuchuan11.github.io/is_analysis/test6/ui/index.html
    
## 3. 用例图设计 [源码](src/UseCase.puml)
![](UseCase.png)

## 4. 类图设计 [源码](src/Class.puml)
![](./Class.png)

## 5. 数据库设计
     
- ### USERS表（用户表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |USER_ID|NUMBER(8,0)|主键|否| | | 用户ID|
    |NAME|VARCHAR2(50 BYTE)| |否| | | 用户真实姓名|
    |GITHUB_USERNAME|VARCHAR2(50 BYTE)| |是|空| | GitHUB用户名|
    |UPDATE_DATE|DATE| |是|空| | GitHUB用户名修改日期|
    |PASSWORD|VARCHAR2(512 BYTE)| |是|空| | 加密存储密码，为空表示密码就是学号|
    |DISABLE|VARCHAR2(20 BYTE)| |否| | |是否禁用,值为是表示禁用,其他表示正常.|

- ### TEACHERS表（教师表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TEACHER_ID|VARCHAR2(50 BYTE)|主键|否| | | 教师的编号|
    |USER_ID|NUMBER(8,0)|外键|是| | | 老师的用户ID，USERS表的外键|
    |TEACHER_NAME|VARCHAR2(50 BYTE)| |否| | | 教师姓名|
    |DEPARTMENT|VARCHAR2(400 BYTE)| |否| | | 老师属于的部门|

- ### STUDENTS表（学生表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |STUDENT_ID|VARCHAR2(50 BYTE)|主键|否| | | 学生的学号|
    |USER_ID|NUMBER(8,0)|外键|是| |空| 学生的用户ID，USERS表的外键，为空表示还没有建立用户|
    |STUDENT_NAME|VARCHAR2(50 BYTE)| |否| | | 学生姓名|
    |CLASS|VARCHAR2(20 BYTE)| |否| | | 学生所在的班级|
    |RESULT_SUM|VARCHAR2(400 BYTE)|外键|是|空| | 成绩汇总（来自GRADES表），以逗号分开，第一个成绩是平均成绩,后面是每次实验的成绩，N表示未批改，平均分只计算已批改的。比如：“81.25,70,80,85,90,N”表示一共批改了4次，第5次未批改，4次的成绩分别是81.25,70,80,85,90,N，4次的平均分是81.25|
    |WEB_SUM|VARCHAR2(400 BYTE)| |是|空| | GitHub网址是否正确，用逗号分开，Y代表正确，N代表不正确。第1位代表总的GitHUB地址是否正确，第2位表示第1次实验的地址，第3位表示第2位实验地址，依此类推。比如：“Y,Y,Y,Y,Y,N”表示第5次实验地址不正确，其他地址正确|
 
- ### GRADES表（学生实验成绩表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |STUDENT_ID|VARCHAR2(50 BYTE)|联合主键1，外键|否| | | 学生的学号，STUDENTS表外键|
    |TEST_ID|NUMBER(6,0)|联合主键2，外键|否| | | 实验编号，TESTS表的外键|
    |RESULT|NUMBER|主键|是|空| 取值0-100| 分数，这个值为空表示没有批改|
    |MEMO|VARCHAR2(400 BYTE)| |是|空| | 老师对实验的评语|
    |UPDATE_DATE|DATE| |是|空| |老师批改实验的日期，为空表示未批改|

- ### TESTS表（实验项目表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TEST_ID|NUMBER(6,0)|主键|否| | | 实验编号|
    |COURSE_NAME|VARCHAR2(100 BYTE)|外键 |否| | | 课程名称|
    |TITLE|VARCHAR2(100 BYTE)| |否| | | 实验名称|
   
- ### COURSES表（课程表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |COURSE_ID|NUMBER(6,0)|主键|否| | | 课程编号|
    |STUDENT_ID|VARCHAR2(50 BYTE)|联合主键1，外键 |否| | | 学生的学号，STUDENTS表外键|
    |TEACHER_ID|VARCHAR2(50 BYTE)|联合主键2，外键 |否| | | 教师的编号，TEACHERS表外键|
    |COURSE_NAME|VARCHAR2(100 BYTE)| |否| | | 课程名称|
    |COURSE_HOUR|VARCHAR2(100 BYTE)| |否| | | 课程学时|
 
- ### TERMS表（学期表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TERM_ID|NUMBER(6,0)|主键|否| | | 学期编号|
    |STUDENT_ID|VARCHAR2(50 BYTE)|联合主键1，外键 |否| | | 学生的学号，STUDENTS表外键|
    |TEACHER_ID|VARCHAR2(50 BYTE)|联合主键2，外键 |否| | | 教师的编号，TEACHERS表外键|
    |TERM_YEAR|VARCHAR2(100 BYTE)| |否| | | 学年|
    
    

## 6. 用例及界面详细设计
- ### [“学生列表”用例](./用例/学生列表.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/index.html)
- ### [“评定成绩”用例](./用例/评定成绩.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/评定成绩.html)
- ### [“查看成绩”用例](./用例/查看成绩.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/查看成绩.html)
- ### [“修改密码”用例](./用例/修改密码.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/顶部菜单.html)
- ### [“修改用户信息”用例](./用例/修改用户信息.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/顶部菜单.html)
- ### [“查看用户信息”用例](./用例/查看用户信息.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/顶部菜单.html)
- ### [“教师列表”用例](./用例/教师列表.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/学生选课.html)
- ### [“课程列表”用例](./用例/课程列表.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/老师选课.html)
- ### [“教师选课”用例](./用例/老师选课.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/老师选课.html)
- ### [“学生选课”用例](./用例/学生选课.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/学生选课.html)
- ### [“选学期”用例](./用例/选学期.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/选学期.html)
- ### [“登出”用例](./用例/登出.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/顶部菜单.html)
- ### [“登录”用例](./用例/登录.md),[界面](https://wuchuan11.github.io/is_analysis/test6/ui/登录.html)
    
