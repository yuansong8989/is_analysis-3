<!-- markdownlint-disable MD033-->
<!-- 禁止MD033类型的警告 https://www.npmjs.com/package/markdownlint -->

# 接口：getTeachers  [返回](../README.md)
  用例： [教师列表](../UseCase/教师列表.md)

- 权限：
    学生/访客：
    老师：

- 功能：
    返回所有教师的课程信息的列表。

- API请求地址：
   接口基本地址/v1/api/getTeachers

- 请求方式 ：
    GET

- 请求参数说明:
    无

- 返回实例：

        {
            "status": true,
            "info": null,
            "total": 8,
            "data": [
                {
                "TEACHER_ID": "12354812",
                "DEPARTMENT": "信息科学与工程学院",
                "TEACHER_NAME": "迪斯科",
                },
                {
                ...其他教师
                }
            ]
        }

- 返回参数说明：

  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|
  |status|bool类型，true表示正确的返回，false表示有错误|
  |info|返回结果说明信息|
  |total|返回教师人数|
  |data|所有教师的课程信息数组|
  |TEACHER_ID|教师工号|
  |DEPARTMENT|教师所属部门|
  |TEACHER_NAME|真实姓名|
  

