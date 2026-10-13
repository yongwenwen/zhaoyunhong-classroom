# 课堂词云：Bmob 短期配置

本页词云通过 Bmob REST API 共享提交。只需云数据库，不需要购买云函数或启用数据监听。代码每 15 秒刷新一次；页面隐藏时暂停轮询。

## 1. 创建开发版应用

在 [Bmob 后端云](https://www.bmobapp.com/) 注册并创建开发版应用。Bmob 价格页当前列出的开发版为 0 元/3 个月、100 万次数据 API；以控制台当时显示的套餐和额度为准。

## 2. 创建数据表

在应用的「数据」中创建 Class：

- Class 名称：`ClassroomWordcloudSubmission`
- 字段：`text`，类型为字符串
- `createdAt` 由 Bmob 自动生成，不需要创建

## 3. 设置表权限

在该 Class 的「更多 / 权限设置」中，启用 ACL，并设置：

- 公开读取：允许
- 公开创建：允许
- 更新和删除：不允许公开访问

词云面向课堂公开提交，公开创建也意味着任何访问者都可能提交内容。仅使用 REST API Key，不要把 Master Key 放进网页。

## 4. 获取 API 测试域名和应用凭证

在应用设置中找到 API 域名管理，复制控制台分配的**API 测试域名**。开发版测试域名有请求限制；Bmob 文档要求正式上线前改用自有备案域名。本方案用于短期课堂活动。

在「应用密钥」中复制：

- Application ID
- REST API Key

不要复制 Master Key。

## 5. 发布前确认

代码分支中的 `index.html` 已填写 API 域名、Application ID 和 REST API Key。合并到 `main` 前，请先确认：

- `ClassroomWordcloudSubmission` 表已经创建，且含字符串字段 `text`
- 表 ACL 允许公开读取和创建，禁止公开更新、删除
- Bmob 控制台中的 API 域名与页面配置一致

公开网页中的 REST API Key 对访问者可见，因此必须保持上述表权限。不要把 Master Key 放进网页。合并后 GitHub Pages 会通过 Bmob 保存提交；现有网页地址和二维码无需改变。

## 来源

- [Bmob 套餐价格](https://old.bmobapp.com/prices)
- [Bmob API 域名与测试域名说明](https://doc.bmobapp.com/other/domain/)
- [Bmob REST API](https://doc.bmobapp.com/data/restful/develop_doc/)
- [Bmob 数据安全](https://doc.bmobapp.com/other/data_safety/)
