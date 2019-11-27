# ESLint

## 第一章 如何提高代码质量

前端开发的同学都知道，Javascript是一门超灵活的语言，但灵活的背后是各种陷阱。

```js
var base = 1;
boss = 2;

console.log(bass); // 1
```

Javascript 语言的各种升级和扩展原生JS,ES6,Typescript等等代码版本也是五花八门。

那么问题来了：

* 前端项目如何用提高代码质量，以减少一些不比要的错误？
* 如何保存团队编码风格一致？
* 如何自动按照指定的风格格式化代码？

> 虽然Javascript没有官方推荐的代码规范，不过社区有些比较热门的代码规范，比如[standardjs](https://standardjs.com/readme-zhcn.html)、[airbnb](https://github.com/airbnb/javascript) [中文](https://github.com/lin-123/javascript)。使用ESLint配合这些规范，能够检测出代码中的潜在问题，提高代码质量。

### ESlint 介绍

eslint 的官方中文网站：https://cn.eslint.org

### 安装

------

首先我们需要安装 eslint.

全局安装

```bash
npm install -g eslint
```

局部安装

```bash
npm install eslint --save-dev
```



## 第二章 代码规范性检测

### 基础使用

写一个测试js文件 classes.js

```javascript
class User {
    constructor(name) {
        this.name= name
    }
  
  
    get name() {
        return this._name
    }
    set   name(value)   {
        if (value.length<5)  {

            console.log('too short')
           }else{
            this._name = value
        }
     }
     sayHi() {
        console.log('my name is : ', this.names)  
    }
}
 
class   SportMan extends User {
    constructor(name,speed) {
          super(name)
         this.speed = speed
    }

    sayHi(){
        super.sayHi()
        console.log('speed is : ', this.speed)
    }
}

let user = new User('John')
user.sayHi()

let lk = new SportMan('李康',200)
lk.sayHi()
xxx
```

运行 eslint

```bash
eslint classes.js
```

错误提示分别是：

```bash
  32:3  error  Unexpected console statement  no-console
  41:1  error  'xxx' is not defined          no-undef

✖ 5 problems (5 errors, 0 warnings)
```

### 自动修复

[命令行](https://cn.eslint.org/docs/user-guide/command-line-interface#fixing-problems)中的 `--fix` 选项可以自动修复一些该规则报告的问题。这些规则在 [规则页面](https://cn.eslint.org/docs/rules) 被标记为 “扳手”。



## 第三章 配置

可以使用2种方式来配置 ESLint，ESLint 会查找和自动读取它们。

- JavaScript 注释

```js
/* eslint-disable */
```

- 配置文件
  - `.eslintrc.*` 文件
  - 或者直接在 `package.json` 文件里的 `eslintConfig` 字段指定配置

### 配置文件

为了正确使用eslint，需要配置代码规范设置。

```bash
eslint --init
```

选择你想要的模式,生成配置文件 `.eslintrc.js` 内容如下：

```javascript
module.exports = {
    "env": {
        browser: true,
        es6: true
    },
    "extends": "eslint:recommended",
  	"rules": {
        "no-console": "off",
        "semi": ["error", "never"]
  	}
};
```

ESLint 支持几种格式的配置文件：

- **JavaScript** - 使用 `.eslintrc.js` 然后输出一个配置对象。
- **YAML** - 使用 `.eslintrc.yaml` 或 `.eslintrc.yml` 去定义配置的结构。
- **JSON** - 使用 `.eslintrc.json` 去定义配置的结构，ESLint 的 JSON 文件允许 JavaScript 风格的注释。
- **(弃用)** - 使用 `.eslintrc`，可以使 JSON 也可以是 YAML。
- **package.json** - 在 `package.json` 里创建一个 `eslintConfig`属性，在那里定义你的配置。

### 推荐配置

在配置文件 ``.eslintrc.js` 的 `rules` 中可以定义规则。

所有的规则默认都是禁用的， `.eslintrc` 配置文件使用下面的一行代码来启用推荐的规则，这些规则在 [规则页面](https://cn.eslint.org/docs/rules) 被标记为 “✔”。

```json
"extends": "eslint:recommended"
```

另外，你可以在 [npmjs.com](https://www.npmjs.com/search?q=eslint-config) 搜索 “eslint-config” 使用别人创建好的配置。

### 常用配置项

ESLint 被设计为完全可配置的，详细配置可参考[[官方文档](https://cn.eslint.org/docs/rules/)](https://cn.eslint.org/docs/rules/)

* 预防错误的规则

  | 规则                                       | 说明                            |
  | ---------------------------------------- | ----------------------------- |
  | [for-direction](https://cn.eslint.org/docs/rules/for-direction) | 强制 “for” 循环中更新子句的计数器朝着正确的方向移动 |
  | [no-cond-assign](https://cn.eslint.org/docs/rules/no-cond-assign) | 禁止条件表达式中出现赋值操作符               |
  | [no-duplicate-case](https://cn.eslint.org/docs/rules/no-duplicate-case) | 禁止出现重复的 case 标签               |
  | [no-func-assign](https://cn.eslint.org/docs/rules/no-func-assign) | 禁止对 `function` 声明重新赋值         |
  | [no-dupe-args](https://cn.eslint.org/docs/rules/no-dupe-args) | 禁止 `function` 定义中出现重名参数       |

* 最佳实践

* 代码风格一致性规则

| 规则                                       | 说明              |
| ---------------------------------------- | --------------- |
| [ no-mixed-spaces-and-tabs](https://cn.eslint.org/docs/rules/no-mixed-spaces-and-tabs) | 禁止空格和 tab 的混合缩进 |

* 特定代码规则
  * ECMAScript 6
  * Node.js and CommonJS
  * Variables

```json
{
    "rules": {
        "semi": ["error", "always"],
        "quotes": ["error", "double"]
    }
}
```

#### semi

强制使用一致的分号作为代码行结束。

字符串选项：

- `"always"` (默认) 要求在语句末尾使用分号
- `"never"` 禁止在语句末尾使用分号 (除了消除以 `[`、`(`、`/`、`+` 或 `-` 开始的语句的歧义)

```js
/*eslint semi: ["error", "always"]*/
```

#### quotes

强制使用一致的反勾号、双引号或单引号。

字符串选项：

- `"double"` (默认) 要求尽可能地使用双引号
- `"single"` 要求尽可能地使用单引号
- `"backtick"` 要求尽可能地使用反勾号

```js
/*eslint quotes: ["error", "single"]*/
```

#### no-console

禁止调用console打印信息。

案例：禁用 console，在项目中使用统一日志。



### 配置方法

rules 中可以定义规则。

规则中的第一个值是错误级别，可以使下面的值之一：

- `"off"` - 关闭规则
- `"warn"`  - 将规则视为一个警告（不会影响退出码）
- `"error"` - 将规则视为一个错误 (退出码为1)

这三个错误级别可以允许你细粒度的控制 ESLint 是如何应用规则



## 第四章 配合IDE





### VSCode