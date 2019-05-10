### Redux Tutorial

<b>Definition:</b> Redux is state container for the Application. 
##### Why we should use redux
All the components in react are stateful but when the application size increases it becomes very tedious task to maintain the state or in the case where apllication is highly nested then we will have to pass down the props to each child component and in some cases number of props also may increase.

To avoid the above scenarios, redux handles the application state seperately globally which will be accessible to entire application <i>based on binding</i>.


Lets understand few terminology before jumping to the Date flow in redux

<pre>Note: Entire tutorial I will be using the example of ToDo app in react/redux. At the end will combined all the concepts into a single example</pre>


#### Actions
Actions are basically javascript object which has two properties type and payload, for ex adding a new todo Item, action would be something like this:

```javascript
var action = {
  type: ADD_ITEM,
  payload: <fetch the text from input box>
};

// Whenever users perform any action on the view, we dispatch the action to the store.
// Remember It
store.dispatch(action);
```

<b>Good Practice: </b> Always define action names as a constant to avoid typo

#### Reducers
Reducers basically are the functions decide the next state of the application, it takes current state and action name as a argument returns the new state of the application.
For ex.
```javascript
var initialState = [];
function reducer (state = initialState, action) {
  if (action.type == ADD_ITEM)
    return state.concat(action.payload);
}
```
<b>Note: </b> Reducers are pure function
<b>Pure function: </b> For a given input it will always return the same output and it should not modify the given inputs

Use Object.assign() for objects and Array.prototype.concat for array to make the reducer function a pure function


#### Store
Store in the javscript object which holds the state of the entire application
<b>Note: </b> An application have only store but multiple reducers
Lets combine all of the above concepts into one to configure the redux for the application, I will be creating multiple files to make it clearConstants.js
```javascript
  
```
