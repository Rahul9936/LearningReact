## Advanced React

### Things to discuss
    - Virtual DOM
    - Data Binding
    - React Lifecycle

### What is DOM 😱
DOM (Document Object Model) is an standerdized way of representing the HTML in a form of tree structure

### IS DOM Slow :question:
Fetching node using document.getElementByID is very fast process then what is it that makes DOM manipulation really slow?
Writting to DOM makes it really slow, when we update any part of DOM then browser needs to recalculate the CSS, do layout, repaint the whole page ant it consumes a lot of time.

### Web browser workflow
Parsing HTML -> Render Tree Construction -> Layout of the rendered tree -> Painting the rendered tree

### Virtual DOM
Its a blueprint of DOM, tree data structure of plain javascript, detached from the browser-specific implemeation details. It exists in memory never actually gets rendered on web page.
React does not directly modifies the DOM structure, first it updates the Virtual DOM and take the diff and update only that part instead of re-rendering the DOM structure which save a lot of time. Check the below image to get the clarity on how the React's Virtual DOM diff works
<b>Note:</b> Concept of Virtual DOM is not developed by react, it has existed before react just uses this concept (Angular and Vue)

Check the below image of how react maintains the Virtual DOM and patches applied to the Reacl DOM which is only the difference of virtual DOM and real DOM.
It does not update the entire real DOM structure as you can see in the below image
<img src="https://i.stack.imgur.com/S1vng.png"/>


### Data Binding in React
TO DO: Update this content later

### Immutability in react
If an object is immutable and we try to update that object then instead of updating this object, it will create a new object, and taht makes it easier to track the made in any object. This concept for update in Component State and Props makes it useful in re rendering of component.

### React Lifecycle
A lifecycle of react component is from initializing the component to mount over the DOM and updating the component if any changes made to props or state and unmouting the component from DOM.
React provides lifecycle methods which are also called lifecycle hooks which can be used to override at particular time. Method names starting with "will" will occur before and names starting with "did" will occur after.
For example componentWillMount will execute before the component is mounted to the DOM and and componentDidMount will execute once the component has been mounted over the DOM.

Below image depicts the execution order of the methods in different lifecycle phases

<img src="https://cdn-images-1.medium.com/max/2000/1*sn-ftowp0_VVRbeUAFECMA.png" />

#### Initialization
Component constructor method is executed first, here we can initialize the component state, for example
```javascript
class MyComponent extends React.Component {
    constructor() {
        super();
        this.state = {
            name: "XYZ"
        }
    }
    render() {
        return (
            <div>
                <span>{this.state.name}</span>
            </div>
        )
    }
}
```

#### componentWillmount()
This method will be called just before the component is going to be mounted over the DOM, here we can update the component state which will be rendered on web page
Note: we can not set the component state outside of constructor directly, we need to call this.setState method to set the state for ex.
```javascript
class MyComponent extends React.Component {
    constructor() {
        super();
        this.state = {
            name: "XYZ"
        }
    }
    
    componentWillMount() {
        this.setState({
            name: "ABC"
        });
    }
    
    render() {
        return (
            <div>
                <span>{this.state.name}</span>
            </div>
        )
    }
}
```

#### render()
 Mounts the component and this is a "pure method" (deterministic) means it will always return the same output if inputs given are same
 <strong>Note:</strong> do not set component state in this method because component rendering may go to infinite loop
 
#### componentDidMount()
This method will be called once the component is mouted over the DOM, this method is called only once during the initial rendering of component. Here DOM is available so jQuery and other similar operation which requires DOM manipulation can be done
<strong>Note:</strong> do not set component state in this method because component rendering may go to infinite loop

### Re-rendering lifecycle hooks
Component re-render can happen in two cases either the state of the component is updated or the props
Lets discuss about lifecycle hooks when the state changes:
#### shouldComponentUpdate()
We can write the logic if the component should be re rendered or not, it returns true/false based on logic to update the component. By default this method return true. This method will have nextProps and nextState parameter which we can compare with the curent state and props and return true /false accordingly to update the component or not. For example
```javascript
class MyComponent extends React.Component {
    constructor() {
        super();
        this.state = {
            name: "XYZ"
        }
    }
    
    shouldComponentUpdate(nextProps, nextStates) {
        if(nextStates.name && this.state.name !== nextStates.name)
            return true
        return false;
    }
    
    render() {
        return (
            <div>
                <span>{this.state.name}</span>
            </div>
        )
    }
}
```
#### componentWillUpdate()
This method is executed only after the shouldComponentUpdate() method return true and similar to componentWillMount(), here we can update the component state

