These functions lets you interface with other Custom Actions by getting and setting variables from them. These functions are also how you retrieve Global Variables defined in the Control Panel.

### var(***string*** variable_name, ***?string/number*** default) : mixed

Retrieves the value of a Variable or Global Variable (defined in the Control Panel). The surrounding dollar signs are not mandatory.

Returns `null` (or the value of `default`) if the variable does not exist.

```javascript
var('request.header.x-request-verification') // returns value of the `x-request-verification` header
```

### set(***string*** variable_name, ***string*** variable_value)

Exports a Variable for use in downstream actions, like the *Set Runtime Variable* action.

For example, the following code:

```javascript
set('myvar', 'Hello world')
```

Would cause the string `$myvar$` to be replaced with `Hello world` in all subsequent actions.

### store(***string*** global_variable_name, ***any*** value): ***any***

Permanently creates or updates a Global Variable (as defined in Control Panel.)

The value can also be retrieved with the `var()` function in subsequent action executions.

### delete(***string*** global_variable_name)

Deletes a global variable.

### variables : array

A variable (not a function) containing an associative array with all available Webhook.site variables.

```javascript
user_agent = variables['request.header.user-agent']
```
