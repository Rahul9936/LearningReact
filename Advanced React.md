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
```