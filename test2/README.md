
# 实验2：图书管理系统用例建模
|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|201510414122|软件(本)15-1|吴川|![flow1](../myself.jpg)|

## 1. 图书管理系统的用例关系图

### 1.1 借阅者用例图PlantUML源码如下：

``` usecase
@startuml

User -> (Start)
User --> (Use the application) : A small label

:Main Admin: ---> (Use the application) : This is\nyet another\nlabel

@enduml
```


### 1.2. 借阅者用例图如下：

参见图7.6

![usecase](usecase.png)

 
### 1.3. 图书管理员用例图PlantUML源码如下：
 
``` usecase
@startuml

User -> (Start)
User --> (Use the application) : A small label

:Main Admin: ---> (Use the application) : This is\nyet another\nlabel

@enduml
```

### 1.4. 图书管理员用例图如下：

参见图7.6

![usecase](usecase.png)


### 1.5. 系统管理员用例图PlantUML源码如下：
 
``` usecase
@startuml

User -> (Start)
User --> (Use the application) : A small label

:Main Admin: ---> (Use the application) : This is\nyet another\nlabel

@enduml
```


### 1.6. 系统管理员用例图如下：

参见图7.6

![usecase](usecase.png)


## 2. 参与者说明：

###     2.1 读者
 

主要职责是：1.将读者借书卡提供给系统；2.将读者所借图书输入系统；3.

###     2.2 图书管理员
 
主要职责是：****

###     2.3 系统管理员
    
主要职责是：****

##     3. 用例规约表

###     3.1 “借出图书”用例

参见：表7.5

###     3.2 “购入图书”用例

参见：表7.5

**“购入图书”用例流程图源码如下：**
``` uc1_flow
@startuml
start
:Hello world;
:This is on defined on
several **lines**;
stop
@enduml
```

**“购入图书”用例流程图源码如下：**

![uc1_flow](usecase1_flow.jpg)

###     3.3 “***”用例

参见：表7.5
