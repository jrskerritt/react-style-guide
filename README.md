
# PayScale React Coding Standards

#### Sources

Based on the styles recommended from:

1. https://github.com/Khan/style-guides/blob/master/style/react.md
2. https://reactjsnews.com/react-style-guide-patterns-i-like/
3. [React.js Training](https://reactjs-training.com/) by [Ryan Florence](https://twitter.com/ryanflorence) and [Michael Jackson](https://twitter.com/mjackson)


# Classes

* Component class names should always begin with an upper case character. React expects elements starting with a lower case character to be built-in HTML elements and will throw an error if your component starts with one.

    ```js
    // Bad
    var myComponent = React.createClass({ /* ... */ });

    // Good
    var MyComponent = React.createClass({ /* ... */ });
    ```

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

* Always define the component's props in a `propTypes` object. This makes it easy to quickly see all of the props that are used in the component, gives the reader an idea of what the component does, and adds validation to incoming props on a new instance. Comment these props generously and alphabetize them if there are many.

* The `render` method should always be last - this way you can easily find it by scrolling to the bottom of the file.

* Prefix custom methods and event handlers with an underscore.

* Event handlers should be named `_handle{EventName}`. Props that pass event handlers should be named `on{EventName}`.

    ```js
    _handleButtonClick : function () {}
    ```

    ```js
    <Component onButtonClick={this._handleButtonClick.bind(this)} />
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

* Align props when you can't fit them all on a single line. The ending ">" of the opening tag should go on its own line. This makes it clearly visible where the opening tag ends and the element's children begin.

    ```js
    // Bad
    <div className="foo-container"
        data-bar="some value">
        { /* ... */ }
    </div>

    // Good
    <div className="foo-container" data-bar="some value">
        { /* ... */ }
    </div>

    // Good
    <div
        className="foo-container"
        data-bar="some value"
    >
        { /* ... */ }
    </div>
    ```

* Open elements that span multiple lines on the same line. This conserves space because it requires one fewer tab and also saves a couple of lines.

    ```js
    // OK...
    var multilineJsx = (
        <div>
            { /* ... */ }
        </div>
    );

    // Better
    var multilineJsx = <div>
        { /* ... */ }
    </div>;

    // Better
    var multilineJsx = <div
        className="really very long class"
        id="reallyReallyReallyLongId"
        data-foo="some important value"
    >
        { /* ... */ }
    </div>;
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

* In general, avoid using jQuery within React components.
* Never use jQuery in a component for DOM manipulation.
* Performing ajax with jQuery in your component is fine.
* If you're using a jQuery plugin, consider encapsulating the use of the plugin in its own component so that you only have to manage it in a single place.

