
# go api项目

## 程序结构

```bash
├── app                            // 程序具体逻辑代码
│   ├── cmd                         // 命令
│   │   ├── cache.go
│   │   ├── cmd.go
│   │   ├── key.go
│   │   ├── make                    // make 命令及子命令
│   │   │   ├── make.go
│   │   │   ├── make_apicontroller.go
│   │   │   ├── make_cmd.go
│   │   │   ├── make_factory.go
│   │   │   ├── make_migration.go
│   │   │   ├── make_model.go
│   │   │   ├── make_policy.go
│   │   │   ├── make_request.go
│   │   │   ├── make_seeder.go
│   │   │   └── stubs               // make 命令的模板
│   │   │       ├── apicontroller.stub
│   │   │       ├── cmd.stub
│   │   │       ├── factory.stub
│   │   │       ├── migration.stub
│   │   │       ├── model
│   │   │       │   ├── model.stub
│   │   │       │   ├── model_hooks.stub
│   │   │       │   └── model_util.stub
│   │   │       ├── policy.stub
│   │   │       ├── request.stub
│   │   │       └── seeder.stub
│   │   ├── migrate.go
│   │   ├── play.go
│   │   ├── seed.go
│   │   └── serve.go
│   ├── http                        // http 请求处理逻辑
│   │   ├── controllers             // 控制器，存放 API 和视图控制器
│   │   │   ├── api                 // API 控制器，支持多版本的 API 控制器
│   │   │   │   └── v1              // v1 版本的 API 控制器
│   │   │   │       ├── users_controller.go
│   │   │   │       └── ...
│   │   └── middlewares             // 中间件
│   │       ├── auth_jwt.go
│   │       ├── guest_jwt.go
│   │       ├── limit.go
│   │       ├── logger.go
│   │       └── recovery.go
│   ├── models                      // 数据模型
│   │   ├── user                    // 单独的模型目录
│   │   │   ├── user_hooks.go       // 模型钩子文件
│   │   │   ├── user_model.go       // 模型主文件
│   │   │   └── user_util.go        // 模型辅助方法
│   │   └── ...
│   ├── policies                    // 授权策略目录
│   │   ├── category_policy.go
│   │   └── ...
│   └── requests                    // 请求验证目录（支持表单、标头、Raw JSON、URL Query）
│       ├── validators              // 自定的验证规则
│       │   ├── custom_rules.go
│       │   └── custom_validators.go
│       ├── user_request.go
│       └── ...
├── bootstrap                       // 程序模块初始化目录
│   ├── app.go
│   ├── cache.go
│   ├── database.go
│   ├── logger.go
│   ├── redis.go
│   └── route.go
├── config                          // 配置信息目录
│   ├── app.go
│   ├── captcha.go
│   ├── config.go
│   ├── database.go
│   ├── jwt.go
│   ├── log.go
│   ├── mail.go
│   ├── pagination.go
│   ├── redis.go
│   ├── sms.go
│   └── verifycode.go
├── database                        // 数据库相关目录
│   ├── database.db                 // sqlite 数据文件（加入到 .gitignore 中）
│   ├── factories                   // 模型工厂目录
│   │   ├── user_factory.go
│   │   └── ...
│   ├── migrations                  // 数据库迁移目录
│   │   ├── 2021_12_21_102259_create_users_table.go
│   │   ├── 2021_12_21_102340_create_categories_table.go
│   │   └── ...
│   └── seeders                     // 数据库填充目录
│       ├── users_seeder.go
│       ├── ...
├── pkg                             // 内置辅助包
│   ├── app
│   ├── auth
│   ├── cache
│   ├── captcha
│   ├── config
│   └── ...
├── public                          // 静态文件存放目录
│   ├── css
│   ├── js
│   └── uploads                     // 用户上传文件目录
│       └── avatars                 // 用户上传头像目录
├── routes                          // 路由
│   ├── api.go
│   └── web.go
├── storage                         // 内部存储目录
│   ├── app
│   └── logs                        // 日志存储目录
│       ├── 2021-12-28.log
│       ├── 2021-12-29.log
│       ├── 2021-12-30.log
│       └── logs.log
└── tmp                             // air 的工作目录
├── .env                            // 环境变量文件
├── .env.example                    // 环境变量示例文件
├── .gitignore                      // git 配置文件
├── .air.toml                       // air 配置文件
├── .editorconfig                   // editorconfig 配置文件
├── go.mod                          // Go Module 依赖配置文件
├── go.sum                          // Go Module 模块版本锁定文件
├── main.go                         // Gohub 程序主入口
├── Makefile                        // 自动化命令文件
├── readme.md                       // 项目 readme
└── README.md                       // 项目 readme
```

## 目录说明

### requests 目录

请求验证目录，用于验证请求数据。支持表单、标头、Raw JSON、URL Query。
处理请求数据和表单验证
controllers 控制器调用 requests

## 入口文件 main.go

入口文件需要简单清晰。完成一些加载和初始化工作后，调用 `app.Run()` 启动程序。

## 添加第三方库

1. 使用 `go get` 命令安装第三方库，如 `go get github.com/gin-gonic/gin`
2. 写代码使用第三方库，如 `import "github.com/gin-gonic/gin"`
3. 使用 `go mod tidy` 命令整理依赖

## 功能开发步骤

1、创建目录和文件，或修改现有文件的逻辑。
2、编写测试用例，测试通过。
3、提交代码，通过 CI/CD 流程。
4、编写文档，提交代码。

### 功能开发

1、 分析功能，是否有现成的库。比如：发送邮件、发送短信、生成二维码、打印日志等。
2、记录日志
  2.1、分析对比市场上常用日志库，选择合适的日志库。
  2.2、我们将使用 Uber 开源的日志工具 zap （github.com/uber-go/zap） 来作为底层库。

## 代码优化

1、代码中有很多重复代码，我们需要对其进行优化，以提高代码的可维护性。
> Go 项目做重构时，一般先修改末端的代码。例如 A 依赖于 B ，B 依赖于 C。重构的顺序是先重构 C 然后是 B 最后是 A。
>
### 重复代码重构方法

  1. 重复部分提取封装
  2. 重复部分抽象成函数
  3. 重复部分抽象成结构体

# 日志系统设计

## 1. 什么是日志？

在我们项目中，使用日志来记录整个系统的运行情况。可能但是不限于：

- HTTP 请求数据
- 数据库 SQL 请求日志
- Panic/Error 错误日志
- 请求第三方接口日志（发送短信、发送邮件等）
- …

## 2. 日志的目的

记录日志的目的是什么？

方便调试，快速精准地帮我们定位问题。


## 命令行基础知识
三层结构里， 树状结构的最顶层是 APPNAME ，在我们这个项目中是 gohub，用来组织子命令用的。

### 命令的组成
命令的四个基本组成部分：

- 主命令（APPNAME）：命令最顶层；
- 命令（Command）：就是需要执行的操作；
- 参数（Arg）：参数即要操作的对象；
- 选项（Flag）：用以调整命令的行为。

```bash
APPNAME COMMAND ARG --FLAG(-f)
```