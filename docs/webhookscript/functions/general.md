## About Functions

These are the functions that can be used in your script, and includes various utility functions and functions to interact with your Webhook.site URL.

### Chaining

Functions can be chained directly to a primitive (strings, numbers, arrays).

These two statements are equivalent:

```javascript
'Hello World'.echo()
```

```javascript
echo('Hello World')
```

They can even be chained, for example:

```javascript
'Hello World'.hash('md5').echo() 
```

Furthermore, functions that begin in a type can be referenced without it, for example, when calling the `format` function with the first argument being a string, the language infers that actually the `string_format` function should be used.

```javascript
echo(string_format('hello %s', 'world')) // hello world

'hello %s'.format('world').echo() // hello world
```

Read more about functions in the [reference](/webhookscript/reference.html#functions).

### Custom functions

Define your own functions like this:

```javascript
function sub(a, b) {
    return a - b;
}
```

Read more about functions in the [reference](/webhookscript/reference.html#functions).

## Debugging and output

### echo(...***string*** string)

Adds `string` to script debug output.

### dd(...***any*** value)

Stops Custom Action execution and adds `value` to script debug output.

### dump(...***any*** value)

Adds `value` as a decoded string to script debug output.

## Types

### type(***any*** value) : ***string***

Returns the type name of a value, e.g. `"string"`.
