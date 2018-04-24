# 实验4：图书管理系统顺序图绘制
|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414122|软件(本)15-1|吴川|![flow1](../myself.jpg)|

## 图书管理系统的顺序图

## 1. 借书用例
## 1.1. 借书用例PlantUML源码

``` sequence
@startuml
actor  借阅者 as reader
actor  图书管理员 as admin
activate reader
activate admin
reader->admin:提供需借书籍
reader->admin:提供借书卡号
deactivate reader
admin->图书管理系统:login()
activate 图书管理系统
admin<-图书管理系统:showReaderInfo()
admin<-图书管理系统:1.check()
图书管理系统->读者:getBookInfo()
activate 读者
图书管理系统->读者:2.check()
deactivate 读者
图书管理系统->book:getBookInfo()
activate book
deactivate book
图书管理系统->读者:borrow()
activate 读者
deactivate 读者
图书管理系统->借书记录:builtBorrowInfo()
activate 借书记录
deactivate 借书记录
图书管理系统->book:updateBookInfo()
activate book
deactivate book
图书管理系统->读者:updateReaderInfo()
activate 读者
deactivate 读者
图书管理系统-->admin:isBorrow()
deactivate 图书管理系统
admin-->reader:借阅成功
activate reader
deactivate reader
deactivate admin
@enduml


```

## 1.2. 借书用例顺序图
![class](wc1.png)

## 1.3. 借书用例顺序图说明
ABCDE....

***

## 2. 还书用例
## 2.1. 还书用例PlantUML源码

``` sequence
@startuml
actor  借阅者 as reader
actor  图书管理员 as admin
activate reader
activate admin
reader->admin:   提供还书书籍
deactivate reader
admin->admin:检查是否损坏书籍
admin->图书管理系统:login()
activate 图书管理系统
图书管理系统->book:getBookInfo()
activate book
deactivate book
图书管理系统->借书记录:getBorrowInfo()
activate 借书记录
图书管理系统->借书记录:getBorrowDate()
图书管理系统->借书记录:getNowDate()
图书管理系统->借书记录:isOverTime()
deactivate 借书记录
图书管理系统->还书记录:builtReturnInfo()
activate 还书记录
deactivate 还书记录
图书管理系统->book:updateBookInfo()
activate book
deactivate book
图书管理系统->读者:updateReaderInfo()
activate 读者
deactivate 读者
图书管理系统->逾期记录:record()
activate 逾期记录
deactivate 逾期记录
图书管理系统-->admin:return
deactivate 图书管理系统
admin-->reader:还书成功
activate reader
deactivate reader
deactivate admin
@enduml
```

## 2.2. 还书用例顺序图
![class](wc2.png)

## 2.3. 还书用例顺序图说明
ABCDE...
***
