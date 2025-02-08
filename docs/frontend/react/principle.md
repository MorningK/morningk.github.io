# Principle

## Render

### Steps

1. Trigger a render
    1. It’s the component’s initial render.
    2. The component’s (or one of its ancestors’) state has been updated.

2. React renders your components
    - On initial render, React will call the root component.
    - For subsequent renders, React will call the function component whose state update triggered the render.

    父组件的重新渲染会引起子组件的重新渲染，但可以使用`memo`函数来优化这一情况。
    > This process is recursive: if the updated component returns some other component, React will render that component next, and if that component also returns something, it will render that component next, and so on. The process will continue until there are no more nested components and React knows exactly what should be displayed on screen.

3. React commits changes to the DOM 
    - For the initial render, React will use the appendChild() DOM API to put all the DOM nodes it has created on screen.
    - For re-renders, React will apply the minimal necessary operations (calculated while rendering!) to make the DOM match the latest rendering output.

    React only changes the DOM nodes if there’s a difference between renders.

4. Browser paint

    After rendering is done and React updated the DOM, the browser will repaint the screen. 
