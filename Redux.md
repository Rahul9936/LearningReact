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

Lets combine all of the above concepts into one to configure the redux for the application, I will be creating multiple files to make it clear

<b>Constants.js</b>
```javascript
export const ADD_ITEM = "add_item";  
```

<b>Actions.js</b>
```javascript>
import {ADD_ITEM} from "./Actions.js";

export addItem function (item) {
  return {
    type: ADD_ITEM,
    payload: item
  }
}
```

<b>Reducer.js</b>
```javascript
import {ADD_ITEM} from "./Actions.js";

var initialState = [];

export default reducers = function (state = initialState, action) {
  switch(action.type) {
    case ADD_ITEM:
      return state.concat(action.payload);
    // Similarly add case for other reducers, In this application we have only one action add item from input box to the list
  }
}
```

<Store.js>
```javascript
import reducer from "./Reducer.js";
import { createStore } from "redux";

var store = createStore(reducer);
export default store;
```

Till now we have configured the Redux for our application, but to access the store in our application component we will use "react-redux" library to glue them together

#### react-redux
It lets the React components to connect with the Redux. react-redux provides "Provider" component which lets the application access the redux store. Provider component should be used at the highest level of the application so that store object is available to all the child components. For ex.
Before binding with Provider application looks like this - 
```html
<App> // Root component of the application
  <Define all the child components here>
</App>
```

After binding with the provider -
```html
<Provider store={store}>
  <App> // Root component of the application
    <Define all the child components here>
  </App>
</Provider>
```
- Provide takes store as props, all the components present under the Provider will have the access to this store object

Lets create a component and add the Provider there to see it in action
```javascript
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "react-redux";
import { addItem } from "./actions.js";
import store from "./store.js";

class App extends React.Component {
  // Add event handler here which dispatch action to store on clicking the enter key on input box, and it will update the state in the reducer function
  // Here it may be confusing that how the reducer function is being called by executing store.dispatch, to answe this check Store.js there while creating the store we are passing the reducer function -> (Line no 90)
  handleChange(event) {
    if (event.key === "Enter") {
      store.dispatch(addItem(event.target.value));
      console.log(store);
    }
  }
    
  render() {
    return (
      <Provider store={store}>
        <input name="todobox" type="text" onKeyDown={this.handleChange.bind(this)} />
        <ListComponent /> // Don't bother about it now, explained in next example
      </Provider>
    );
  }
}
```

In the above example how to dispatch an event from a React component and update the state.
Now in next example we will fetch the state from store and update the view of the component. 

To connect the redux store with the component props, we have to use <b>connect</b> api provided by react-redux
#### connect
connect api maps the store state to the component props, check in the below example we have used mapStateToProps function which maps state to props (items).
syntax - <b>connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])</b>

Here I have created one more component ListComponent, so when we type anything in the input box and hit enter, that text item will be updated in the list of ListComponent.

So lets hit it ...

<b>ListComponent.js</b>
```javascript
import React from "react";
import { connect } from "react-redux";

class ListComponent extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(function(name, index) {
          return <li key={index}>{name}</li>;
        })}
      </ul>
    );
  }
}

function mapPropsToState(state) {
  console.log(state);
  return {
    items: state
  };
}
// export default ListComponent; - By doing this we are exporting the dumb component here which does not have any idea about the store data
// Make the component aware of the store data
export default connect(mapPropsToState)(ListComponent);
```

TODO: Explain about the Presentational component and Container Component

Note: Find my live working wxample of ToDo App here <a href="https://codesandbox.io/embed/kx29v5myp3">Link</a>
