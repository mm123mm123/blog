# JavaScript 的历史

## JavaScript 是由一个叫布莱登的人花十天时间设计了最初的版本，当时网景公司要求给浏览器添加一个脚本功能，之后 JS 推出后大获成功，微软在不久后就为 IE3 浏览器推出了 JScript,与网景的 JavaScript 竞争。

## 当时浏览器端存在着多种脚本语言，这也意味着语言标准化的缺失，之后网景向 ECMA 提交语言标准，ECMA 就以 JavaScript 语言为基础指定了 ECMAScript 标准

## 之后随着 IE 浏览器在 IE6 取得巨大成功之后开始走下坡路，IE7，8 一直问题不断，谷歌在此期间抓住机会，发布了 Chrome 浏览器，最终 Chrome 浏览器在 2016 年取得百分之六十二的份额。另外一方面，智能手机开始崛起，IE 在手机上也基本消失。这两方面的原因，让 IE 最终走向消亡，也让 JavaScript 成为了浏览器脚本语言的霸主。

# JavaScript 的 10 个设计缺陷

- ## 不适合开发大程序
- ## 非常小的标准库
- ## null 在编程实践中几乎没用，还容易和 undefined 混淆，根本不应该设计。
- ## 任何一个函数内部都可生成全局变量，大大加剧了程序的复杂性。
- ## 所有语句都必须以分号结尾，如果忘记加，解释器不报错，会自动加上，这会导致一些难以发现的错误。
- ## 加号运算符，既可以表示数字与数字的和，又可以表示字符与字符的连接，如果是数字和字符相加，数字自动转化为字符，不必要的加剧了运算的复杂性。
- ## NaN 是一种数字表示超出了解释器的极限，与其如此设计，不如解释器直接报错，有利于简化程序
- ## 数组也属于对象，所以要区分一个对象到底是不是数组，比较麻烦
- ## ==用来判断两个值是否相等时候，当两个值类型不同时候，会发生自动准换，得到的结果不符合直觉。
- ## 基本数据类型，又相应的函数，可以生成对象，而着三类对象作用很小，还造成混淆
