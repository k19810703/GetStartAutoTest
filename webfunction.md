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
```javascript
  maxWorkers: "1",
  preset: "jest-puppeteer",
  reporters: ["default", "jest-html-reporters"],
  // testEnvironment: "node",
```

##  配置浏览器
推荐配置，更多配置[参考](https://github.com/puppeteer/puppeteer/blob/v2.1.0/docs/api.md#puppeteerconnectoptions)
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

##  创建测试用例

创建文件case1.test.js
```javascript
jest.setTimeout(600000);

describe('豆瓣网', () => {
  describe('权利的游戏 第8季', () => {
    beforeAll(async () => {
      await page.goto('https://movie.douban.com/subject/26584183/');
    });

    test('豆瓣评分 6.1', async () => {
      const score = await page.waitForXPath('/html/body/div[3]/div[1]/div[2]/div[1]/div[1]/div[1]/div[2]/div/div[2]/strong');
      const text = await page.evaluate(targetObject => targetObject.textContent, score);
      await expect(text).toBe('6.1');
    });

    test('导演: 米格尔·萨普什尼克,大卫·纳特,戴维·贝尼奥夫,D·B·威斯', async () => {
      const expected = ['米格尔·萨普什尼克', '大卫·纳特', '戴维·贝尼奥夫', 'D·B·威斯'];
      const directors = await page.$x('/html/body/div[3]/div[1]/div[2]/div[1]/div[1]/div[1]/div[1]/div[2]/span[1]/span[2]/a');
      const texts = await Promise.all(directors.map(direcctor => page.evaluate(targetObject => targetObject.textContent, direcctor)));
      expect(texts).toEqual(expect.arrayContaining(expected));
    });
  });
});
```

同理可以创建其他测试用例，jest默认的测试用例为*.test.js

##  执行测试用例
单个执行
```SHELL
jest case1
```

全部执行
```SHELl
jest
```

headless执行
```SHELl
headless=true jest
```

测试报告　jest_html_reporters.html
