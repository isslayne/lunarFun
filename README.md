# lunarFun
原生农历(阴历, 阴阳历)和公历(阳历)互相转换的插件

## 如何使用

### 直接下载引入
把项目文件夹下的 `./v2.0.0/lunarFun.js` 或压缩后的 `./v2.0.0/lunarFun.min.js` 下载到本地并引入。
```html
<script src="你存放的文件夹/lunarFun.min.js"></script>
<script>
    lunarFun.gregorianToLunal(1906, 1, 26); // [1906, 1, 2, false]
    lunarFun.lunalToGregorian(1906, 4, 30, true); // [1906, 6, 21]
</script>
```

### 使用 npm 引入
项目支持 npm 进入，打开终端运行下方的命令
```bash
npm i lunar-fun -save
```
然后在项目入口文件引入
```javascript
// ES6
import lunarFun from 'lunar-fun';
// node
const lunarFun = require('lunar-fun');
```

## 方法文档

| 方法名 | `gregorianToLunal(year, month, day)`                                                       |
| :------ | :----------------------------------------------------------------------------------------- |
| 功能   | 传入中国公历年月日返回农历年月日数组                                                       |
| 参数   | `year`: 四位数年； `month`: 月； `day`: 日； 注意：填入的参数都是中国公历年月日，必填。    |
| 返回值 | 返回农历年月日组成的数字，数组的第四个项是在输出年份为闰年的时候决定输出的月份是否是闰月； |

**例子**
```javascript
// 传入中国公历年月日返回农历年月日数组 
lunarFun.gregorianToLunal(1999, 6, 6); // [1999, 4, 23, false]
```

| 方法名 | `lunalToGregorian(year, month, day, isRun)`                                                                                                |
| :------ | :----------------------------------------------------------------------------------------------------------------------------------------- |
| 功能   | 传入中国农历年月日返回中国公历年月日数组                                                                                                   |
| 参数   | year: 四位数年； month：月； day：日； isRun：布尔值，传入的年份如果是闰年的话决定输入的农历月份是正常月份还是闰月，默认 `false` 正常月份; |
| 返回值 | 反正中国公历年月日数组                                                                                                                     |

**例子**
```javascript
// 传入中国农历年月日返回中国公历年月日数

// 传入农历的 "正常月份"
lunarFun.lunalToGregorian(1906, 4, 30); // [1906, 5, 23]
// 传入农历的 "闰月"
lunarFun.lunalToGregorian(1906, 4, 30, true); // [1906, 6, 21]
```

**更多方法请参考对应版本文件夹下的 `lunarFun.js` 文件，里面有详细的备注，以下仅列出方法名、功能及基础例子**

| 方法名                                            | 功能                                                                   | 例子                                                                                   |
| :------------------------------------------------ | :--------------------------------------------------------------------- | :------------------------------------------------------------------------------------- |
| `formatDate(dateObj, formatText)`                 | 格式化输出中国时间对象                                                 | `lunarFun.formatDate(new Date(), 'YYYY-MM-DD WT')` 输出: `"2020-07-07 星期二"`         |
| `getDateYMD(year, month, day)`                    | 输入中国公历年月日，返回其中国时间日期对象，时分秒不传默认 0           | `lunarFun.getDateYMD(2019,3,4).valueOf()` 输出 `1551628800000`                         |
| `distanceDate(date1, date2)`                      | 输入两个公历日期对象，输出两个日期间隔的天数                           | `lunarFun.distanceDate(new Date(1999, 6 - 1, 6), new Date(1997, 5-1, 13))`) 输出 `754` |
| `distanceLunarFirstDays(year, month, day, isRun)` | 输入中国农历日期，输出日期距离那年正月初一的天数                       | `lunarFun.distanceLunarFirstDays(1906, 4, 1, true)` 输出 `118`                         |
| `getLunarYearDaysTotal(year)`                     | 传入中国农历年份，输出那年所有的天数                                   | `lunarFun.getLunarYearDaysTotal(1999)` 输出 `354`                                      |
| `formatLunarDate(year, month, day, isRun)`        | 传入中国农历年月日返回其汉字表示                                       | `lunarFun.formatLunarDate(1906, 4, 22, true)` 输出 `"一九零六年闰四月廿二日"`          |
| `getLunarMonthNumberDays(year, month, isRun)`     | 传入中国农历年份和月份，输出对应月份的天数                             | `lunarFun.getLunarMonthNumberDays(1999, 6)` 输出 `29`                                  |
| `getMonthNumberDays(year, month)`                 | 传入中国公历年份和月份，输出对应月份的天数                             | `lunarFun.getMonthNumberDays(1999, 6)` 输出 `30`                                       |
| `getZodiac(year)`                                 | 传入中国公历年份，输出生肖，如果参数错误返回空字符串                   | `lunarFun.getZodiac(1999)` 输出 `"兔"`                                                 |
| `getEarthlyBranches(year)`                        | 传入中国公历年份，输出地支，如果参数错误返回空字符串                   | `lunarFun.getEarthlyBranches(1999)` 输出 `"卯"`                                        |
| `getHeavenlyStems(year)`                          | 传入中国公历年份，输出天干，如果参数错误返回空字符串                   | `lunarFun.getHeavenlyStems(1996)` 输出 `"丙"`                                          |
| `isLeapYear(year)`                                | 判断输入的中国公历年份是否是闰年                                       | `lunarFun.isLeapYear(1996)` 输出 `true`                                                |
| `toJSON(year, numStr)`                            | 传入中国农历年份和其对应的十六进制字符串信息，返回JS对象表示的农历数据 | 具体例子请查看下方的方法解析                                                           |

