# AutoTestHighLevelGuide
自动化测试High Level Guide，通过本guide，希望帮助项目能够选择合适的自动化测试框架，开始自动化测试的落地

## 必要知识
1.  Docker
2.  docker-compose
3.  [css selector](https://www.w3.org/TR/CSS2/selector.html)
4.  [xpath](https://www.w3school.com.cn/xpath/index.asp)
5.  Node.js

## 测试环境构建

### 概要
推荐使用[docker-compose](https://docs.docker.com/compose/install/)来构建容器测试环境，每个被测系统都有一定的特殊性，需要根据实际情况来调整。

### 步骤
* build
  拉取代码，执行编译并打包成可部署的资产(jar,docker image等)
* deploy
  发布测试环境，包括被测应用，数据库以及周边需要mock的环境
* init
  执行必要的初始化job(导入必要数据，添加系统管理员用户等等)，使系统处于可以测试状态

##  周边系统的mock

### RestAPI服务的mock
推荐使用[jsonserver](https://github.com/typicode/json-server),可以在几分钟内启动一个符合rest标准的服务

## API自动化测试

参考我的[APITestGuide](https://github.com/k19810703/APITestGuide),包含了比较详细的guide，细节问题，联系wuhd@cn.ibm.com探讨

##  web应用的功能测试

### 概要
因为很多情况下会需要一些复杂的逻辑来完成测试和断言，full regression的功能测试不太建议使用0代码的2次开发自动化测试框架。

推荐使用[puppeteer](https://github.com/puppeteer/puppeteer)来做功能测试，这个框架可以在Chromium内核上执行自动化测试，相当稳定，文档也清晰，上手容易。

[cypress](https://github.com/cypress-io/cypress)也可以做一个选择。

### 推荐
* 测试框架：[puppeteer](https://github.com/puppeteer/puppeteer)
* Runner：[jest](https://jestjs.io/)
* 整合框架：[jest-puppeteer](https://github.com/smooth-code/jest-puppeteer)
* 报告：[jest-html-reporter](https://github.com/Hargne/jest-html-reporter)
如果希望sample的话，联系wuhd@cn.ibm.com

##  web应用的兼容性测试

### 方案概要
推荐使用[selenium](https://selenium.dev/)来做兼容性测试，兼容性测试建议使用2次开发好的框架来做

##  手机应用功能测试

### 方案概要
推荐使用[macaca](https://github.com/alibaba/macaca)

### 推荐
暂无，欢迎有需要的项目联系我来一起做一个试试

##  性能测试

### 方案概要
推荐使用[k6](https://github.com/loadimpact/k6)

### 推荐
暂无，欢迎有需要的项目联系我来一起做一个试试



