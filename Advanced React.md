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

### Efficient rendering using Virtual DOM
Its a blueprint of DOM, tree data structure of plain javascript, detached from the browser-specific implemeation details. It exists in memory never actually gets rendered on web page.
React does not directly modifies the DOM structure, first it updates the Virtual DOM and take the diff and update only that part instead of re-rendering the DOM structure which save a lot of time. Check the below image to get the clarity on how the React's Virtual DOM diff works
<b>Note:</b> Concept of Virtual DOM is not developed by react, it has existed before react just uses this concept (Angular and Vue)
<img src="https://i.stack.imgur.com/S1vng.png"/>


### Data Binding in React
TO DO: Update this content later

### Immutability in react
If an object is immutable and we try to update that object then instead of updating this object, it will create a new object, and taht makes it easier to track the made in any object. This concept for update in Component State and Props makes it useful in re rendering of component.