## 文件说明

### "/lunarData" 文件夹
此文件夹下保存从香港天文台爬取的数据， `lunarinfo` 保存的是已经转为十六进制字符串的数据， `lunarInfoFormat` 保存的是 `JSON` 格式的详细数据。

### "/lunarNpm" 文件夹
此文件夹下保存的是上传至 `npm` 服务器的内容，每次更新记得要手动更新 `package.json` 里的版本号。

### "/v1.0.0" 文件夹
此文件夹下保存的是 `v1.0.0` 版本的代码，其中 `lunarFun.js` 为源代码， `lunarFun.min.js` 为压缩后的代码， `test.html` 为简单的测试用例，打开页面后在控制台查看。

### "/v2.0.0" 文件夹
此文件夹下保存的是 `v2.0.0` 版本的代码，其中 `lunarFun.js` 为源代码， `lunarFun.min.js` 为压缩后的代码， `test.html` 为简单的测试用例，打开页面后在控制台查看。


## 更新日志

### 20200619
#### 更新
- 更新时区对插件的影响，现支持非中国时区（注意：大部分时区都正常，小部分时区受夏令时还有真实偏移量等影响可能存在误差。
- npm导入、浏览器导入等导入方法更新。

### 20191116
#### 发布
- 发布 v1.0.0 版本


## 农历数据说明
农历和公历不一样，农历年份信息和公历不一样，没有规律可遵循，都是由天文台观测计算。大部分公历换农历都是用查表法进行转换。

