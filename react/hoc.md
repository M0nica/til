# Higher-Order Component (HOC)

A HOC is a component that **returns a new component**; this is a functional programming concept. 

There is no UI associated with HOC as the output is another component!

The most common signature for HOCs looks like this:

```
// React Redux's `connect`
const ConnectedComment = connect(commentSelector, commentActions)(CommentList);
```

What?! If you break it apart, it’s easier to see what’s going on.

```
// connect is a function that returns another function
const enhance = connect(commentListSelector, commentListActions);
// The returned function is a HOC, which returns a component that is connected
// to the Redux store
const ConnectedComment = enhance(CommentList);
```

Connect is a higher-order function that returns a higher-order component. 

```// Instead of doing this...
const EnhancedComponent = withRouter(connect(commentSelector)(WrappedComponent))

// ... you can use a function composition utility
// compose(f, g, h) is the same as (...args) => f(g(h(...args)))
const enhance = compose(
  // These are both single-argument HOCs
  withRouter,
  connect(commentSelector)
)
const EnhancedComponent = enhance(WrappedComponent)
```

### Things to keep in mind

- HOCs should **not** be used inside of render method! Bad things will happen if you try to render a component inside of a component's render function in order to avoid losing information if they render has to re-render.


Above examples are from React docs, read more here: https://reactjs.org/docs/higher-order-components.html
