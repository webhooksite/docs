### array_contains(***array*** array, ***string/number*** needle) : bool

Returns true or false depending on whether ***array*** contains a value equal to ***needle***.

To check whether a key exists, use the `array_has` function.

```javascript
employees = [6547: 'Simon', 235345: 'Jack', 4657: 'Jim']

dd(array_contains(employees, 'Simon'))
// -> true
```

### array_chunk(***array*** array, ***number*** count, ***bool*** preserve_keys = false) : array

Splits a single array into chunks of `count`. When `preserve_keys` is set to `true`, the array keys are preserved.

```javascript
test_arr = [
    'a': 123,
    'b': 234,
    'c': 345,
    'd': 345, 
    'e': 456
]

dump(array_chunk(test_arr, 2, true))
// -> [0: ["a": 123, "b": 234], 1: ["c": 345, "d": 345], 2: ["e": 456]]

dump(array_chunk(test_arr, 2, false))
// -> [0: [0: 123, 1: 234], 1: [0: 345, 1: 345], 2: [0: 456]]
```

### array_copy(***array*** array) : array

Returns a copy of ***array***

### array_diff(***array*** array1, ***array*** array2) : array

Returns the items of array1 that are not present in array2 while keeping the array indices.

### array_get(***array*** array, ***string/number*** index, ***any*** default) : any

### array_has(***array*** array, ***string/number*** key) : bool

Returns true if `array` contains `key`, and false if it does not.

To check whether a value exists, use the `array_contains` function.

```javascript
employees = [6547: 'Simon', 235345: 'Jack', 4657: 'Jim']

dd(array_has(employees, 235345))
// -> true
```

### array_join(***array*** array, ***string*** joiner) : string

Returns a string where all the values are joined by `joiner`.

```javascript
['hello', 'world'].join(',')
-> "hello,world"
```

### array_keys(***array*** array) : array

Returns the keys of an array.

### array_length(***array*** array) : number

### array_map(***array*** array, ***func*** function)

Runs function with each array value, and returns array with key as result.

```javascript
employees = ['Simon', 'Jack', 'Jim']

result = array_map(employees, function (employee) {
    return 'Hello, '+employee+'!'
})

dd(result)

// -> [0: "Hello, Simon!", 1: "Hello, Jack!", 2: "Hello, Jim!"]
```

### array_merge(***array*** array1, ***array*** array2): array

Merges 2 arrays into a single array.

```javascript
test1 = [123, 234, 345]
test2 = [345, 456]

dump(array_merge(test1, test2))

// -> [0: 123, 1: 234, 2: 345, 3: 345, 4: 456]
```

### array_number_of(***array***, ***string/number*** value) : number

Returns amount of ***value***

### array_pop(***array*** array) : any

Pop element off end of array

### array_push(***array*** array, ***any*** value) : any

Adds ***value*** to end of ***array*** and returns ***value***

### array_random(***array*** array) : any

Returns random value of ***array*** 

### array_range(***array*** array, ***int*** offset, ***?int*** length = 0, ***?bool*** preserve_keys = false) : array

Returns a range of `array`, starting from `offset`, and returns the amount specified in `length` if set (otherwise until the end of the array.) 

If `preserve_keys` is true, the result has the array keys preserved.

```javascript
array = ['one', 'two', 'three', 'four', 'five']

dump(array_slice(array, 2))
// [0: "three", 1: "four", 2: "five"]

dump(array_slice(array, 2, 2))
// [0: "three", 1: "four"]

dump(array_range(array, -3, 2))
// [0: "three", 1: "four"]
```

### array_reverse(***array*** array) : array

Returns ***array*** in reverse order

```javascript
employees = [6547: 'Simon', 235345: 'Jack', 4657: 'Jim']

dd(array_reverse(employees))
// -> [0: "Jim", 1: "Jack", 2: "Simon"]
```

### array_shuffle(***array*** array) : array

Returns shuffled version of ***array***

### array_sort(***array*** array) : array

Sorts ***array*** by its values. Keys are kept as-is.

### array_splice(***array*** array, ***int*** offset, ***?int*** length, ***array*** replacement) : array

Removes `length` amount of values from `array`, starting from `offset` (if `offset` is negative, starts from the end of the array.)

If `replacement` is specified, the removed values are replaced with it.

```javascript
array = ['one', 'two', 'three', 'four', 'five']

dump(array_splice(array, 2, 2))
// [0: "one", 1: "two", 2: "five"]

dump(array_splice(array, 2, 2, ['hello']))
// [0: "one", 1: "two", 2: "hello", 3: "five"]
```

### array_values(***array*** array) : array

Returns the values of an array.

```javascript
employees = [6547: 'Simon', 235345: 'Jack', 4657: 'Jim']

dd(array_values(employees))

// -> [0: "Simon", 1: "Jack", 2: "Jim"]
```

### to_array(***array*** array) : array

Returns ***array***.
