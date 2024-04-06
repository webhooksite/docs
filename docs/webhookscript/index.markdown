---
title: WebhookScript
nav_order: 500
has_children: true
---

# About WebhookScript

!["WebhookScript" Custom Action screenshot](/images/webhookscript-in-action.png)

WebhookScript is an easy to use scripting language designed for executing Web-related actions on incoming requests. 

While the other actions like Extract Regex and Send Email allows you to create flows in a visual editor, WebhookScript makes it quicker to create more advanced logic.

WebhookScript can be combined with other Custom Actions as data can be shared between them using [Variables](/custom-actions.html#about-variables).

## Syntax

The syntax is very similar to PHP and JavaScript. See also the [full language specification](/webhookscript/reference.html).

```javascript
products = [
  'apple':     ['price': 10],
  'blueberry': ['price': 1],
  'cake':      ['price': 550]
]

shouldAddVat = var('request.query.vat');
selectedProduct = var('request.query.product');

if (!selectedProduct) {
    respond('Please select a product!', 500)
}

price = products[selectedProduct]['price'];

if (shouldAddVat == 1) {
    price = price * 1.25;
}

respond(
    'Your price is {}'.format(price),
    200
);
```

## Variables in WebhookScript

[Custom Action Variables](/custom-actions.html#about-variables) in WebhookScript behave a little differently than other action types: in the code, they will *not* be replaced automatically like in other action types.

Instead, to interface with Custom Action Variables (created in previous actions, or default variables provided for each request or email), the function [var()](/webhookscript/functions/variables.html#varstring-variable_name-stringnumber-default-mixed) can be used.

The dollar-sign syntax (e.g. `$request.content$`) is optional when using the `var()` function, and the following two statements are equivalent: `var('$request.content$')` / `var('request.content')`.

In addition, [set()](/webhookscript/functions/variables.html#setstring-variable_name-string-variable_value) can be used to export a variable from your script to further downstream actions.  [store()](/webhookscript/functions/variables.html#storestring-global_variable_name-any-value-any) is used to permanently set a Global Variable.

## About the Editor

!["WebhookScript" Custom Action screenshot](/images/webhookscript-action.png)

### Shortcuts

The shortcuts are available when the editor is focused.

| Windows  | Mac     | Shortcut                       |
|----------|---------|--------------------------------|
| Alt-R    | Alt-R   | Test code (update Debug Panel) |
| Ctrl-S   | Cmd-S   | Save action without exiting    |

### Debug Panel

Below the editor is the "debug panel" containing data relating to the current and previous actions:

* **Debug outputs** shows the outputs of all the actions, with the current action being edited or created marked in blue.

* **Response** shows details of the response of the URL formatted in JSON.

* **Variables** is a table of all current available variables for use in the script with the `var()` function or `variables` array.

### Fullscreen Mode

To enable fullscreen mode, click the Expand button in the upper right corner to make the editor take up more screen space. Click again to disengage fullscreen mode.
