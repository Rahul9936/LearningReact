## About React
React is an open source Javascript library from facebook for building User Interfaces (UIs). React powers the UI of Instagrams web client and Facebook's Ad management products. There are multiple benefits , ranging from nice templates with JSX, to a fist, virtual DOM.

Often people talk about how react is different than other frameworks like AnuglarJS, so next we will emphasize more on Good and Bad parts of React JS

### Advantages of using the React
- Component based architecture: In React an UI page can be broken into multiple pieces which are called components. For ex our Incident form can be categorised into multiple components Header, Form, Buttons, etc. These components are completely reusable. We will discuss more about the components.
- Fast DOM manipulation: As we know direct DOM manipulation is very costly (Time wise) but react utilizes the concept of Virtual DOM.

##### Note: React is mainly the view layer, one cannot build a fully functional dynamic application with React alone

React gives you a template language and some function hooks to essentially render HTML. That's all React outputs, HTML.

## What is component
As you know React is based upon component design. Everything in React is a component which makes it easy to reuse components frequently. In react, a web page is divided into small individual section which are component, for example check the below image of Incident form, it has following component
- Header
    - UI Action
- Form
    - Form Fields
- Tabs
- Activity Formatter

Its our choice to divide the page into different components but its advised to have smaller component to make it reusable and maintaining also becomes easier.
A component can have multiple child components for example Header has child component like Ui Actions.

<img src="https://github.com/Rahul9936/LearningReact/blob/master/images/Screen%20Shot%202018-04-05%20at%2012.22.22%20AM.png?raw=true" />

## Set up React JS
A simple way to start starightway to development in react would be using <b>create-react-app</b> package, its a npm package which sets up all the basic things like setting up webpack server and give us an bare minimum React component to start with.
Follow the below command to create a react app
1. npm i create-react-app -g
2. create-react-app MyApp
3. cd MyApp
4. npm start


As we know React is component based design, so we will start learning with Component and will discuss all the concepts related to it

## Creating Components
### there are multiple ways to create a component :beers:
- Method #1: The most simple form of creating a component in React
```javascript
function MyComponent (prop) {
    return /* write your JSX here */
}
```

- Method #2: Using javascript method
```javascript
var myComponent = React.createClass({
    render() {
        return /* write your jsx syntax here /*;
    }
})
```

Note: This method has been deprecated, latest version of react does not support this

- Method #3: Using Javascript Classes
```javascript
class MyComponent extends React.Component {
    render() {
        return /*write your jsx code here*/
    }
}
```

##### Components extending React.Component have some advantage over the functional components because functional components are stateless while class components are stateful component.

#### Stateful vs Stateless Components
A stateless component does not maintain the state of the state. So, basically stateless components are static component. It changes only when the parent component (Stateful) changes. For example, on FB page Login/Logout text can be stateless component because it does not change until the application state does not change.

## Attaching the components
In the above section we have learnt how to create the component now lets attach the above component with browser DOM,
ReactDOM. ReactDOM is used to render the react component on the web page, check the below code
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
class MyComponent extends React.Component {
    render() {
        return <div>Hello world</div>
    }
}

ReactDOM.render(<MyComponent />, document.getElementById("body"));
```

#### React vs ReactDOM
Initially there was only one library for React, it has both the functionality of React and ReactDOM. Later due to the emerge of React native which is used to support both the mobile and Web platform single library got split into two different libraries React and ReactDOM.
React support both the mobile as well web platform while ReactDOM supports only Web platform

#### Pure vs Impure functions
Pure functions returns the same value always if the given input is same and also does not modify the passed function arguments


## .js or .jsx :question:
React provides the support of writting the JSX so what should be the extension of the file .js or .jsx?
So to answer this question, I will say it does not matter because it is transpiled by the same Babel compiler which uses the same configuration for both the js and jsx so no need to provide the .jsx extension. If you are using different configuration for compiling the jsx file then you are good to go otherwise use .js extension for all the files.

<pre>
<b>Note: </b>Before babel, JSXTransfer tool was being used for compiling the jsx code so that requires file extension as .jsx only
but it has been deprecated and babel does not differentiate between .js or .jsx extension
</pre>
One advantage of using the .js syntax is while importing the file you don't need to provide the extension, for ex
```javascript
import MyComponent from './MyComponent'
```

### Examples
Hello world example - [js bin URl](http://jsbin.com/vuweno/1/edit?html,js,output)
Steps to remember:
    - Create a component and implement render method
    - Render method must returns the JSX expression
    - Mount this component which will be rendered on the screen

### Explanation of the above code

#### Export and Import modules in ES6
"Export" Statement is used to make a piece of code of a module visible and reusable to other modules.
"Import" statement is used to import a module in ES6, Importing modules has not existed before ES6 but it was possible by using libraries like CommonJS. CommonJS uses require() syntax and NodeJS utilises extensively this feature.
In our case, we are using Babel to transpile the ES6 code to ES5, so babel transpiles import ... from statement to require() statement which is used by webpack to bundle into a single file.
A module can import things from other modules , it refer to those modules via module specifiers as string in form of:

<strong>Relative Paths:</strong> ('../src/sn-component-form') load modules from a file located at the relative path <br />
<strong>Absolute path:</strong> ('/Documents/myapp/src/sn-component-form') load modules from a file located at absolute path <br />
<strong>Names:</strong> What module name has to refer needs to be configured, it can reference the node_modules folder or we can specify the loader for them
Example:

```javascript
//--------- lib.js --------
export var name = "XYZ";

