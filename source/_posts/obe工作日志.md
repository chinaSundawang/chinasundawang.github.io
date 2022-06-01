---
title: 工作
type:
  - 工作
tags: workharding
categories: wordhard
comments: true
abbrlink: '29206147'
date: 2022-05-11 13:57:21
---
# 工作日志 
## OBE 工作日志
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
8. 基本信息课程下拉double 需要改进
### 疑问
1. 为什么直接用name查询，不用code进行查询

### 页面及相关表
#### 人才培养方案
- 人才培养方案列表 
    <pre> /plans : obe_cultivation_plan (人陪表) </pre>
- 删除人陪信息 
    <pre> /plan/delete : obe_cultivation_plan</pre>
- 提交审核 
    <pre> /plan/auditing/{planCode} : obe_cultivation_plan</pre>
- 人才方案撰写: 
    - 人陪信息 
        - 保存人陪信息 <pre>  /plan : obe_cultivation_plan、obe_plan_class（人培班级关系表）</pre> 
    - 培养目标 
        - 提交培养目标 <pre>  /goals/status : obe_plan_status </pre>  
        - 保存培养目标拆分点 <pre>  /goals/split : obe_goals （培养目标关系表）、obe_goals_split （培养目标拆解表）</pre> 
        - 保存培养目标 <pre> /goals : obe_goals </pre> 
    - 毕业要求 
        - 保存毕业要求  <pre> /graduate : obe_graduate (毕业要求表)</pre> 
        - 保存拆解指标点 <pre>  graduate/split : obe_graduate 、obe_graduate_split(毕业要求拆解表)</pre> 
        - 提交毕业要求  <pre> /graduate/status/{planCode} : obe_plan_status </pre> 
        - 查询毕业要求模板信息 <pre>  /graduate/templates : obe_graduate_template (毕业要求模板表)</pre> 
        - 查询毕业要求信息 <pre>  /graduate/info : obe_graduate 、obe_graduate_split </pre> 
        - 查询毕业要求支撑矩阵 
          <pre>  /graduate/split/matrix/{planCode} : obe_graduate_split、obe_graduate、obe_goals_graduate_weight（课程体系与毕业要求权重矩阵）、obe_goals、obe_goals_split </pre> 
        - 保存毕业要求支撑矩阵的权重  
          <pre>  /graduate/split/matrix/weight : obe_goals_graduate_weight </pre> 
    - 课程体系 
        - 保存课程体系 <pre>  /courseSystem : obe_course_system (课程体系表) </pre> 
        - 查询课程体系 <pre>  /courseSystemList/{planCode} : obe_course_system 、obe_cultivation_plan </pre> 
        - 查询课程体系统计信息 <pre> /courseSystem/statistics/{planCode} : obe_course_system </pre>
        - 查询课程体系支撑矩阵 <pre> /courseSystem/matrix/{planCode} : obe_graduate_split、obe_graduate、obe_course_graduate_weight（课程体系与毕业要求权重矩阵）、obe_course_system、obe_cultivation_plan  </pre>
        - 保存课程体系支撑矩阵的权重 <pre> /courseSystem/matrix/weight : obe_course_graduate_weight</pre>
    - 毕业条件
        - 保存扩展信息 <pre> /planCertificate/extra : obe_plan_extra (人培方案毕业条件)</pre>
        - 查询扩展信息 <pre> /planCertificate/extra/info/{planCode} : obe_plan_extra</pre>
        - 保存取证要求 <pre> /planCertificate : obe_plan_certificate (人陪需要证书表)</pre>
    - 其他说明
        - **同毕业条件**
- 如图 :
- ![](https://imgur.com/INaUOdV.png)
## 2022年5月16日 工作日志
### 达成目标
- 将课程大纲模板问题解决
- 泳道图设计
### 问题或建议
1. 课程大纲编辑选择人才方案为空，应该有问题 待改进。
2. 
### 疑问

### 课程大纲管理如下图
![](https://i.imgur.com/0u8twIb.png)
## 2022年5月17日 工作日志
### 问题或建议
1. 查看教学研讨接口报错 
### 教学过程管理如图
![](https://i.imgur.com/mCiYNzl.png)
## 2022年5月18日 工作日志
### 有联系的表的相关图
![](https://imgur.com/OXY4JGB.png)

### 接下来要做的
- 验证这个有联系的表之间知否做到了数据的互通。
  - obe_cultivation_plan 通
### obe问题
#### 人才培养方案
1. <del> 课程体系接口有点慢 </del>
2. 毕业条件接口存在循环调用问题
3. 课程体系查询存在重复查询问题 planCode = PL202204071119520566
4. 提交毕业要求接口（/graduate/status/）权重配置错误的情况 未正确返回提示。
6. 毕业条件页面 如果保存的列表为空，则无法切换其他页面并且没有提示
7. 毕业条件删除没有提示。
8. 人陪列表学院筛选失败
#### 课程大纲管理
1. 点击新建课程大纲，查询单个课程体系接口报错（405）前端传参错误造成
2. 保存成功没有前端提示
3. 基本信息课程下拉double 需要改
4. 考核方案  设计说明 保存不上
5. 课程大纲列表删除没反应
6. 提交审核之后不自动刷新列表
7. 课程大纲管理列表学院筛选失败
#### 教学过程管理
- 资料管理 下载失败！

## 2022年5月31日 
### 目前的成果：
1. 做了功能测试，提出了一些问题
2. 已经将后台的bug修复完成
3. 关于obe的项目已经达到可开发新模块和改动原有模块的程度，能够了解大体业务数据的流通
4. 已将obe涉及的核心表，泳道流程图，整理并以图的方式输出。

### 目前问题：
1. obe达不到交付的标准。
2. 缺乏完成的标准，开发目标模糊。
	1. 比如数据什么条件下算通
	2. 还有bug的改动在什么标准算完成，性能问题这期是否需要完善。
	3. 等等...
3.bug改动需要前端协助。

### 针对以上问题的个人建议：
1. 优先明确obe的完善标准，有明确清晰的开发目标
2. 有了明确的目标之后，在通过各岗位人员之间的协作完善此项目