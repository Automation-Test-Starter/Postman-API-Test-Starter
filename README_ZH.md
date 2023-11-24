<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->
<div align="right"><strong>🇨🇳中文</a></strong>  | <strong><a href="./README.md">🇬🇧English</strong></div>
<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->

# Postman-API-Test-Starter

使用 Postman 进行 API 自动化测试的入门 QuickStart 项目文档。

- [Postman-API-Test-Starter](#postman-api-test-starter)
  - [介绍](#介绍)
    - [接口测试简介](#接口测试简介)
      - [什么是 API?](#什么是-api)
      - [什么是 API 测试？](#什么是-api-测试)
      - [API 测试类型](#api-测试类型)
      - [API 测试步骤](#api-测试步骤)
    - [Postman 与 newman 介绍](#postman-与-newman-介绍)
  - [项目依赖](#项目依赖)
  - [项目文件结构](#项目文件结构)
  - [从 0 到 1 搭建 Postman 接口自动化测试项目](#从-0-到-1-搭建-postman-接口自动化测试项目)
    - [新建项目文件夹](#新建项目文件夹)
    - [项目初始化](#项目初始化)
    - [安装依赖](#安装依赖)
    - [Postman 编写接口测试用例](#postman-编写接口测试用例)
      - [新建 Collection 和 Request](#新建-collection-和-request)
      - [编辑 Request 和编写测试用例](#编辑-request-和编写测试用例)
        - [get-demo](#get-demo)
        - [post-demo](#post-demo)
    - [Postman 编写测试环境配置文件](#postman-编写测试环境配置文件)
      - [添加环境变量](#添加环境变量)
      - [更新 Request](#更新-request)
      - [验证环境变量](#验证环境变量)
      - [导出环境变量和测试用例文件](#导出环境变量和测试用例文件)
    - [调整项目文件结构](#调整项目文件结构)
      - [新建 Env 和 Testcase 文件夹](#新建-env-和-testcase-文件夹)
      - [调整用例文件和环境变量文件](#调整用例文件和环境变量文件)
      - [调整 package.json 文件](#调整-packagejson-文件)
    - [运行测试用例](#运行测试用例)
  - [进阶用法](#进阶用法)
    - [输出 html 测试报告](#输出-html-测试报告)
      - [安装 newman-reporter-htmlextra 依赖包](#安装-newman-reporter-htmlextra-依赖包)
      - [调整 package.json](#调整-packagejson)
      - [运行测试用例输出 html 报告](#运行测试用例输出-html-报告)
      - [输出多种格式的测试报告](#输出多种格式的测试报告)
    - [CI/CD 持续集成](#cicd-持续集成)
      - [接入 github action](#接入-github-action)
    - [集成 allure 测试报告](#集成-allure-测试报告)
      - [安装 allure 测试报告依赖](#安装-allure-测试报告依赖)
      - [调整 package.json 中输出 allure 测试报告的脚本](#调整-packagejson-中输出-allure-测试报告的脚本)
      - [调整 Postman 测试用例](#调整-postman-测试用例)
      - [运行测试用例输出 allure 报告](#运行测试用例输出-allure-报告)
    - [常用测试脚本](#常用测试脚本)
      - [响应测试脚本](#响应测试脚本)
      - [请求前脚本](#请求前脚本)
    - [测试脚本中可用的第三方库](#测试脚本中可用的第三方库)
      - [chai.js 断言库方法](#chaijs-断言库方法)
        - [1. 安装 Chai](#1-安装-chai)
        - [2. 使用 BDD 风格断言](#2-使用-bdd-风格断言)
        - [3. 使用 TDD 风格断言](#3-使用-tdd-风格断言)
        - [4. Chai 支持的一些常用断言](#4-chai-支持的一些常用断言)
      - [使用 cheerio 操作 HTML 文件](#使用-cheerio-操作-html-文件)
      - [使用 tv4 来验证 JSON Schema](#使用-tv4-来验证-json-schema)
      - [生成 uuid](#生成-uuid)
        - [1. 安装 `uuid` 模块](#1-安装-uuid-模块)
        - [2. 生成 UUID](#2-生成-uuid)
        - [示例](#示例)
      - [使用 xml2js 将 XML 转换为 JavaScript 对象](#使用-xml2js-将-xml-转换为-javascript-对象)
      - [常用工具函数 util](#常用工具函数-util)
        - [1. `util.guid()` - 生成全局唯一标识符（GUID）](#1-utilguid---生成全局唯一标识符guid)
        - [2. `util.timestamp()` - 获取当前时间戳](#2-utiltimestamp---获取当前时间戳)
        - [3. `util.randomInt(min, max)` - 生成指定范围内的随机整数](#3-utilrandomintmin-max---生成指定范围内的随机整数)
        - [4. `util.unixTimestamp()` - 获取当前时间戳（Unix 时间戳，秒）](#4-utilunixtimestamp---获取当前时间戳unix-时间戳秒)
        - [5. `util.encodeBase64(str)` 和 `util.decodeBase64(base64Str)` - Base64 编码和解码](#5-utilencodebase64str-和-utildecodebase64base64str---base64-编码和解码)
        - [6. `util.each(obj, callback)` - 遍历对象或数组](#6-utileachobj-callback---遍历对象或数组)
        - [注意事项](#注意事项)
      - [stream 流操作](#stream-流操作)
        - [1. **读取流（Readable Streams）：**](#1-读取流readable-streams)
        - [2. **写入流（Writable Streams）：**](#2-写入流writable-streams)
        - [3. **转换流（Transform Streams）：**](#3-转换流transform-streams)
      - [定时器 timers](#定时器-timers)
        - [1. `setTimeout` - 延时执行](#1-settimeout---延时执行)
        - [2. `setInterval` - 定时执行重复操作](#2-setinterval---定时执行重复操作)
        - [3. 在 Postman 中使用](#3-在-postman-中使用)
      - [时间处理 events](#时间处理-events)
        - [1. 创建事件发射器](#1-创建事件发射器)
        - [2. 定义事件处理函数](#2-定义事件处理函数)
        - [3. 注册事件处理函数](#3-注册事件处理函数)
        - [4. 触发事件](#4-触发事件)
        - [示例](#示例-1)

## 介绍

### 接口测试简介

#### 什么是 API?

API:应用程序接口（全称：application programming interface），缩写为 API，是一种计算接口，它定义多个软件中介之间的交互，以及可以进行的调用（call）或请求（request）的种类，如何进行调用或发出请求，应使用的数据格式，应遵循的惯例等。它还可以提供扩展机制，以便用户可以通过各种方式对现有功能进行不同程度的扩展。一个 API 可以是完全定制的，针对某个组件的，也可以是基于行业标准设计的以确保互操作性。通过信息隐藏，API 实现了模块化编程，从而允许用户实现独立地使用接口。

#### 什么是 API 测试？

接口测试是[软件测试](https://zh.wikipedia.org/wiki/软件测试)的一种，它包括两种测试类型：狭义上指的是直接针对[应用程序接口](https://zh.wikipedia.org/wiki/应用程序接口)（下面使用缩写 API 指代，其中文简称为接口）的功能进行的测试；广义上指[集成测试](https://zh.wikipedia.org/wiki/集成测试)中，通过调用 API 测试整体的功能完成度、可靠性、安全性与性能等指标。

API Best Practice:

- API 定义遵循 RESTFUL API 风格，语意化的 URI 定义，准确的 HTTP 状态码，通过 API 的定义就可以知道资源间的关系
- 配有详细且准确的 API 文档（如 Swagger 文档）
- 对外的 API 可以包含版本号以快速迭代（如 https://thoughtworks.com/v1/users/）

测试四象限中不同象限的测试，其测试目的跟测试策略也不同，API 测试主要位于第二、第四象限

API 测试在测试金子塔中处于一个相对靠上的位置，主要站在系统、服务边界来测试功能和业务逻辑，执行时机是在服务完成构建、部署到测试环境之后再执行、验证。

#### API 测试类型

功能测试

- 正确性测试
- 异常处理
- 内部逻辑
- ……

非功能测试

- 性能
- 安全
- ……

#### API 测试步骤

- 发送请求
- 得到响应
- 验证响应结果

### Postman 与 newman 介绍

Postman 是一个流行的 API 开发工具，它提供了一个易于使用的图形界面，可用于创建，测试和调试 API。Postman 还提供了一个可以轻松编写和共享测试脚本的功能。它支持多种 HTTP 请求方法，包括 GET，POST，PUT，DELETE 等，并且可以使用各种身份验证和授权方式来测试 API。

Newman 是 Postman 的命令行工具，可用于在不使用 Postman GUI 的情况下运行测试集。使用 Newman，用户可以轻松地将 Postman 集合导出为一个可执行文件，并在任何环境中运行它。此外，Newman 还支持生成 HTML 或 Junit 格式的测试报告，以及集成到 CI/CD 管道中以实现自动化测试。

总的来说，Postman 是一个强大的 API 开发和测试工具，而 Newman 则是一个方便的命令行工具，用于在不使用 Postman GUI 的情况下运行测试集。它们的结合使用可以提高 API 测试和开发的效率和准确性。

除了基本功能，Postman 还具有以下特性：

1. 环境和变量管理：Postman 支持在不同环境之间切换，例如在开发、测试和生产环境之间切换。同时，它还支持变量管理，可以轻松地为不同的测试用例和请求设置变量。
2. 自动化测试：用户可以使用 Postman 创建和运行自动化测试，以便在持续集成或部署流程中集成。这使得测试变得更加准确和高效。
3. 协作和共享：Postman 支持将集合和环境与团队共享，方便团队成员之间的协作。
4. 监控：Postman 还提供 API 监控功能，可以实时监控 API 的可用性和性能。

而 Newman 则主要有以下特点：

1. 命令行接口：Newman 可以在命令行中运行，因此可以方便地自动化测试和集成到 CI/CD 流程中。
2. 支持多种输出格式：Newman 支持多种输出格式，包括 HTML、JSON 和 JUnit 格式，方便用户在不同场景下使用。
3. 并发执行：Newman 支持并发执行测试，从而提高了测试的效率。
4. 轻量级：与 Postman GUI 相比，Newman 是一个轻量级的工具，因此在运行测试时需要更少的资源。

总之，Postman 和 Newman 是现代 API 测试的重要工具，它们提供了强大的功能，可以使 API 测试变得更加高效、准确和自动化。

除了上述提到的功能和特点，Postman 和 Newman 还有其他一些重要的功能和优势：

1. 集成：Postman 和 Newman 可以与许多其他工具和服务进行集成，例如 GitHub、Jenkins、Slack 等。这使得它们可以轻松地集成到开发和部署流程中，以实现更高效的 API 开发和测试。
2. 文档生成：Postman 可以使用 API 的请求和响应来生成 API 文档。这可以使 API 文档更加准确和及时。
3. 测试脚本：Postman 可以使用 JavaScript 编写测试脚本，这可以使测试变得更加灵活和自定义。用户可以轻松地编写自定义测试脚本，以确保 API 的行为符合预期。
4. 历史记录：Postman 可以存储 API 请求的历史记录，这可以方便用户查看和管理以前的请求和响应。这对于调试和问题排查非常有用。
5. 多平台支持：Postman 和 Newman 可以在多种平台上运行，包括 Windows、MacOS 和 Linux 等。

总之，Postman 和 Newman 是现代 API 测试和开发的强大工具。它们提供了丰富的功能和灵活的测试脚本，可以帮助开发人员和测试人员更快、更准确地构建和测试 API。

## 项目依赖

> 需提前安装好以下环境

- [x] nodejs, demo 版本为 v21.1.0
- [x] Postman 安装完成，可通过官方网站下载安装包进行安装

## 项目文件结构

以下是一个 Postman 和 Newman 的接口自动化测试项目的文件结构，其中包含了测试配置文件、测试用例文件、测试工具文件和测试报告文件。可进行参考。

```Text
Postman-Newman-demo
├── README.md
├── package.json
├── package-lock.json
├── Data // 测试配置文件
│   └── testdata.csv // 测试数据
├── Testcase // 测试用例文件夹
│   └── APITestDemo.postman_collection.json // 测试用例文件
├── Env // 不同测试环境文件夹
│   └── DemoEnv.postman_environment.json // 测试环境配置文件
├── Report // 测试报告文件
│   └── report.html
├── .gitignore
└── node_modules // 项目依赖
```

## 从 0 到 1 搭建 Postman 接口自动化测试项目

下面会介绍从 0 到 1 搭建一个 Postman 和 Newman 的接口自动化测试项目，包括测试配置、测试用例、测试环境、测试工具和测试报告等。

可参考 demo 项目：<https://github.com/Automation-Test-Starter/Postman-Newman-demo>

### 新建项目文件夹

```bash
mkdir Postman-Newman-demo
```

### 项目初始化

```bash
// 进入项目文件夹下
cd Postman-Newman-demo
// nodejs 项目初始化
npm init -y
```

### 安装依赖

> 目前 newman 最新版本在 html 测试报告的一些包兼容性上有问题，所以这里使用 5.1.2 版本

```bash
// 安装 newman
npm install newman@5.1.2--save-dev
```

### Postman 编写接口测试用例

#### 新建 Collection 和 Request

1. 打开 Postman，点击左上角的 New 按钮，选择 Collection，输入 Collection 的名称，点击 Create Collection 按钮，创建一个名称为 demo 的 Collection。
2. 在 Collection 中，点击右上角的三个点，选择 Add Request，输入 Request 的名称，点击 Save 按钮，创建一个 Request 命名为 get-demo。再添加一个 Request 命名为 post-demo。

#### 编辑 Request 和编写测试用例

可根据项目文件下的 demoAPI.md 文件中的接口文档，获取 demo 使用的 Request 的 URL、请求方法、请求头、请求体等信息。

##### get-demo

- 在 get-demo 的 Request 中，选择 GET 请求方法，输入 URL 为<https://jsonplaceholder.typicode.com/posts/1>
- 在 Headers 中，添加一个 Key 为 Content-Type，Value 为 application/json; 的请求头。
- 在 Tests 下，添加以下脚本，用于验证响应结果：

```JavaScript
pm.test("res.status should be 200", function () {
  pm.response.to.have.status(200);
});
pm.test("res.body should be correct", function() {
  var data = pm.response.json();
  pm.expect(data.id).to.equal(1);
  pm.expect(data.title).to.contains('provident');
});
```

- 点击 Send 按钮，发送请求，验证响应结果。

![2023112117P6poCX](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112117P6poCX.png)

确认响应结果正确后，点击 Save 按钮，保存 Request。

##### post-demo

- 在 post-demo 的 Request 中，选择 POST 请求方法，输入 URL 为<https://jsonplaceholder.typicode.com/posts>
- 在 Headers 中，添加一个 Key 为 Content-Type，Value 为 application/json; 的请求头。
- 在 Body 中，选择 raw，选择 JSON 格式，输入以下请求体：

```JSON
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
```

- 在 Tests 下，添加以下脚本，用于验证响应结果：

```JavaScript
pm.test("res.status should be 201", function () {
  pm.response.to.have.status(201);
});
pm.test("res.body should be correct", function() {
  var data = pm.response.json();
  pm.expect(data.id).to.equal(101);
  pm.expect(data.title).to.equal('foo');
});
```

![2023112117x34eSN](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112117x34eSN.png)

确认响应结果正确后，点击 Save 按钮，保存 Request。

### Postman 编写测试环境配置文件

下面会取接口请求的 host 为环境变量来进行 demo

#### 添加环境变量

- 在 Postman 的右上角，点击齿轮图标，选择 Manage Environments，点击 Add 按钮，输入环境名称为 DemoEnv，点击 Add 按钮，创建一个名称为 DemoEnv 的环境。
- 编辑环境变量，添加一个 Key 为 host，Value 为<https://jsonplaceholder.typicode.com>的环境变量。
- 点击 Add 按钮，保存环境变量。

#### 更新 Request

- 在 get-demo 的 Request 中，更新 URL 为{{host}}/posts/1
- 在 post-demo 的 Request 中，更新 URL 为{{host}}/posts

#### 验证环境变量

- 在 Postman 的右上角，点击齿轮图标，选择 DemoEnv，切换环境变量为 DemoEnv。
- 选择 get-demo 的 Request，点击 Send 按钮，发送请求，验证响应结果。确认响应结果正确后，点击 Save 按钮，保存 Request。
- 选择 post-demo 的 Request，点击 Send 按钮，发送请求，验证响应结果。确认响应结果正确后，点击 Save 按钮，保存 Request。

#### 导出环境变量和测试用例文件

- 在 Postman 的右上角，点击齿轮图标，选择 Export，选择 DemoEnv，点击 Export 按钮，导出环境变量。
- 选择 get-demo request 和 post-demo request 所在的 demo Collection，点击右上角的三个点，选择 Export，选择 Collection v2.1，点击 Export 按钮，导出测试用例文件。

### 调整项目文件结构

#### 新建 Env 和 Testcase 文件夹

- 在项目文件夹下，新建一个名为 Env 的文件夹，用于存放环境变量文件。

```bash
// 新建 Env 文件夹
mkdir Env
```

- 在项目文件夹下，新建一个名为 Testcase 的文件夹，用于存放测试用例文件。

```bash
// 新建 Testcase 文件夹
mkdir Testcase
```

#### 调整用例文件和环境变量文件

将导出的环境变量文件和测试用例文件放到项目文件夹下的 Env 和 Testcase 文件夹下。

![2023112117ePiBiv](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112117ePiBiv.png)

#### 调整 package.json 文件

- 在 package.json 文件中，添加以下脚本，用于运行测试用例：

```JSON
"scripts": {
    "test": "newman run Testcase/demo.postman_collection.json -e Env/DemoEnv.postman_environment.json"
}
```

### 运行测试用例

```bash
npm run test
```

![2023112117lt8FW9](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112117lt8FW9.png)

## 进阶用法

以下会介绍 Postman 和 Newman 的一些进阶用法，包括测试数据、测试脚本、测试报告和测试报告集成等。
也会介绍如何将 Postman 和 Newman 集成到 CI/CD 流程中，以实现自动化测试。

### 输出 html 测试报告

demo 会以集成[newman-reporter-htmlextra]([https://npm](https://github.com/DannyDainton/newman-reporter-htmlextra))为例，介绍如何输出 html 测试报告。

#### 安装 newman-reporter-htmlextra 依赖包

```bash
npm install newman-reporter-htmlextra --save-dev
```

> 注意：目前 newman 最新 V6 版本在 html 测试报告的一些包兼容性上有问题，所以这里使用 5.1.2 版本

#### 调整 package.json

在 package.json 文件中，更新测试测试脚本，用于运行测试用例并输出 html 测试报告：

```JSON
"test": "newman run Testcase/demo.postman_collection.json -e Env/DemoEnv.postman_environment.json -r htmlextra --reporter-htmlextra-export ./Report/Postman-newman-demo-api-testing-report.html"
```

> 指定输出 html 测试报告的路径为 Report/Postman-newman-demo-api-testing-report.html

#### 运行测试用例输出 html 报告

- 运行测试用例

```bash
 npm run test
```

- 检查报告文件

![2023112211zs7xCl](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112211zs7xCl.png)

- 浏览器打开报告文件

![2023112211IHIUzV](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112211IHIUzV.png)

#### 输出多种格式的测试报告

前面的配置是输出 html 格式的测试报告，如果想要输出多种格式的测试报告，如命令行 cli 的报告，可以在 package.json 文件中添加以下脚本：

```JSON
"test": "newman run Testcase/demo.postman_collection.json -e Env/DemoEnv.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export ./Report/Postman-newman-demo-api-testing-report.html"
```

再次运行测试用例，可以看到在 Report 文件夹下，除了 html 格式的测试报告，还有 cli 格式的测试报告。

![202311221109B7Fg](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/202311221109B7Fg.png)

### CI/CD 持续集成

将接口自动化测试的代码集成到 CI/CD 流程中，可以实现自动化测试，提高测试效率。

#### 接入 github action

以 github action 为例，其他 CI 工具类似

可参考 demo：<https://github.com/Automation-Test-Starter/Postman-Newman-demo>

创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 postman.yml。

编辑 postman.yml 文件：将以下内容复制到文件中

```YAML
name: RUN Postman API Test CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  RUN-Postman-API-Test:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [ 18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'

      - name: Installation of related packages
        run: npm ci

      - name: RUN SuperTest API Testing
        run: npm test

      - name: Archive Postman test report
        uses: actions/upload-artifact@v3
        with:
          name: Postman-test-report
          path: Report

      - name: Upload Postman report to GitHub
        uses: actions/upload-artifact@v3
        with:
          name: Postman-test-report
          path: Report
```

- 提交代码：将 postman.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 RUN-Postman-API-Test 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。

![2023112213AFVWZe](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112213AFVWZe.png)

### 集成 allure 测试报告

allure 是一个轻量级的、灵活的、多语言支持的测试报告工具，可以生成各种各样的测试报告，包括饼图、柱状图、曲线图等，可以方便地查看测试结果。

#### 安装 allure 测试报告依赖

```bash
npm install newman-reporter-allure --save-dev
```

#### 调整 package.json 中输出 allure 测试报告的脚本

```JSON
"test": "newman run Testcase/demo.postman_collection.json -e Env/DemoEnv.postman_environment.json -r cli,allure --reporter-allure-export ./allure-results"
```

#### 调整 Postman 测试用例

- 调整 get-demo 的 Tests 脚本，添加以下脚本，用于生成 allure 测试报告：

```JavaScript
// @allure.label.suite=postman-new-api-testing-demo
// @allure.label.story="Verify-the-get-api-return-correct-data"
// @allure.label.owner="naodeng"
// @allure.label.tag="GETAPI"

pm.test("res.status should be 200", function () {
  pm.response.to.have.status(200);
});
pm.test("res.body should be correct", function() {
  var data = pm.response.json();
  pm.expect(data.id).to.equal(1);
  pm.expect(data.title).to.contains('provident');
});
```

- 调整 post-demo 的 Tests 脚本，添加以下脚本，用于生成 allure 测试报告：

```JavaScript
// @allure.label.suite=postman-new-api-testing-demo
// @allure.label.story="Verify-the-post-api-return-correct-data"
// @allure.label.owner="naodeng"
// @allure.label.tag="POSTAPI"

pm.test("res.status should be 201", function () {
  pm.response.to.have.status(201);
});
pm.test("res.body should be correct", function() {
  var data = pm.response.json();
  pm.expect(data.id).to.equal(101);
  pm.expect(data.title).to.equal('foo');
});
```

- 保存更改后的 postman 测试用例，重新导出测试用例文件并替换原来的测试用例文件。

#### 运行测试用例输出 allure 报告

- 运行测试用例

```bash
 npm run test
```

会在项目文件夹下生成 allure-results 文件夹，里面包含了测试用例的执行结果。

![2023112213YUMTwz](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112213YUMTwz.png)

- 预览 allure 测试报告

```bash
allure serve
```

![2023112214Aa77VG](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2023112214Aa77VG.png)

### 常用测试脚本

Postman 提供了测试脚本功能，可以使用 JavaScript 编写脚本来验证 API 的响应和行为。这些脚本可以在请求的“Tests”标签下添加，分为请求前脚本（Pre-request Script）和响应后脚本（Tests）两个部分。下面是一些常用的 Postman 和 Newman 测试脚本：

#### 响应测试脚本

1. **状态码检查：**

   ```javascript
   pm.test("Status code is 200", function () {
       pm.response.to.have.status(200);
   });
   ```

2. **响应时间检查：**

   ```javascript
   pm.test("Response time is less than 200ms", function () {
       pm.expect(pm.response.responseTime).to.be.below(200);
   });
   ```

3. **响应体 JSON 格式检查：**

   ```javascript
   pm.test("Response body is a valid JSON", function () {
       pm.response.to.be.json;
   });
   ```

4. **响应体字段值检查：**

   ```javascript
   pm.test("Response body contains expected value", function () {
       pm.expect(pm.response.json().key).to.eql("expectedValue");
   });
   ```

5. **响应体数组长度检查：**

   ```javascript
   pm.test("Response body array has correct length", function () {
       pm.expect(pm.response.json().arrayKey).to.have.lengthOf(3);
   });
   ```

6. **响应体属性存在性检查：**

   ```javascript
   pm.test("Response body has required properties", function () {
       pm.expect(pm.response.json()).to.have.property("key");
   });
   ```

#### 请求前脚本

1. **动态设置请求参数：**

   ```javascript
   pm.variables.set("dynamicVariable", "dynamicValue");
   ```

2. **使用全局变量设置请求头：**

   ```javascript
   pm.request.headers.add({ key: 'Authorization', value: pm.globals.get('authToken') });
   ```

3. **生成随机数并设置为变量：**

   ```javascript
   const randomNumber = Math.floor(Math.random() * 1000);
   pm.variables.set("randomNumber", randomNumber);
   ```

4. **签名生成或加密等操作：**

   ```javascript
   // 示例：使用 CryptoJS 进行 HMAC SHA256 签名
   const CryptoJS = require('crypto-js');
   const secretKey = 'yourSecretKey';
   const message = 'dataToSign';
   const signature = CryptoJS.HmacSHA256(message, secretKey).toString(CryptoJS.enc.Base64);
   pm.variables.set("signature", signature);
   ```

### 测试脚本中可用的第三方库

提供的 require 方法允许您使用沙箱内置库模块。下面列出了个人常用的可用库和示例
更多可用的库可以在[这里](https://learning.postman.com/docs/writing-scripts/script-references/postman-sandbox-api-reference/#using-external-libraries)找到

#### chai.js 断言库方法

在 Postman 的测试脚本中，你可以使用 Chai 断言库来编写断言，以验证你的 API 响应是否符合预期。Chai 提供了多种断言风格，包括 BDD（Behavior Driven Development）、TDD（Test Driven Development）等。以下是一些基本的 Chai 使用方法：

##### 1. 安装 Chai

在 Postman 的脚本环境中，你无需单独安装 Chai，因为 Postman 默认已经内置了 Chai。

##### 2. 使用 BDD 风格断言

在 Postman 的 "Tests" 部分中，你可以使用 Chai 的 BDD 风格断言，例如：

```javascript
// 引入 Chai 库
const chai = require('chai');

// 使用 BDD 风格断言
const expect = chai.expect;

// 示例：验证响应状态码为 200
pm.test('Status code is 200', function() {
    expect(pm.response.code).to.equal(200);
});

// 示例：验证响应体是 JSON
pm.test('Response body is JSON', function() {
    expect(pm.response.headers.get('Content-Type')).to.include('application/json');
});
```

##### 3. 使用 TDD 风格断言

```javascript
// 引入 Chai 库
const chai = require('chai');

// 使用 TDD 风格断言
const assert = chai.assert;

// 示例：使用 assert 断言响应状态码为 200
assert.equal(pm.response.code, 200, 'Status code should be 200');
```

##### 4. Chai 支持的一些常用断言

- **相等性：**

  ```javascript
  expect(actual).to.equal(expected);
  ```

- **包含：**
  
  ```javascript
  expect(actual).to.include(expected);
  ```

- **类型检查：**
  
  ```javascript
  expect(actual).to.be.a('string');
  ```

- **大于/小于：**
  
  ```javascript
  expect(actual).to.be.above(expected);
  expect(actual).to.be.below(expected);
  ```

- **空/非空：**
  
  ```javascript
  expect(actual).to.be.null;
  expect(actual).to.not.be.null;
  ```

- **深度相等性：**
  
  ```javascript
  expect(actual).to.deep.equal(expected);
  ```

以上只是 Chai 断言库的一些基本用法，你可以根据需要使用更多的断言方法和组合。Chai 提供了丰富的断言功能，可以满足各种测试需求。更多详细信息，请查阅 Chai 的官方文档：[Chai Documentation](https://www.chaijs.com/)。

#### 使用 cheerio 操作 HTML 文件

在 Postman 中，Cheerio 是一个基于 jQuery 的库，用于在服务器端操作 HTML 文档。它允许你使用类似于 jQuery 的语法来选择和操作 HTML 元素，非常适用于解析和提取 HTML 页面中的信息。在 Postman 中，你可以使用 Cheerio 库进行 HTML 响应的解析。以下是 Cheerio 在 Postman 中的基本用法：

1. **安装 Cheerio：**
   - 由于 Postman 使用的是 Node.js 运行时环境，你可以通过在 Postman 的脚本中安装 Cheerio 来使用它。在请求的 "Pre-request Script" 或 "Tests" 部分，可以使用以下方式安装 Cheerio：

   ```javascript
   // 安装 Cheerio
   const cheerio = require('cheerio');
   ```

2. **使用 Cheerio 解析 HTML：**
   - 在请求的 "Tests" 部分中，你可以使用 Cheerio 解析 HTML。以下是一个简单的例子：

   ```javascript
   // 从响应中获取 HTML 内容
   const htmlContent = pm.response.text();

   // 使用 Cheerio 解析 HTML
   const $ = cheerio.load(htmlContent);

   // 示例：从 HTML 中提取标题文本
   const titleText = $('title').text();
   console.log('Title:', titleText);

   // 示例：从 HTML 中提取所有链接的 href 属性
   const links = [];
   $('a').each(function () {
       const link = $(this).attr('href');
       links.push(link);
   });
   console.log('Links:', links);
   ```

   在上述例子中，`cheerio.load(htmlContent)` 用于加载 HTML 内容，并使用类似于 jQuery 的语法来选择和操作元素。

3. **注意事项：**
   - Cheerio 主要用于解析静态 HTML，对于使用 JavaScript 动态生成的内容，可能无法正常获取。在这种情况下，你可能需要考虑使用 Puppeteer 或其他支持 JavaScript 执行的工具。

这只是 Cheerio 在 Postman 中的基本用法。你可以根据具体的需求使用 Cheerio 提供的各种选择器和方法。请查阅 Cheerio 的官方文档以获取更详细的信息：[Cheerio Documentation](https://cheerio.js.org/)。

#### 使用 tv4 来验证 JSON Schema

在 Postman 中，tv4 是一个 JSON Schema 验证库，用于验证 JSON 数据是否符合给定的 JSON Schema。JSON Schema 是一种描述 JSON 数据结构的规范，它定义了 JSON 对象的属性、类型和其他约束。

以下是在 Postman 中使用 tv4 进行 JSON Schema 验证的基本步骤：

1. **安装 tv4 库：**
   - 由于 Postman 使用的是 Node.js 运行时环境，你可以通过在 Postman 的脚本中安装 tv4 来使用它。在请求的 "Pre-request Script" 或 "Tests" 部分，你可以使用以下方式安装 tv4：

   ```javascript
   // 安装 tv4
   const tv4 = require('tv4');
   ```

2. **定义 JSON Schema：**
   - 在 Postman 中，你可以在请求的 "Pre-request Script" 或 "Tests" 部分定义 JSON Schema。JSON Schema 可以作为一个 JavaScript 对象进行定义。以下是一个简单的例子：

   ```javascript
   // 定义 JSON Schema
   const jsonSchema = {
       "type": "object",
       "properties": {
           "name": { "type": "string" },
           "age": { "type": "number" }
       },
       "required": ["name", "age"]
   };
   ```

3. **使用 tv4 进行验证：**
   - 在请求的 "Tests" 部分，你可以使用 tv4 对 JSON 数据进行验证。以下是一个简单的例子：

   ```javascript
   // 获取响应的 JSON 数据
   const jsonResponse = pm.response.json();

   // 使用 tv4 进行 JSON Schema 验证
   const isValid = tv4.validate(jsonResponse, jsonSchema);

   // 检查验证结果
   pm.test('JSON is valid according to the schema', function() {
       pm.expect(isValid).to.be.true;
   });
   ```

   在上述例子中，`tv4.validate(jsonResponse, jsonSchema)` 用于验证 `jsonResponse` 是否符合 `jsonSchema` 定义的规范。验证结果存储在 `isValid` 变量中，然后使用 `pm.test` 来检查验证结果。

这只是 tv4 在 Postman 中的基本用法。你可以根据实际需求，定义更复杂的 JSON Schema，并使用 tv4 的其他功能进行更灵活的验证。请查阅 tv4 的官方文档以获取更详细的信息：[tv4 Documentation](https://github.com/geraintluff/tv4)。

#### 生成 uuid

在 Postman 中，你可以使用 `uuid` 模块来生成 UUID（Universally Unique Identifier），也被称为 GUID。以下是在 Postman 中使用 `uuid` 模块的基本用法：

##### 1. 安装 `uuid` 模块

在 Postman 的 "Pre-request Script" 或 "Tests" 部分，你可以使用以下方式安装 `uuid` 模块：

```javascript
// 安装 uuid 模块
const uuid = require('uuid');
```

##### 2. 生成 UUID

```javascript
// 生成 UUID
const generatedUUID = uuid.v4();
console.log('Generated UUID:', generatedUUID);
```

在上述例子中，`uuid.v4()` 用于生成一个基于随机数的 UUID。你可以在 Postman 脚本中使用生成的 UUID，例如将其设置为请求头或参数的值。

##### 示例

以下是一个在 Postman "Pre-request Script" 中生成 UUID 并设置为请求头的示例：

```javascript
// 安装 uuid 模块
const uuid = require('uuid');

// 生成 UUID
const generatedUUID = uuid.v4();

// 设置请求头
pm.request.headers.add({ key: 'X-Request-ID', value: generatedUUID });
```

在上述例子中，`X-Request-ID` 是一个常见的请求头，用于标识请求的唯一性。生成的 UUID 被设置为这个请求头的值，以确保每个请求都有唯一的标识。

请注意，Postman 在运行脚本时会自动执行安装依赖项的步骤，无需手动安装 `uuid` 模块。

#### 使用 xml2js 将 XML 转换为 JavaScript 对象

在 Postman 中，`xml2js` 是一个用于将 XML 转换为 JavaScript 对象的库。在 Postman 的脚本中，你可以使用 `xml2js` 来处理 XML 响应并将其转换为易于处理的 JavaScript 对象。以下是在 Postman 中使用 `xml2js` 的基本步骤：

1. **安装 xml2js 库：**
   - 由于 Postman 使用的是 Node.js 运行时环境，你可以通过在 Postman 的脚本中安装 `xml2js` 来使用它。在请求的 "Pre-request Script" 或 "Tests" 部分，你可以使用以下方式安装 `xml2js`：

   ```javascript
   // 安装 xml2js
   const xml2js = require('xml2js');
   ```

2. **解析 XML 响应：**
   - 获取 XML 响应后，你可以使用 `xml2js` 将其解析为 JavaScript 对象。以下是一个简单的例子：

   ```javascript
   // 获取响应的 XML 内容
   const xmlContent = pm.response.text();

   // 使用 xml2js 解析 XML
   xml2js.parseString(xmlContent, function (err, result) {
       if (err) {
           console.error('Error parsing XML:', err);
           return;
       }

       // result 是解析后的 JavaScript 对象
       console.log('Parsed XML:', result);
   });
   ```

   在上述例子中，`xml2js.parseString(xmlContent, function (err, result) {...}` 用于异步地解析 XML 内容。解析后的 JavaScript 对象存储在 `result` 中。

3. **处理解析后的 JavaScript 对象：**
   - 一旦你获得了解析后的 JavaScript 对象，你就可以按照普通的 JavaScript 对象处理方式访问和操作它的属性。

   ```javascript
   // 示例：访问解析后的 JavaScript 对象的属性
   const value = result.root.element[0].subelement[0]._;
   console.log('Value from parsed XML:', value);
   ```

   在上述例子中，`result.root.element[0].subelement[0]._` 是一个访问解析后对象属性的示例。具体的结构取决于你的 XML 结构。

这只是 `xml2js` 在 Postman 中的基本用法。你可以根据实际需求使用 `xml2js` 的其他功能，例如设置解析选项，处理命名空间等。请查阅 `xml2js` 的官方文档以获取更详细的信息：[xml2js Documentation](https://github.com/Leonidas-from-XIV/node-xml2js)。

#### 常用工具函数 util

在 Postman 中，`util` 是一个全局对象，提供了一些常用的实用工具函数，可以在 Postman 脚本中使用。以下是一些常见的 `util` 对象的用法：

##### 1. `util.guid()` - 生成全局唯一标识符（GUID）

```javascript
// 生成一个全局唯一标识符
const uniqueId = util.guid();
console.log('Unique ID:', uniqueId);
```

##### 2. `util.timestamp()` - 获取当前时间戳

```javascript
// 获取当前时间戳（毫秒）
const timestamp = util.timestamp();
console.log('Timestamp:', timestamp);
```

##### 3. `util.randomInt(min, max)` - 生成指定范围内的随机整数

```javascript
// 生成 1 到 100 之间的随机整数
const randomInt = util.randomInt(1, 100);
console.log('Random Integer:', randomInt);
```

##### 4. `util.unixTimestamp()` - 获取当前时间戳（Unix 时间戳，秒）

```javascript
// 获取当前时间戳（秒）
const unixTimestamp = util.unixTimestamp();
console.log('Unix Timestamp:', unixTimestamp);
```

##### 5. `util.encodeBase64(str)` 和 `util.decodeBase64(base64Str)` - Base64 编码和解码

```javascript
// Base64 编码
const encodedString = util.encodeBase64('Hello, World!');
console.log('Encoded String:', encodedString);

// Base64 解码
const decodedString = util.decodeBase64(encodedString);
console.log('Decoded String:', decodedString);
```

##### 6. `util.each(obj, callback)` - 遍历对象或数组

```javascript
// 遍历数组
const array = [1, 2, 3, 4];
util.each(array, function (value, index) {
    console.log(`Index ${index}: ${value}`);
});

// 遍历对象
const obj = { a: 1, b: 2, c: 3 };
util.each(obj, function (value, key) {
    console.log(`Key ${key}: ${value}`);
});
```

##### 注意事项

- 在 Postman 脚本中，可以通过 `util` 对象直接调用这些实用工具函数。
- `util` 对象提供的这些方法能够简化在 Postman 脚本中的一些常见任务，如生成随机数、处理时间戳等。
- 请注意查阅 Postman 的官方文档，因为 Postman 会不断更新和改进其脚本环境，可能会引入新的实用工具函数。

#### stream 流操作

在 Node.js 中使用流（Streams）通常用于处理大量的数据，可以有效地降低内存占用并提高性能。以下是一些在 Node.js 中使用流的基本用法，可以参考这些方法来处理数据或文件。

##### 1. **读取流（Readable Streams）：**

```javascript
const fs = require('fs');

// 创建可读流
const readableStream = fs.createReadStream('input.txt');

// 设置编码（如果是文本文件）
readableStream.setEncoding('utf-8');

// 处理数据
readableStream.on('data', function(chunk) {
    console.log('Received chunk:', chunk);
});

// 处理结束
readableStream.on('end', function() {
    console.log('Stream ended.');
});

// 处理错误
readableStream.on('error', function(err) {
    console.error('Error:', err);
});
```

##### 2. **写入流（Writable Streams）：**

```javascript
const fs = require('fs');

// 创建可写流
const writableStream = fs.createWriteStream('output.txt');

// 写入数据
writableStream.write('Hello, World!\n');
writableStream.write('Another line.');

// 结束写入
writableStream.end();

// 处理结束
writableStream.on('finish', function() {
    console.log('Write completed.');
});

// 处理错误
writableStream.on('error', function(err) {
    console.error('Error:', err);
});
```

##### 3. **转换流（Transform Streams）：**

```javascript
const { Transform } = require('stream');

// 创建转换流
const myTransform = new Transform({
    transform(chunk, encoding, callback) {
        // 转换数据
        const transformedData = chunk.toString().toUpperCase();
        this.push(transformedData);
        callback();
    }
});

// 管道连接读取流、转换流和写入流
readableStream.pipe(myTransform).pipe(writableStream);
```

这只是 Node.js 中使用流的一些基本用法。在 Postman 中，你可以在请求的脚本中使用这些方法，例如 "Pre-request Script" 或 "Tests" 部分，通过 Node.js 运行环境来执行这些脚本。请注意，Node.js 中的流 API 可以更复杂，例如通过使用 `pipeline` 函数来处理多个流的连接。

#### 定时器 timers

在 Postman 中，你可以使用 Node.js 的定时器功能来处理定时任务或延时执行的操作。以下是一些基本的 Node.js 定时器的用法，这些用法可以在 Postman 的脚本中使用。

##### 1. `setTimeout` - 延时执行

```javascript
// 延时执行操作
setTimeout(function() {
    console.log('Delayed operation.');
}, 2000); // 2000 毫秒（2 秒）
```

##### 2. `setInterval` - 定时执行重复操作

```javascript
// 定时执行重复操作
const intervalId = setInterval(function() {
    console.log('Repeated operation.');
}, 3000); // 3000 毫秒（3 秒）

// 取消定时执行
// clearInterval(intervalId);
```

##### 3. 在 Postman 中使用

在 Postman 中，你可以在 "Pre-request Script" 或 "Tests" 部分中使用这些定时器。例如，在 "Tests" 部分中延时执行操作：

```javascript
// 在 "Tests" 部分延时执行操作
setTimeout(function() {
    console.log('Delayed operation in Tests.');
}, 2000); // 2000 毫秒（2 秒）
```

请注意，在 Postman 的 "Pre-request Script" 或 "Tests" 部分执行的代码是在 Node.js 环境中运行的，因此你可以使用 Node.js 支持的大多数功能，包括定时器。

在以上例子中，`setTimeout` 会在指定的延时后执行一次操作，而 `setInterval` 会在每隔指定的时间间隔后执行一次操作。在 Postman 中，你可以根据实际需求使用这些定时器功能。

#### 时间处理 events

在 Postman 的脚本环境中，你可以使用 Node.js 的 `events` 模块来处理事件。`events` 模块提供了 `EventEmitter` 类，该类可以用于定义和触发事件。以下是在 Postman 中使用 Node.js 的 `events` 模块的一些基本用法：

##### 1. 创建事件发射器

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();
```

##### 2. 定义事件处理函数

```javascript
// 定义事件处理函数
function myEventHandler() {
    console.log('Event handled.');
}
```

##### 3. 注册事件处理函数

```javascript
// 注册事件处理函数
myEmitter.on('myEvent', myEventHandler);
```

##### 4. 触发事件

```javascript
// 触发事件
myEmitter.emit('myEvent');
```

##### 示例

在 Postman 的脚本环境中，你可以使用事件来实现异步操作的回调或处理。以下是一个简单的例子，演示如何在异步操作完成后触发事件：

```javascript
const EventEmitter = require('events');
const myEmitter = new EventEmitter();

// 模拟异步操作
function performAsyncOperation() {
    setTimeout(function() {
        console.log('Async operation completed.');
        // 触发事件
        myEmitter.emit('asyncOperationComplete');
    }, 2000);
}

// 注册事件处理函数
myEmitter.on('asyncOperationComplete', function() {
    console.log('Handling async operation completion.');
    // 这里可以执行异步操作完成后的处理逻辑
});

// 执行异步操作
performAsyncOperation();
```

在上述例子中，`performAsyncOperation` 函数模拟了一个异步操作，当该操作完成时，通过 `myEmitter.emit` 触发了 `asyncOperationComplete` 事件。在事件处理函数中，你可以编写处理异步操作完成后的逻辑。

请注意，在 Postman 的脚本中，异步操作的执行方式可能受到限制，因此在实际使用中需要谨慎考虑。
