<p align="center">
  <img src="resources/preconf-logo.png" width="400" alt="preconf">
  <br>
  <a href="https://www.npmjs.org/package/preconf"><img src="https://img.shields.io/npm/v/preconf.svg?style=flat" alt="npm"></a> <a href="https://travis-ci.org/synacor/preconf"><img src="https://travis-ci.org/synacor/preconf.svg?branch=master" alt="travis"></a>
</p>

A Higher Order Component that provides configuration (from context & defaults) as props.

Preconf is just 400 bytes and works well with [preact-context-provider](https://github.com/synacor/preact-context-provider).

* * *

## Usage

```js
import preconf from 'preconf';
import Provider from 'preact-context-provider';

// generally from an import
const defaults = {
	greeting: 'hello'
};

let configure = preconf(null, defaults);

/** Wire two configuration fields up to props: */
@configure('greeting, name')
class Foo extends Component {
	render({ greeting, name }) {
		return <span>{greeting}, {name}</span>
	}
}

/** Render from defaults: */
render(<Foo />);
// <span>hello, </span>

/** Provide overrides as `context.config`: */
render(
	<Provider config={{ name: 'Stan' }}>
		<Foo />
	</Provider>
);
// <span>hello, Stan</span>
```

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### preconf

Creates a higher order component that provides values from configuration as props.

**Parameters**

-   `namespace` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)?** If provided, exposes `defaults` under a `namespace`
-   `defaults` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)?** An object containing default configuration values

**Examples**

```javascript
let configure = preconf();
export default configure({ a: 'a' })(MyComponent);
```

```javascript
let configure = preconf(null, { url:'//foo.com' });
export default configure({ url: 'url' })( props =>
	<a href={props.url} />
);
```

```javascript
let configure = preconf('weather', { url:'//foo.com' });
export default configure({
	url: 'weather.url'
})( ({ url }) =>
	<a href={props.url} />
);
```

Returns **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** [configure()](#configure)

#### configure

Creates a Higher Order Component that provides configuration as props.

**Parameters**

-   `keys` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>)** An object where the keys are prop names to pass down and values are dot-notated keypaths corresponding to values in configuration. If a string or array, prop names are inferred from configuration keys.

Returns **[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)** configureComponent(Component) -> Component
