# Get Started

##  前提
Node.js环境

## 初始化
本例为crossbrowser，名字请自行更改
```SHELL
mkdir crossbrowser
cd crossbrowser
npm init -y
npm install --save jest selenium-webdriver jest-html-reporters
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

拉取[jest-selenium](https://github.com/k19810703/jest-selenium)下所有.js文件，覆盖到本目录
```SHELL
wget https://github.com/k19810703/jest-selenium/archive/master.zip
unzip master.zip
mv ./jest-selenium-master/*.js ./
rm -rf jest-selenium-master
rm master.zip
```

下载必要的driver,[参考](https://selenium.dev/documentation/en/getting_started_with_webdriver/third_party_drivers_and_plugins/)

##  创建测试用例

创建文件case1.test.js
```javascript
jest.setTimeout(600000);

describe(`${process.env.browser||'firefox'} 豆瓣网`, () => {
  describe('权利的游戏 第8季', () => {
    beforeAll(async () => {
      await driver.get('https://movie.douban.com/subject/26584183/');
    });

    test('豆瓣评分 6.1', async () => {
      const score = await driver.findElement(By.xpath('/html/body/div[3]/div[1]/div[2]/div[1]/div[1]/div[1]/div[2]/div/div[2]/strong'));
      const text = await score.getAttribute('textContent')
      await expect(text).toBe('6.1');
    });

    test('导演: 米格尔·萨普什尼克,大卫·纳特,戴维·贝尼奥夫,D·B·威斯', async () => {
      const expected = ['米格尔·萨普什尼克', '大卫·纳特', '戴维·贝尼奥夫', 'D·B·威斯'];
      const directors = await driver.findElements(By.xpath('/html/body/div[3]/div[1]/div[2]/div[1]/div[1]/div[1]/div[1]/div[2]/span[1]/span[2]/a'));
      const texts = await Promise.all(directors.map(direcctor => direcctor.getAttribute('textContent')));
      expect(texts).toEqual(expect.arrayContaining(expected));
    });
  })
})
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

指定浏览器执行，不指定时默认firefox
```SHELl
browser=safari jest
```

测试报告　${browser}_reporter.html

报告sample参考[功能测试报告](webfunction.md)

