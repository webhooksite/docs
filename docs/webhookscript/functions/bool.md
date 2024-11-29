

https://github.com/user-attachments/assets/afb93940-f507-4b26-95f4-a78c7417cfdf

### bool_and(***bool*** value1, ***bool*** value2): ***bool***

Returns `value1 && value2`

### bool_not(***bool*** value) : ***bool***

Returns `!value`

### is_empty(***any*** value): ***bool***

Returns `true` if:

* value is `""` (empty string)
* value is `[]` (empty array)
* value is `null`

### is_null(***any*** value) : ***bool***

Returns `true` if value is `null`. An alternative to `if (value == null)` that won't break when `value` isn't null due to type checking.

Example:

```javascript
value = 'example'
if (is_null(value)) {
  // Won't trigger a type error
}
```

### to_bool(***string/number/array/bool*** value) : ***bool***

Casts `value` to a bool.