//--------- Main.js -------
import name from './lib'
```
<pre><b>Note:</b>
1. .js extension can be omitted for javascript modules
2. Modules are singleton in nature, even if they are exported multiple times only a single instance of it exist
</pre> 

- Refer to this url for [List of syntax supported in ES6](https://gist.github.com/caridy/839d5359321604a12648)
- Refer to this [URL](https://hackernoon.com/node-js-tc-39-and-modules-a1118aecf95e) to understand how module import works in CommonJS and ES6 and what are the differeces between them
- Complete understanding of the Modules [URL](http://exploringjs.com/es6/ch_modules.html)

#### JSX
<img src="https://cdn-images-1.medium.com/max/1800/1*N2KU7pOcwZwKeOi3B-YBLQ.png"><br/>
JSX is similar to HTML like syntax used by react which is written in javascript file. Check the above example where render mehtod of MyComponent return jsx which can be mix of HTML or component or both.

JSX syntax transpiled into javascript object with transpiler like Babel, check the below example how JSX Elements are transpiled (right side) into javascript while we can directly write the javascript code instead of writting of JSX syntax code but it will increase the complexity and will be harder to maintain <br/>
<img src="https://cdn-images-1.medium.com/max/1800/1*iEMbKsYd4nCFiZ_yoRJvoA.png" />

##### HTML elements supported by JSX
<code>a abbr address area article aside audio b base bdi bdo big blockquote body br button canvas caption cite code col colgroup data datalist dd del details dfn div dl dt em embed fieldset figcaption figure footer form h1 h2 h3 h4 h5 h6 head header hr html i iframe img input ins kbd keygen label legend li link main map mark menu menuitem meta meter nav noscript object ol optgroup option output p param pre progress q rp rt ruby s samp script section select small source span strong style sub summary sup table tbody td textarea tfoot th thead time title tr track u ul var video wbr
</code>

##### Expressions in JSX
Javascript expressions can be embed in JSX using curly braces, for example:
```javascript
var userName = {
    firstName: "Joe",
    lastName: "Employee"
}
// we can use above javascript object in jsx
<div>{userName.firstName} {userName.lastName}</div>

// we can call javascript functions as well
function getName() {
    return "Joe Employee";
}
// jsx syntax will be like
<div>{getName()}</div>
```
##### Element Attributes in JSX
You will see attributes specified in HTML are written in camelCase in JSX but this is not necessary for custom attributes, but as JSX is more close to javascript than HTML then we should follow the javascript convention and specify attributes in camel casing. onclick attribute of html is used as onClick (camel case) in JSX similarly onchange is specified as onChange
Ex:
```
<div name="Joe Employee">Childrens</div>
<div count={2+3}>Childrens</div> // javascript expression in attributes
```
Properties can be accessed in Component by <strong>this.props.{property name}</strong>

<b>Note:</b> JSX specify HTML <em>class</em> and <em>for</em> property as <em>className</em> and <em>htmlFor</em> respectively to avoid any confusion and it also make more sense to mirror the conventions from the DOM API.
for ex:

```
<div className="red">Childrens</div> // here we have used className instead of class to specify the class attribute of the element
```
##### Inline styling in JSX
One thing should be noticed here is when specifying the inline style attribute in jsx, css should be in camel casing for example:
```
var redStyle = {
	color:'red',
	backgroundColor:'black',
	fontWeight:'bold'
};

