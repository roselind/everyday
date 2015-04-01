# reactjs总结

标签（空格分隔）： reactjs todo

---
## 核心API说明

###  React.createClass

1. render: 
2. this.getInitialState: 
2. this.setState({})
3. this.state 
4. this.refs.refName.getDOMNode()
5. this.props 
6. this.props.children:  get component all children 
6. mixins: [SomeMixins]
7. this.forceUpdate() 
8. shouldComponentUpdate: function(){ return false }

### this.state 

alswery use for form element. like input,radio, checkbox, textarea, select .. option

- setState({}) 
- props 
- React.createElement 
- component lifecycle 
> 1. Mounting
> 2. Updating
> 3. Unmounting

###  brower dom
> 
1. ref: `<input ref="username"/>`
2. this.refs.username.getDOMNode().focus() 

### spread operation ...
### mixins: just like ruby mixin.  
### addons 

1. two-way bindings: ReactLink
2. animation: ReactTransition, ReactCSSTransition


### React Perf

## 原理 

Virtual DOM 

在内存中构建一个Virtual DOM, 每次更新内容, 都从新生成Virtual Dom与旧的virtual dom比较, 找出不同点, 通过diff, batch update to brower dom. 达到高性能

## 核心API文档
### Updating: shouldComponentUpdate

```jsx
boolean shouldComponentUpdate(object nextProps, object nextState)
```

Invoked before rendering when new props or state are being received. This method is not called for the initial render or when forceUpdate is used.

Use this as an opportunity to return false when you're certain that the transition to the new props and state will not require a component update.
```javascript
shouldComponentUpdate: function(nextProps, nextState) {
  return nextProps.id !== this.props.id;
}
```
If shouldComponentUpdate returns false, then render() will be completely skipped until the next state change. (In addition, componentWillUpdate and componentDidUpdate will not be called.)

By default, shouldComponentUpdate always returns true to prevent subtle bugs when state is mutated in place, but if you are careful to always treat state as immutable and to read only from props and state in render() then you can override shouldComponentUpdate with an implementation that compares the old props and state to their replacements.

If performance is a bottleneck, especially with dozens or hundreds of components, use shouldComponentUpdate to speed up your app.

## TOP LEVEL API 
[React API](http://facebook.github.io/react/docs/top-level-api.html)

- React.createClass
- React.createElement
- React.createFactory
- React.render
- React.unmountComponentAtNode
- React.renderToString
- React.renderToStaticMarkup
- React.isValidElement
- React.DOM: React.DOM.div
- React.PropTypes
- React.initializeTouchEvents
- React.Children: this.props.children
> 
1. React.Children.map
2. React.Children.forEach
3. React.Children.count
4. React.Children.only

## ReactComponent API 

- setState
- replaceState
- forceUpdate
- getDOMNode
- isMounted
- setProps
- replaceProps

## Component Specs and Lifecycle

### Component Specs Methods 

- getInitialState
- getDefaultProps
- propTypes
- mixins
- statics
- displayName

### Lifecycle Methods

- Mounting: componentWillMount
- Mounting: componentDidMount
- Updating: componentWillReceiveProps
- Updating: shouldComponentUpdate
- Updating: componentWillUpdate
- Updating: componentDidUpdate
- Unmounting: componentWillUnmount

##  Functional Reactive Programming:FRP  


