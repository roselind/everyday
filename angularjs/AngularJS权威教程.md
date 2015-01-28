# AngularJS权威教程

标签（空格分隔）： angularjs todo

---

## Angular动画

Angular团队创建了ngAnimate模块, 让我们的应用能够通过如下3中方式创建动画: 
- 使用CSS3动画
- 使用CSS3过渡
- 使用JavaScript动画

自1.2起, ngAnimate就不再是Angular核心的一部分, 安装方式: 
```js
bower install --save angular-animate 
angular.module("myApp", ['ngAnimate'])
```
### 动画运作方式? 

$animate服务默认给动画元素的每个动画事件添加两个CSS类, 支持多个angular内置的指令, 无需额外的配置即可支持动画. 
所有这些预先存在的支持动画的指令, 都是通过监听指令上的事件实现的. 例如, 
- 当一个新的ngView进入并且把新的内容带进浏览器时, 这个事件就叫做ngView的enter事件. 
- 当ngHide准备一个元素时, remove事件就会触发. 

下面是指令以及不同状态触发的事件列表: 
|   指令    |   事件    |
|:------------:|:-------------------:|
|ngRepeat| enter, leave, move|
|ngView|    enter , leave |
|ngInclude| enter, leave|
|ngSwitch| enter, leave|
|ngIf| enter, leave|
|ngClass or class=''|add, remove|
|ngShow| add, remove(.ng-class)|
|ngHide| add, remove|

$animate服务基于指令发出的事件来添加特定的样式类.
- 对于结构性(比如进入, 移动和离开), 添加上去的CSS类是ng-[EVENT]和ng-[EVENT]-active这样的形式. 
- 对于基于样式类的动画(比如ngClass), 动画样式类的形式是: [CLASS]-add, [CLASS]-add-active, [CLASS]-remove, [CLASS]-remove-active. 
- 对于ngShow和ngHide, 只有.ng-hide类会被添加和移动, 它的形式跟ngClass一样: ng-hide-add, ng-hide-active, ng-hide-active, ng-hide-remove, ng-hide-remove-active. 

### 自动添加类

触发enter事件的指令会在DOM变更时收到一个.ng-enter样式类, 然后, angular添加ng-enter-active类, 它会触发动画. ngAnimate自动检测CSS代码来判定动画什么时候完成. 

这个事件完成后, Angular会从DOM中移除ng-enter和ng-enter-active两个类, 使我们能够在DOM元素上定义动画相关的属性. 

如果浏览器不支持CSS过渡或者动画, 动画会开始, 然后立即结束, DOM会处于最终状态, 不会添加过渡或者动画的样式类. 

所有支持的结构性动画事件都遵循着同样的约定: 进入, 离开, 移动. 基于样式的动画事件略有不同. 

### 使用CSS过渡动画










