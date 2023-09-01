# hello-wo
直播内容

1. 多环境 5 - 10min
2. 项目部署上线 1h √
   - 原始前端 / 后端项目
   - 宝塔 Linux 
   - 容器
   - 容器平台
3. 前后端的联调 —— 跨域 15 min
4. 用户中心项目扩展和规划（优化点）5 - 10 min



## 多环境

参考文章：https://blog.csdn.net/weixin_41701290/article/details/120173283

本地开发：localhost（127.0.0.1）

多环境：指同一套项目代码在不同的阶段需要根据实际情况来调整配置并且部署到不同的机器上。

为什么需要？

1. 每个环境互不影响
2. 区分不同的阶段：开发 / 测试 / 生产
3. 对项目进行优化：
   1. 本地日志级别
   2. 精简依赖，节省项目体积
   3. 项目的环境 / 参数可以调整，比如 JVM 参数

针对不同环境做不同的事情。



多环境分类：

1. 本地环境（自己的电脑）localhost
2. 开发环境（远程开发）大家连同一台机器，为了大家开发方便
3. 测试环境（测试）开发 / 测试 / 产品，单元测试 / 性能测试 / 功能测试 / 系统集成测试，独立的数据库、独立的服务器
4. 预发布环境（体验服）：和正式环境一致，正式数据库，更严谨，查出更多问题
5. 正式环境（线上，公开对外访问的项目）：尽量不要改动，保证上线前的代码是 “完美” 运行
6. 沙箱环境（实验环境）：为了做实验



### 前端多环境实战

- 请求地址

  - 开发环境：localhost:8000

  - 线上环境：user-backend.code-nav.cn

  ```js
  startFront(env) {
      if(env === 'prod') {
          // 不输出注释 
          // 项目优化
          // 修改请求地址
      } else {
          // 保持本地开发逻辑
      }
  }
  ```

  用了 umi 框架，build 时会自动传入 NODE_ENV == production 参数，start NODE_ENV 参数为 development

- 启动方式

  - 开发环境：npm run start（本地启动，监听端口、自动更新）
  - 线上环境：npm run build（项目构建打包），可以使用 serve 工具启动（npm i -g serve）

- 项目的配置

  不同的项目（框架）都有不同的配置文件，umi 的配置文件是 config，可以在配置文件后添加对应的环境名称后缀来区分开发环境和生产环境。参考文档：https://umijs.org/zh-CN/docs/deployment

  - 开发环境：config.dev.ts
  - 生产环境：config.prod.ts
  - 公共配置：config.ts 不带后缀

前端区分环境

### 后端多环境实战

SpringBoot 项目，通过 application.yml 添加不同的后缀来区分配置文件

可以在启动项目时传入环境变量：

```bash
java -jar .\user-center-backend-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

主要是改：

- 依赖的环境地址

  - 数据库地址

  - 缓存地址

  - 消息队列地址

  - 项目端口号

- 服务器配置



## 项目部署

参考文章：https://www.bilibili.com/read/cv16179200

需要 Linux 服务器（建议大家用 CentOS 8+ / 7.6 以上）

###  原始部署

什么都自己装
