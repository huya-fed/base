# Base test3

test4
---

Base 是一个基础类，提供 Class、Events、Attribute 、 Aspect 和 Hub 支持。

https://github.com/aralejs/aralejs.org/issues/314

https://github.com/aralejs/widget/wiki/Base-&-Widget-%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B

---

## 使用说明

### extend `Base.extend(properties)`

基于 Base 创建子类。例子：

```js
/* pig.js */
var Base = require('base');

var Pig = Base.extend({
    attrs: {
        name: ''
    },
    talk: function() {
        alert('我是' + this.get('name'));
    }
});

module.exports = Pig;
```

继承 Base 可覆盖 initialize 构造函数， **但需要调用父类构造函数**，如 arale 的 widget 定义了组件的生命周期

```js
/* widget.js */
var Base = require('base');

var Widget = Base.extend({
    initialize: function(config) {
        Widget.superclass.initialize.call(this, config);
        this.parseElement()
        this.initProps()
        this.delegateEvents()
        this.setup()
    },
    ...
});

module.exports = Widget;
```

Base 继承和混入了一下功能，可查看文档 ：

- [Class 使用文档](https://github.com/huya-fed/class.git)
- [Events 使用文档](https://github.com/huya-fed/events.git)
- [Attribute 使用文档](https://github.com/huya-fed/attribute.git)
- [Aspect 使用文档](https://github.com/huya-fed/aspect.git)


### Base 与 Class 的关系

Base 是使用 `Class` 创建的一个基础类，默认混入了 `Events`、`Attribute`、`Aspect` 模块：

```js
/* base.js */
var Class = require('class');
var Events = require('events');
var Aspect = require('./aspect');
var Attribute = require('./attribute');

var Base = Class.create({
    Implements: [Events, Aspect, Attribute],

    initialize: function(config) {
        ...
    },

    ...
});

...
```
