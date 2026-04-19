# 云栖公寓 - 公寓租赁平台

尚庭公寓是一个完整的公寓租赁平台，包含**移动端**（用户找房、预约、签约）和**后台管理系统**（管理员管理房源、租约、用户等）。项目采用前后端分离架构，覆盖公寓租赁的核心业务流程：签约、续约、退租。

## ✨ 主要功能

### 📱 移动端

- 房源检索（多条件筛选、排序）
- 看房预约（选择公寓/时间，提交预约）
- 租约管理（查看合同、申请续约/退租）
- 浏览历史（记录查看过的房源）

### 🖥️ 后台管理系统

- 公寓/房间信息管理（增删改查、发布状态）
- 属性管理（支付方式、租期、标签、配套、杂费、房间属性）
- 看房预约处理
- 租约管理（创建、审核、终止）
- 用户管理（移动端用户、后台系统用户）
- 系统管理（岗位管理、用户权限）

## 🛠 技术栈

| 层级     | 技术                                                |
| :------- | :-------------------------------------------------- |
| 后端框架 | Spring Boot 3.0.5, MyBatis Plus 3.5.3               |
| 数据库   | MySQL 8.0, Redis 7.0（缓存、验证码）                |
| 对象存储 | MinIO（图片存储）                                   |
| 接口文档 | Knife4j (OpenAPI 3)                                 |
| 身份认证 | JWT                                                 |
| 验证码   | EasyCaptcha（图形验证码），阿里云短信（短信验证码） |
| 前端     | Vue 3                                               |
| 部署     | Nginx（反向代理 + 静态资源）                        |

## 📁 项目结构

text

```
lease
├── common          # 公共模块：工具类、全局异常、配置
├── model           # 数据模型：实体类、枚举
└── web
    ├── web-admin   # 后台管理模块（Controller/Service/Mapper）
    └── web-app     # 移动端模块
```



## 🚀 快速开始

### 1. 环境要求

- JDK 17
- MySQL 8.0
- Redis 7.0
- MinIO（或任意 S3 兼容对象存储）
- Maven 3.6+

### 2. 数据库初始化

sql

```
CREATE DATABASE lease CHARACTER SET utf8mb4;
-- 执行项目中的 lease.sql 脚本
```



### 3. 配置文件

在 `web-admin` 和 `web-app` 模块的 `application.yml` 中配置：

- MySQL、Redis、MinIO 连接信息
- 阿里云短信（可选，若不使用可屏蔽）

### 4. 启动后端

bash

```
# 进入项目根目录
mvn clean package
# 分别启动 admin 和 app 模块
java -jar web-admin/target/web-admin-1.0-SNAPSHOT.jar
java -jar web-app/target/web-app-1.0-SNAPSHOT.jar
```



### 5. 启动前端（可选）

- 移动端前端：`rentHouseH5`（Vue3）
- 管理后台前端：`rentHouseAdmin`（Vue3）

修改 `.env.development` 中的后端接口地址，然后：

bash

```
npm install
npm run dev
```



### 6. 访问

- 后台管理接口文档：`http://localhost:8080/doc.html`
- 移动端接口文档：`http://localhost:8081/doc.html`

## 📦 部署（生产环境）

详见项目文档中的 **部署准备** 和 **项目部署** 章节，典型部署架构：

- `server01`：部署 MySQL、Redis、MinIO、后端服务（jar）
- `server02`：部署 Nginx（代理前后端请求 + 托管前端静态资源）
- 配置域名映射（如 `lease.atguigu.com` 和 `admin.lease.atguigu.com`）

## 📄 开源协议

本项目仅供学习交流使用，无特定开源协议。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request。