<div style={redStyle}>Childrends</div>
```
Check in the above example css styles are in camel case,
background-color becomes backgroundColor and font-weight becomes fontWeight, all hyphen seperated styles should be camel case in JSX
##### html attributes supported in JSX
<code>
    accept accessKey action allowFullScreen allowTransparency alt autoCapitalize autoComplete autoFocus autoPlay cellPadding cellSpacing charSet checked className colSpan content contentEditable contextMenu controls data dateTime dir disabled draggable encType form frameBorder height hidden href htmlFor httpEquiv icon id label lang list loop max maxLength method min multiple name pattern placeholder poster preload radioGroup readOnly rel required role rowSpan scrollLeft scrollTop selected size spellCheck src step style tabIndex target title type value width wmode
</code>

### Props
- Props are one way of passing data to react component
- Props are immutable in nature
- Props can be accessed by this.props
- Props lets one component to be used at different places

Check the below example, how the props pass the data to the component. Run the below example on  [JSBin](http://jsbin.com/qekejop/1/edit?html,js,output)
```javascript
class HelloWorldComponent extends React.Component {
  render() {
    return (      
      <h1>Hello {this.props.name}</h1>   // it will render Hello Joe employee on the web page   
    );
  }
}

ReactDOM.render(
  <HelloWorldComponent name="Joe employee"/>,
  document.getElementById('react_example')
);
```

Passing javascript objects as props, check this example on [JsBin](http://jsbin.com/yiriyej/edit?html,js,output)
```javascript
class HelloWorldComponent extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello {this.props.user.name}</h1>
        <h3>Email: {this.props.user.email}</h3>
      </div>
    );
  }
}

const user = {
  name: "Joe Employee",
  email: "joe@employee.com"
}

ReactDOM.render(
  <HelloWorldComponent user={user}/>,
  document.getElementById('react_example')
);
```

### Component States
Component states are also used to store data for component similar to props but props can not change over time while states can change as a result of user interaction/events. States of a components are accesible by this.states. Changes in the value of states causes re-render of the UI.

Check the below example of how changing the state value causes the re-render of the component. [JsBin URL](http://jsbin.com/tosusac/edit?js,console,output)

```javascript
class CheckBoxComponent extends React.Component {
  constructor() {
    super();
    this.state = {
      checked: true
    }
  }
  
  handleCheckboxChange(event) {
    if(event.target.checked)
      this.setState({
        checked: true
      })
    else 
      this.setState({
        checked: false
      })
  }
  
  render() {
    var msg = "checked";
    if(this.state.checked){
      msg = "checked";
    } else {
      msg = "unchecked";
    }
    return(
      <div>
        <input type="checkbox" onChange={this.handleCheckboxChange.bind(this)}/>
        <div> Checkbox is {msg}</div>
      </div>
    )
  }
}

ReactDOM.render(<CheckBoxComponent />, document.getElementById("element"));
```
<b>Caution!</b> State is a double-edged sword. On the one hand, it’s useful for sanely controlling internal data. On the other, it can lead to all sorts of mayhem, if not properly controlled. Use it wisely!


### Component Constructor
Constructors for each component is not necessary, Component without constructor will work fine but sometimes it is useful like initializing component state. 
super() method should be called from the first line only of the constructor.
Two things to remeber while implementing constructor:
- Its necessary to call super() from constructor, <em>this</em> will be uninitialized if the super() is not called, for ex:
```javascript
class MyClass extends React.Component {
    constructor(){
        console.log(this) //Error: 'this' is not allowed before super()
    }
}
```
- Pass props while calling super(props) in constructor, it is necessary if we are accessing this.props in constructor method, Anywhere else it will be accessible automatically
```javascript
class MyClass extends React.Component{
    constructor(props){
        super();
        console.log(this.props); // this.props is undefined
    }
}
```
### Initializing state with getInitialState vs Initializing state in constructor
As we discussed previously there are two ways of creating component, if we follow the ES6 class pattern to create component then state should be initialized in  constructor, check the below example
```javascript
class MyComponent extends React.Component {
    constructor(){
        super();
        this.state = {
            // initialize your state here
        }
    }
}
```

If we are following the method approach to create component then implement getInitialState to initialize the state and this method will be called automatically as part of the Component lifecycle, check the below example
```javascript
var MyComponent = React.craeteClass({
    getInitialState: function() {
        return {
            // initialize your state here
        };
    }
})
```
### State Vs Props
<img src="https://ihatetomatoes.net/wp-content/uploads/2017/08/03-state-vs-props.png"/>

### Moving state up in React
When you want to aggregate data from multiple children or to have two child components communicate with each other, move the state upwards so that it lives in the parent component. The parent can then pass the state back down to the children via props, so that the child components are always in sync with each other and with the parent.

## Following topics has been covered in Advance react
- Flux
- Redux
