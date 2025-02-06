# React Hooks

## useReducer
1. `reducer`需要是**纯函数**并且**只负责计算**下一个state，不应该处理其他的事务，包括提示消息等；其他事务应该在事件处理中完成。
> The reducer should be a pure function — it should only calculate the next state. It should not “do” anything, including displaying messages to the user. That should happen in the event handler.

## useEffect
1. `effect`在**组件渲染完成后**才会执行。
> Every time your component renders, React will update the screen and then run the code inside useEffect. In other words, useEffect “delays” a piece of code from running until that render is reflected on the screen.
2. 当提供依赖数组时，只有所有的依赖都相等（通过`Object.is`方法来判断）时，才会跳过这次执行。需要特别注意当依赖的类型是**数组**、**对象**和**函数**时的判断。
> The dependency array can contain multiple dependencies. React will only skip re-running the Effect if all of the dependencies you specify have exactly the same values as they had during the previous render. React compares the dependency values using the [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is) comparison.
3. 在下一次effect执行前都会先完成本次的清理函数，并且每次effect执行时（包括清理函数）都会记住并使用当时的依赖。
> React will call your cleanup function before the Effect runs next time, and during the unmount.
[Each render has its own Effects](https://react.dev/learn/synchronizing-with-effects#each-render-has-its-own-effects)
