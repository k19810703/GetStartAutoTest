# Get Started

## 初始化
本例为mytest，名字请自行更改
```SHELL
mkdir mytest
cd mytest
npm init -y
npm install --save jest jest-html-reporters jest-puppeteer puppeteer lodash
npm install -g jest
```

初始化jest
```SHELL
jest --init
```

推荐如下配置
```
The following questions will help Jest to create a suitable configuration for your project

✔ Would you like to use Jest when running "test" script in "package.json"? … yes
✔ Choose the test environment that will be used for testing › node
✔ Do you want Jest to add coverage reports? … no
✔ Automatically clear mock calls and instances between every test? … no
```

打开jest.config.js，找到如下字段，取消注释并做相应修改
```
  maxWorkers: "1",
  preset: "jest-puppeteer",
  reporters: ["default", "jest-html-reporters"],
  testEnvironment: "node",
```

##  配置浏览器
推荐配置，更新配置参考,[puppeteer API](https://github.com/puppeteer/puppeteer/blob/v2.1.0/docs/api.md#puppeteerconnectoptions)
```SHELL
cat << EOF > jest-puppeteer.config.js
module.exports = {
  launch: {
    headless: process.env.headless === 'true',
    slowMo: 30,
    defaultViewport: {
      width: 1280,
      height: 600,
    },
  },
}
EOF
```
