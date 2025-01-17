# 日期处理

在抓取网页的时候，通常情况下网页会提供日期。这篇教程用于说明插件应当如何正确的处理相关情况

## 没有日期

在源没有提供日期的时候，**请勿添加日期**。`pubDate`选项应当被留空。

## 规范

`pubDate`接受一个[Date Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)。或者是可以被正确解析的字符串。这里**并不推荐直接返回字符串的方式**，因为其行为可能在不同环境下不一致，[Date.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)

## 使用工具类

目前，我们推荐使用[dayjs](https://github.com/iamkun/dayjs)进行日期的处理和时区调整。相关工具类有两个：

### Parse Date

这个是一个工具类用于使用[dayjs](https://github.com/iamkun/dayjs)。大部分情况下，应当可以直接使用他获取到正确的`Date Object`  

具体解析参数请参考dayjs github说明

```javascript
const parseDate = require('@/utils/parse-date');

const pubDate = parseDate('2020/12/30', 'YYYY/MM/DD')
```


### Timezone

部分网站并不会依据访问者来源进行时区转换，此时获取到的时间是网站本地时间，不一定适合所有RSS订阅者。此时，应当手动指定获取的时间时区：

::: warning 注意
此时，时间将会被转换到服务器时间，方便后续中间件处理。这个是正常流程！
:::

```javascript
const timezone = require('@/utils/timezone');

const pubDate = timezone(new Date(), +8)
```