#### componentDidUpdate()
This method is executed once the re-rendering of the component is completed. This method is used to re trigger the third party libraries used to make sure these libraries also update and reload themselves.

### When component props changes following lifecycle hooks will be called
#### componentWillReceiveProps()
This method is executed when the child component props are dependent upon the parent and changes during the re render of the parent component causes the udpdate of the child component
For ex.
```javascript
class MyComponent extends React.Component {
    componentWillReceiveProps(nextProps) {
        if(nextProps.name && this.props.name !== nextProps.name)
            return true
        return false;
    }
    
    render() {
        return (
            <div>
                <span>{this.props.name}</span>
            </div>
        )
    }
}
```

### Flux and Redux
Here we will mostly discuss about the Redux functionality because 
1) Redux can be integrated React, Angular or any other framework
2) Servicenow seismic framework extensively utilizes the Redux
 

## Redux
As we know, component state can be used to change the UI dynamically on performing some actions, this state handling can be done in the component itself but it becomes hard to maintain the states for a larger size project, this is where Redux comes to picture to rescue from this kind of situations

#### when to use redux
As we have learnt that we can dynamically update the UI in react using component state, by calling this.setState of a component will automatically the component and it child components as well.

Now a days applications are becoming more dynamic in nature especially in Single Page Application, and if the number of pages more than 2-3 then managing the component by changing the state becomes very complex. It becomes hard to tell which module has changed the state and unwanted data changes may be there. It also helps in restructuring the application.

for e.g. Incidents list can be one component and Incident form can be another component so to provide the interaction between either we move both the components under the same parent element and pass states as props or use Redux which maintains the application state not the component state.

Facebook developers came up with the solution called <strong>Flux</strong>.
Its a one directional data flow architecture to manage the application state. Check the below how state management is done using flux

<img src="https://i.stack.imgur.com/bK7nC.png"/>
<br></br>

Redux is also similar to the Flux, data flow in unidirectional but it uses a single store, check the below image to understand the state management in React using Redux

<img src="https://cdn-images-1.medium.com/max/1600/0*95tBOgxEPQAVq9YO.png" />

Integrating redux with the react has two parts, first one is how to configure redux(Action, reducer, store) and second one is connecting redux with the react (binding store with the components props and actions). 
We will start with the first part, it includes the following concepts:
- Actions
- Reducer
- Store

### Action
Actions are simply the Javascript object that send data to the store
- Actions must have the type attributes
- Any number of attributes can be specified for an Action
- As a best practive action names should be defined as a constant because typing the actions names are more prone to errors 
```javascript
{
    type: "ITEM_SELECTED",
    sys_id: "3434355vfgf43343dvvf434",
    incident_number: "INC100023"
}
```

#### Action Creator
Its best practice to wrap every action within a method called Action creators, e.g.
```javascript
function addToDo() {
    return {
        type: "ITEM_SELECTED",
        sys_id: "3434355vfgf43343dvvf434",
        incident_number: "INC100023"
    }
}
```
### TODO: read about async action creator

### Reducers
When the user performs any operation on the UI, action gets created now its reducers job to determine the next state of the application.
Reducers are Pure methods, it takes current state and action name as argument and return the next state of the application.
Following things should not be done in reducers:
- Change the current state or action object directly, always create a copy of state and then perform any operation on it
- Do not call non-pure functions like Date.now()

```javascript
(state = initialState, action) => {
    switch(action.type){
        // update state based on action type
    }
    return nextStep;
}
```

#### Methods to use in reducers to avoid mutability of state and action object
Arrays: concat, slice and use spread operator
Objects: Object.assign and spread operator

### Store
Store acts as glue in Redux, store holds the whole state tree of the application keeps an updated version of the states. Store can be updated by dispatching an action.
Following is an example of dispatching the action and updating it

```javascript
import { createStore } from 'redux';

function addItemReducer(state, action) {
    switch(action.type){
        case 'ADD_ITEM':
            return {...state, payload: action.payload};
        default:
            return state;
    }
}

var store = new createStore(addItemReducer);

store.dispatch({
    type: "ADD_ITEM",
    payload: "Any Random Text"
});
```

