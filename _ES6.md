# _ES6

正式名称es2015,以后,包括统称es6

## babel转码,导入,配置

## let 和const

- 有作用域
- 不存在变量提升
- 暂时性死区 区块中存在`let`和`const`命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。例如如果typeof undefined,但是如果多了let 报Reference error
- 不允许重复声明