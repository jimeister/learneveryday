# React refs with multiple input types

When working with forms, if there are multiple input values that need to be processed with the `onChange` event, here are some ways:

Using `ref` string attribute
```
handleChange: function() {
  this.props.onUserInput(
    this.refs.filterTextInput.value,
    this.refs.inStockOnlyInput.checked
  );
},
render: function() {
  return (
    <form>
      <input
        type="text"
        placeholder="Search..."
        value={this.props.filterText}
        ref="filterTextInput"
        onChange={this.handleChange}
      />
      <p>
        <input
          type="checkbox"
          checked={this.props.inStockOnly}
          ref="inStockOnlyInput"
          onChange={this.handleChange}
        />
        {' '}
        Only show products in stock
      </p>
    </form>
  );
}
```

To avoid using the [ref string attribute](https://facebook.github.io/react/docs/more-about-refs.html#the-ref-string-attribute), an event handler can be used per input:
```
getInitialState: function() {
    return {
      value: 'Hello!',
      author: 'Jim'
    };
},
handleValueChange: function(event) {
  this.setState({value: event.target.value});
},
handleAuthorChange: function(event) {
  this.setState({author: event.target.value});
}
render: function() {
  return (
    <input
      type="text"
      value={this.state.value}
      onChange={this.handleValueChange}
    />
    <input
      type="text"
      value={this.state.author}
      onChange={this.handleAuthorChange}
    />
  );
}
```
[refs](https://facebook.github.io/react/docs/more-about-refs.html)  
[forms](http://facebook.github.io/react/docs/forms.html)
[stackoverflow](http://stackoverflow.com/questions/21029999/react-js-identifying-different-inputs-with-one-onchange-handler)
