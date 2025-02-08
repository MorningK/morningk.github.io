# React Hooks

## Rulers

1. Components and Hooks must be pure
 
    只有当渲染是纯粹时，React才能理解各个部分的渲染的优先级，并优先渲染最重要的部分，暂缓渲染不那么重要的部分，所以整个渲染逻辑可能会执行多次来提供最好的用户体检。
    > When render is kept pure, React can understand how to prioritize which updates are most important for the user to see first. This is made possible because of render purity: since components don’t have side effects in render, React can pause rendering components that aren’t as important to update, and only come back to them later when it’s needed. Concretely, this means that rendering logic can be run multiple times in a way that allows React to give your user a pleasant user experience.

    - Components must be idempotent – React components are assumed to always return the same output with respect to their inputs – props, state, and context.
    
        避免在渲染期间直接使用非幂等的方法，如果需要使用，应该在effect中调用。
        > This doesn’t mean you shouldn’t use non-idempotent functions like new Date() at all – you should just avoid using them during render. In this case, we can synchronize the latest date to this component using an Effect.
    
    - Side effects must run outside of render – Side effects should not run in render, as React can render components multiple times to create the best possible user experience.
    
    - Props and state are immutable – A component’s props and state are immutable snapshots with respect to a single render. Never mutate them directly.
    
    - Return values and arguments to Hooks are immutable – Once values are passed to a Hook, you should not modify them. Like props in JSX, values become immutable when passed to a Hook.
    
    - Values are immutable after being passed to JSX – Don’t mutate values after they’ve been used in JSX. Move the mutation before the JSX is created.

2. React calls Components and Hooks
    - Never call component functions directly – Components should only be used in JSX. Don’t call them as regular functions.
    - Never pass around hooks as regular values – Hooks should only be called inside of components. Never pass it around as a regular value.

1. Only call Hooks at the top level.
    - Do not call Hooks inside conditions or loops.
    - Do not call Hooks after a conditional return statement.
    - Do not call Hooks in event handlers.
    - Do not call Hooks in class components.
    - Do not call Hooks inside functions passed to useMemo, useReducer, or useEffect.
    - Do not call Hooks inside try/catch/finally blocks.
    
    > Hooks rely on a stable call order on every render of the same component. React holds an array of state pairs for every component. It also maintains the current pair index, which is set to 0 before rendering. Each time you call useState, React gives you the next state pair and increments the index. 

2. Only call Hooks from React functions 
    - Call Hooks from React function components.
    - Call Hooks from custom Hooks.

## useReducer

1. `reducer`需要是**纯函数**并且**只负责计算**下一个state，不应该处理其他的事务，包括提示消息等；其他事务应该在事件处理中完成。
    > The reducer should be a pure function — it should only calculate the next state. It should not “do” anything, including displaying messages to the user. That should happen in the event handler.

## useEffect

1. `effect`在**组件渲染完成后**才会执行。
    > Every time your component renders, React will update the screen and then run the code inside useEffect. In other words, useEffect “delays” a piece of code from running until that render is reflected on the screen.

2. 当提供依赖数组时，只有所有的依赖都相等（通过`Object.is`方法来判断）时，才会跳过这次执行。需要特别注意当依赖的类型是**数组**、**对象**和**函数**时的判断。
    > The dependency array can contain multiple dependencies. React will only skip re-running the Effect if all of the dependencies you specify have exactly the same values as they had during the previous render. React compares the dependency values using the [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is) comparison.

3. 在下一次effect执行前都会先完成本次的清理函数，并且每次effect执行时（包括清理函数）都会记住并使用当时的依赖。
    > React will call your cleanup function before the Effect runs next time, and during the unmount. [Each render has its own Effects](https://react.dev/learn/synchronizing-with-effects#each-render-has-its-own-effects)
