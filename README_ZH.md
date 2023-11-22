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
