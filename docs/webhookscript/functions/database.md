## Database

### db(***string/int*** db_id) : function

The `db_id` parameter must either be the name or ID of a [Webhook.site Database](/database.html) instance.

When called directly, `db()` returns a Webhook.site Database instance in the form of a function that takes the following arguments: `query`, `params` and returns an array with the following keys: `result`, `error`, `time`.

```javascript
// Connect to a Webhook.site Database instance
mydb = db('mydb')

// You can use both numeric parameter names ...
res = mydb(
  'insert into users (name, email) values (?, ?)',
  [
    get('request.query.name'),
    get('request.query.email')
  ]
)
dump(res)
// [
//   "result": [
//     0: []
//   ], 
//   "error": null, 
//   "time": 0
// ]


// ... as well as named
res = mydb(
  'select * from users where email = :email',
  [
    'email': get('request.query.email')
  ]
)
dump(res)
// [
//   "result": [
//     0: [
//       "name": "example", 
//       "email": "user@example.com"
//       ]
//     ], 
//   "error": null, 
//   "time": 0
// ]


// On error, the `error` key is set:
res = db('select * from nonexisting_table')
dump(res)
// [
//   "result": null, 
//   "error": "Undefined table: 7 ERROR: relation \"nonexisting\" does not exist", 
//   "time": 0
// ]
```