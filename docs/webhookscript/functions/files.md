
When you send an email, or send a multipart/form-data request, files are extracted as the `file.*.*` variables, but you can also loop over files using WebhookScript.

### files(***string*** name) : array

Returns an array of files, with the following keys:

* id - unique file ID
* filename - original filename
* size - size of the file in bytes
* content-type - mime content type of the file

```javascript
dump(files())

// [
//   0: [
//     "id": "76b7274a-e806-4f72-ba49-85ad05926ef0", 
//     "filename": "Screen Shot 2020-06-05 at 2.15.29 PM.png", 
//     "size": 1203671, 
//     "content_type": "image/png"
//   ]
// ]

// Filtering files by type
for (file in files()) {
    if (r'.*\.png'.match(file['filename'])) {
        dump(file['filename'] + ' is png.')
    }
}

// "Screen Shot 2020-06-05 at 2.15.29 PM.png is png."
```

### file_content(***string*** fileId) : string

Returns the content of a specific file, using the `id` key from the `files()` function above.

```javascript
firstFile = array_get(files(), 0)
fileContent = file_contents(firstFile['id']);
```