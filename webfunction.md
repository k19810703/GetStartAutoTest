# Get Started

## 创建一个目录
本例为mytest，名字请自行更改
```SHELL
mkdir mytest
cd mytest
npm init -y
npm install --save jest jest-html-reporters jest-puppeteer puppeteer lodash
npm install -g jest
```

打开package.json文件，找到scripts，按照如下修改
```JSON
  "scripts": {
    "test": "jest"
  },
```