#### Provider

Now coming to the second part, where we discuss how to link redux with the react. react-redux provide a component called 'Provider' which provides the store object to all of child components so ideally Provider should be the root component of our App as only chilren under provider have the access of Store object, below example is given for the todo app

```javascript
class MyApp extends Component {
    render() {
        return (
            <Provider store = {store}>
                <input type="text" name="inputbox" />
                <input type="submit" name="submitToDo"/>
                <TodoList />
            </Provider>
        )
    }
}
```

### Connect
After adding the Provider component we have access to store is available but but there is no direct link between the store and component that is when the component changes how the component is going to update.
Connect provide the mechanism to map the store's state and dispatch with the component props, in other words React view is connected to Redux state through the connect function provided by react-redux library

connect requires mapStateToProps and mapDispatchToProps and binds state and Actions to the component props

```javascript
const mapStateToProps = (state) => {
    return {
        prop1: state.items
    }
}

const mapDispatchToProps = (dispatch) => {
    return {
        onClickHandler: (payload) => {dispatch(addItem(payload))}
    }
}

connect(mapStateToProps, mapDispatchToProps)(MyApp);
```
#### Note: As you check in the above example, both the methods returns object which will mapped with component props


## Let's connect the dots ...
If you have understood the data flow in redux, means how the action dispatches which cause the store to update the state and this state will be re-rendered with latest changes

I will be creating a Simple Todo app which has input box and submit button and below that we will have the list of todos and when we submit the input list will be updated automatically

Let's begin
```javascript
// Actions.js - This file will have all the action constants
export const ADD_ITEM = "ADD_ITEM";

// ActionCreator.js - This file will have all the actions which returns an action Object comprising of type and and <payloads> attributes
import {ADD_ITEM} from './Actions';

export function addItem(data) {
    return {
        type: ADD_ITEM,
        payload: data
    };
}

// Reducers.js - This file will help in producing the next state, and also makes redux predictable
import {ADD_ITEM} from './Actions'; 

export function addItemReducer (state = [], action) {
    console.log(action);
    switch(action.type) {
        case ADD_ITEM:
            return [...state, action.payload];
        break;
        default:
            state;
    }
}

// ListComponent.js - After submitting the input field, list will be re rendered based on the props (articles) passed to this component
import React from 'react';
import ReactDOM from 'react-dom';

export default class ListComponent extends React.Component {
    render() {
        return (
            <div>
                {
                    this.props.articles.map((value, index) => {
                        return <div key={index}>{value}</div>
                    })
                }
            </div>
        )
    }
}

// MyApp.js - This one is main Component, here we write logic to map the store state with component props
import React from 'react';
import { addItem } from './ActionCreator';
import { connect } from 'react-redux';
import ListComponent from './ListComponent';
import { bindActionCreators } from 'redux';

class MyApp extends React.Component {
	constructor(props) {
		super(props);
		this.handleSubmitClick = this.handleSubmitClick.bind(this);
	}

	handleSubmitClick(event) {
		this.props.handleTheSubmitClick(document.getElementsByName("title")[0].value);
	}

	render() {
		console.log(this.props);
		return (
            <div>
                <input type="text" name="title"/>
                <button onClick={this.handleSubmitClick}>Submit</button>
                <ListComponent articles={this.props.articles || []}/>
            </div>
		)
	}
}

const mapStateToProps = (state) => {
	console.log(state);
	return {
		articles: state
	}
};

const mapDispatchToProps = (dispatch) => {
	return {
		handleTheSubmitClick : (data) => { dispatch(addItem(data)) }
	};
}

export default connect(mapStateToProps, mapDispatchToProps)(MyApp);

// index.js - Entry file for the react-redux app, we will wrap the parent compoent of the app within Provider which provides store object to all the child components
import ReactDOM from 'react-dom';
import React from 'react';
import { addItemReducer } from './Reducers';
import { addItem } from './ActionCreator';
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import MyApp from './MyApp';

let store = new createStore(addItemReducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());

class MainComponent extends React.Component {

	render() {
		return (
			<Provider store = {store}>
				<MyApp />
			</Provider>
		)
	}
}

var el = document.getElementById("app");
ReactDOM.render(<MainComponent />, el);
```


# ========== Happy Coding ===================
