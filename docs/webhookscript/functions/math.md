## Trigonometry

### atan(***number*** number) : number

### cos(***number*** number) : number

### sin(***number*** number) : number

### tan(***number*** number) : number

## Hexadecimal & Binary

### bin2hex(***string*** data): string

Converts a binary tring to a hexadecimal representation.

### hex2bin(***string*** hex_string) : ?string

### num2hex(***number*** number) : string

### hex2num(***string*** hex_string) : number

## General 

### abs(***number*** number) : number

### ceil(***number*** number) : number

Rounds a number up to nearest integer.

### floor(***number*** number) : number

Rounds a number down to nearest integer.

### is_numeric(***any*** value) : bool

Returns `true` if `value` is numeric. 

Examples: 

* `12345` returns `true`.
* `"1.0"` returns `true`.
* `null` returns `false`.

### max(***array*** numbers) : number

### min(***array*** numbers) : number

### mod(***number*** number, ***number*** divisor) : number

Returns the remainder after number is divided by `divisor`.

### number_length(***number*** number) : number

### pi() : number

Returns the value of Pi.

### pow(***number*** number, ***number*** power) : number

### rand(***number*** min, ***number*** max) : number

Returns a random number between `min` and `max`.

### round(***number*** number, ***number*** precision) : number

Rounds a number up with specified precision (number of digits after decimal point.)

```javascript
round(1.39, 1) // -> 1.4
```

### sqrt(***number*** number) : number

### to_number(***any*** value) : number
