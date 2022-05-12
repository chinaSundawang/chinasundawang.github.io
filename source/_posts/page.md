---
title: 工作
date: 2022-05-11 13:57:21
type:
- 工作
tags: workharding
categories: wordhard
---
# <center>工作日志 </center>
## <center>OBE 工作日志</center>
<!--more-->
### 达成目标
- 将人才培养模块熟悉并调试
- 整理调试过程中遇到的问题
- 整理obe项目数据流向
### 问题或建议
1. 支持筛选学院，但列表为展示学院信息。
![](https://imgur.com/NpLknDT.png)
2. 人陪信息-所属专业保存不成功  (默认是测试专业)
3. 同时修改多个培养目标，只保存最后一个修改过的
4. 课程体系接口有点慢
5. 毕业条件接口存在循环调用问题
6. 课程体系查询存在重复查询问题 planCode = PL202204071119520566
7. 提交毕业要求接口（/graduate/status/）权重配置错误的情况 未正确返回提示。
### 疑问
1. 为什么直接用name查询，不用code进行查询

### 页面及相关表
#### 人才培养方案
- 人才培养方案列表 - /plans : obe_cultivation_plan (人陪表)
- 删除人陪信息 - /plan/delete : obe_cultivation_plan
- 提交审核 - /plan/auditing/{planCode} : obe_cultivation_plan
- 人才方案撰写: 
    - 人陪信息 
        - 保存人陪信息 - /plan : obe_cultivation_plan、obe_plan_class（人培班级关系表）
    - 培养目标 
        - 提交培养目标 - /goals/status : obe_plan_status 
        - 保存培养目标拆分点 - /goals/split : obe_goals （培养目标关系表）、obe_goals_split （培养目标拆解表）
        - 保存培养目标 - /goals : obe_goals
    - 毕业要求 
        - 保存毕业要求 - /graduate : obe_graduate (毕业要求表)
        - 保存拆解指标点 - graduate/split : obe_graduate 、obe_graduate_split(毕业要求拆解表)
        - 提交毕业要求 - /graduate/status/{planCode} : obe_plan_status
        - 查询毕业要求模板信息 - /graduate/templates : obe_graduate_template (毕业要求模板表)
        - 查询毕业要求信息 - /graduate/info : obe_graduate 、obe_graduate_split