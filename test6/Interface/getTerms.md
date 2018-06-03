<!-- markdownlint-disable MD033-->
<!-- 禁止MD033类型的警告 https://www.npmjs.com/package/markdownlint -->

# 接口：getTerms  [返回](../README.md)
  用例： [选学期](../UseCase/选学期.md)

- 权限：
    学生/访客：
    老师：

- 功能：
    返回所选学期。

- API请求地址：
   接口基本地址/v1/api/getTerms

- 请求方式 ：
    GET

- 请求参数说明:
    无

- 返回实例：

        {
            "status": true,
            "info": null,
            "total": 2,
            "data": [
                {
                "TERM_ID": 2,
                "TERM_YEAR": 2015,
                }，
                {
                ...其他课程
                }
            ]
        }

- 返回参数说明：

  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|
  |status|bool类型，true表示正确的返回，false表示有错误|
  |info|返回结果说明信息|
  |total|返回学期数|
  |data|所有学期信息的数组|
  |TERM_ID|学期编号|
  |TERM_YEAR|学年|
  