### 数据来源
- [香港天文台](https://gb.weather.gov.hk/gts/time/conversionc.htm) 获取农历 1901年 - 2099年 数据
- [asia-home](https://www.asia-home.com/china/nongli/year/2101/lang/cn.php) 获取农历 2100年数据 (这网站打开贼慢)

### 数据误差
由于计算数十年后的月相及节气时间可能会有数分钟的误差，若新月(即农历初一)或节气时间很接近午夜零时，相关农历月份或节气的日期可能会有一日之差别。  
这些情况会出现在（以下年份都是公历表示）
- 2057年09月28日、2089年09月04日、2097年08月07日 的新月
- 2021年的冬至(2021年12月21日)、2051年的春分(2051年03月20日)、2083年的立春(2083年02月03日)、2084年的春分(2084年03月19日)

### 一些常识
- 有闰月的年份中，农历节日只按原月算，不按闰月算，只有除夕例外，有闰腊月则过闰腊月除夕。（除夕是一年的最后一天的夜晚）
- 在一个公历里面不可能出现两个农历新年，农历春节(正月初一)在一月和二月之间，具体区间可自行查询。

### 年份表示
农历年份对应的不应该是数字形式，而是以立春为界限的干支表示法（例如：辛丑年、壬寅年等）  
这里为了代码理解方便，把**农历年份的正月初一所在的公历年份作为农历年份的数字表示**  
例如：公历1902年2月8日 是 壬寅年正月初一，所以 壬寅年对应的数字是1902

### 数据压缩
一开始是从网上获取各种十六进制的农历年份数据信息，但都不准确，无奈自己从香港天文台把自己想要的数据扒下来，初始数据格式如下：
```javascript
let lunarInfo = {
    // JSON 的 key 推荐是双引号括起来的字符串，虽然在 JS 中还可以用数字作为 key
    "1901": {
        "year": 1901, // 农历年份的数字表示
        "firstMonth": 2, // 农历年份正月初一对应的公历月份
        "firstDay": 19, // 农历年份正月初一对应的公历日子
        "isRun": false, // 是否是闰年
        "runMonth": 0, // 是闰年的话闰几月，非闰年为 0
        "runMonthDays": 0, // 是闰年的话闰月的天数，非闰年为 0
        "monthsDays": [29,30,29,29,30,29,30,29,30,30,30,29] // 正常十二个月的每月天数
    },
    // other coding...
}
```
200 个数据扒下来文件非常大，达到 30kb 多，压缩后大概 2kb。  
原始文件在 `lunarData/lunarInfoFormat.js`, 压缩后的文件在 `lunarData/lunarInfo.js`    
网上大多是用二进制表示然后压缩成十六进制，这里我也沿用，但各个位置上表示的数据确有差别。具体过程如下：    
用 24 位二进制数表示数据信息（二进制位数从右往左数）    

|      24      |       23-19        |       18-17        |  16-13   |   12-9   |   8-5    |   4-1    |
| :----------: | :----------------: | :----------------: | :------: | :------: | :------: | :------: |
| 表示闰月大小 | 正月初一对应的日子 | 正月初一对应的月份 | 正常月份 | 正常月份 | 正常月份 | 表示闰月 |

+ 1-4 位
    - 表示是否有闰月，如果没有，则 1-4 都为 0, 如果有闰月则用二进制表示闰几月，不足四位左边补零到四位。
+ 5-16 位
    - 表示农历正常月份(除闰月) 1-12 月的天数，1表示大月30天，0表示小月29天。16位-5位分别表示1月-12月。
+ 17-18 位
    - 二进制表示农历正月初一对应的公历月份，不足两位左边补零到两位， 正月初一春节只会出现在公历的一月和二月，所以用两位二进制数就能表示完全
+ 19-23 位
    - 二进制表示农历正月初一对应的公历日子，不足五位补零到五位。注意：这里表示日子是用了5位二进制数，因为从16开始(二进制表示10000)，用二进制表示就需要用5位数了，而公历月份天数最大可以有 31 天。
+ 24 位
    - 第二十四位表示闰月的天数。1表示大月30天，0表示小月29天。仅在是闰年的情况下生效

这样就得到了一串 24 位的二进制串，然后再转为 16进制数即可。  
注意：从16进制数转为2进制数的时候如果不足24位，则需要在左边补零到24位，再根据上面的规则转为相应的数据。

**例子：农历 1901 年的数据转为 16 进制数**  
1901年不是闰年，所以 4-1 是 0000      
根据 1901 年的正常月份可知 16-5 位是 010010101110   
1901 年正月初一对应的公历月份是 2  所以 18-17 位是 10  
1901 年正月初一对应的公历日子是 19 所以 23-19 位是 10011  
1901年不是闰年，所以 第 24 位 我们填 0  
最后得到的二进制串是 010011100100101011100000    
转为十六进制后是 0x4e4ae0

**例子：农历 1906 年的数据转为 16 进制数**  
1906年是闰年，且闰4月，所以 4-1 是 0100      
根据 1906 年的正常月份可知 16-5 位是 011001010101   
1906 年正月初一对应的公历月份是 1  所以 18-17 位是 01  
1906 年正月初一对应的公历日子是 25 所以 23-19 位是 11001  
1906年是闰年，且闰月是大月，所以 第 24 位 我们填 1  
最后得到的二进制串是 111001010110010101010100    
转为十六进制后是 0xe56554

**附上根据十六进制字符串转为JSON格式数据的方法**
```javascript
/**
* 用 2000 年数据 16c960 来做 demo
* 传入年份和其对应的十六进制字符串，返回JS对象表示的数据
* 传入的十六进制字符串不包括 “0x” 前缀
*/
function toJSON(year, numStr) {
    if (!year || !numStr) {
        return '';
    }
    let hexadecimal = numStr.toString('16'); // 保证使用的数据是十六进制的字符串
    let binary = parseInt(hexadecimal, 16).toString(2);
    if (binary.length !== 24) { // 不足24位则左边补0补足24位
        binary = '0'.repeat(24 - binary.length) + binary;
    }
    let lunarItem = {
        'year': +year,
    };
    // binary 第 21-24 个字符判断是否是闰年，如果是则得到闰几月
    // binary 第 1 个字符是当年份是闰年的时候判断闰月的天数，1是大月30天， 0是小月29天，如果不是闰年则为0
    let runInfo = binary.slice(-4);
    if (runInfo === '0000') {
        lunarItem.isRun = false;
	    lunarItem.runMonth = 0;
	    lunarItem.runMonthDays = 0;
    } else {
        lunarItem.isRun = true;
        lunarItem.runMonth = parseInt(runInfo, 2);
        lunarItem.runMonthDays = +binary.slice(0, 1) + 29;
    }

    // binary 第 9-20 个字符是当年的正常月份天数，1是大月30天， 0是小月29天
    lunarItem.monthsDays = [];
    let monthInfo = binary.slice(8, 20);
    [...monthInfo].map(item => {
        lunarItem.monthsDays.push(+item + 29);
    })

    // binary 第 7-8 个字符是 农历年份正月初一对应的公历月份
    lunarItem.firstMonth = parseInt(binary.slice(6, 8), 2);

    // binary 2-6 个字符是 农历年份正月初一对应的公历日子
    lunarItem.firstDay = parseInt(binary.slice(1, 6), 2);

    return lunarItem;
}
console.log(toJSON(2000, '16c960'));
/*
    {
         "year": 2000,
         "isRun": false,
         "runMonth": 0,
         "runMonthDays": 0,
         "monthsDays": [30, 30, 29, 29, 30, 29, 29, 30, 29, 30, 30, 29],
         "firstMonth": 2,
         "firstDay": 5
    }
*/
```

**附上根据JSON格式数据转为十六进制字符串的方法**
```javascript
/**
 * 以下是把 lunarInfoFormat 数据转为 16进制字符串方法
 * 传入 lunarInfoFormat 数据，返回十六进制字符串组成的数组
 */
function toHexadecimalStr(data) {
    let HexadecimalStrArr = [];
    let yearArr = Object.keys(data);
    yearArr.sort(function (a, b) {
        return a-b;
    })
    yearArr.forEach(item => {
        let binaryStrArr = [];

        // 1-4
        let oneToFour = [];
        if (data[item].isRun) { // 如果是闰年
            let isRun2 = data[item].runMonth.toString(2);
            isRun2 = '0000' + isRun2;
            oneToFour = [...isRun2].slice(-4);
        } else { // 如果不是闰年
            oneToFour = ['0', '0', '0', '0'];
        }

        // 16-5
        let sixteenToFive = [];
        data[item].monthsDays.forEach((item, index) => {
            sixteenToFive.push((item - 29) + '');
        })

        // 18-17
        let eighteenToSeventeen = [];
        let firstMonth2 = data[item].firstMonth.toString(2);
        firstMonth2 = '00' + firstMonth2;
        eighteenToSeventeen = [...firstMonth2].slice(-2);

        // 19-23
        let nineteenToTwentyThree = [];
        let firstDay2 = data[item].firstDay.toString(2);
        firstDay2 = '00000' + firstDay2;
        nineteenToTwentyThree = [...firstDay2].slice(-5);

        // 24
        let twentyFour = ['0'];
        if (data[item].isRun && (data[item].runMonthDays === 30)) {
            twentyFour = ['1'];
        }

        binaryStrArr = [...twentyFour, ...nineteenToTwentyThree, ...eighteenToSeventeen, ...sixteenToFive, ...oneToFour];
        HexadecimalStrArr.push((parseInt(binaryStrArr.join(''), 2)).toString(16))
    })
    
    return HexadecimalStrArr;
}
```



