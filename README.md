
# PayScale React Coding Standards

#### Sources

Based on the styles recommended from:

1. https://github.com/Khan/style-guides/blob/master/style/react.md
2. https://reactjsnews.com/react-style-guide-patterns-i-like/


# Classes

* Methods should generally be ordered by the following:

    1. `displayName`
    2. `propTypes`
    3. Lifecycle methods in order of first to last
    4. Custom methods
    5. `render`
    
    ```js
    React.createClass({  
        displayName : '',
        propTypes: {},
        getInitialState : function () {},
        componentWillMount : function () {},
        componentWillUnmount : function () {},
        _handleButtonClick : function () {},
        _myCustomMethod: function () {},
        render : function () {}
    });
    ```

* Always define the component's props in a `propTypes` object. This makes it easy to quickly see all of the props that are used in the component, gives the reader an idea of what the component does, and adds validation to incoming props on a new instance.

* The `render` method should always be last - this way you can easily find it by scrolling to the bottom of the file.

* Prefix custom methods and event handlers with an underscore. 

* Event handlers should be named `_handle{EventName}`. Props that pass event handlers should be named `on{EventName}`.

    ```js
    _handleButtonClick : function () {}
    ```

    ```js
    <Component onButtonClick={this.handleButtonClick.bind(this) />
    ```

# ES6

Defining a component class in ES6 is done like this:

```js
const displayName = '';
const propTypes = {};
 
class FooComponent extends React.Component {
    constructor() {
        super(props);
        this.state = {};
    }
     
    componentWillMount() {}
    componentWillUnmount() {}
    _handleButtonClick() {}
    _myCustomMethod() {}
    render() {}
}
 
FooComponent.displayName = displayName;
FooComponent.propTypes = propTypes;
```

* Defining `displayName` and `propTypes` as constants at the top achieves the same result as in the ES5 example from above - key information about the component is easily discoverable at the top of the file.

* A constructor that calls `super(props)` is required.

* `getInitialState` should not be defined on your class - set `this.state` in your constructor instead.


# JSX

* Align properties when you can't fit them all on a single line.
    
    ```js
    // Bad
    <div className="foo-container"
        data-bar="some value">
    
    // Good
    <div className="foo-container" data-bar="some value">
    
    // Good
    <div
        className="foo-container"
        data-bar="some value">
    ```

* Open elements that span multiple lines on the same line. This conserves space because it requires one fewer tab and also saves a couple of lines. The exception would be if your parent element is long and doesn't fit on a single line. In this case it is fine to use parentheses and align props/attributes.

    ```js
    // Bad
    var multilineJsx = (
        <div>
            // ...
        </div>
    );
    
    // Good
    var multilineJsx = <div>
        // ...
    </div>;
    
    // OK
    var multilineJsx = (
        <div class="really very long class" id="reallyReallyReallyLongId">
            // ...
        </div>
    );
    
    // OK
    var multilineJsx = (
        <div 
            class="really very long class" 
            id="reallyReallyReallyLongId"
            data-foo="some important value">
            // ...
        </div>
    );
    ```

* Variables holding a JSX object can stay on one line if it is short enough.
    
    ```js
    var singleLineJsx = <h1>My header</h1>;
    ```

* Components without children should be self-closing.
    
    ```js
    // Bad
    <FooComponent></FooComponent>
    
    // Good
    <FooComponent />
    ```

* When rendering a list of components from an array, do it inline if it makes sense. If the map function is too long or complicated, consider extracting it out into its own method on the component class.

    ```js
    <ul>
        {items.map(function (item, i) { 
            return <li key={i}>{item}</li>;
        )}
    </ul>;
    
    // or with ES6
    
    <ul>
        {items.map((item, i) => <li key={i}>{item}</li>)}
    </ul>;
    ```


# jQuery

* In general, avoid using jQuery within React components when possible.
* Never use jQuery in a component for DOM manipulation.
* Performing ajax with jQuery in your component is fine.
* If you're using a jQuery plugin, consider encapsulating the use of the plugin in its own component so that you only have to manage it in a single place.

