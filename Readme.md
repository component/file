# File

  File component wrapping the native `File` and `FileReader` objects
  with a higher level API.

## Installation

node.js:

```
$ npm install file-component
```

browser:

```
$ component install component/file
```

## Events

### Reader

  - `error` an error occurred
  - `progress` in progress (`e.percent` etc)
  - `end` read is complete

## Example

```js
var file = require('file');
var input = document.querySelector('input');

input.onchange = function(){
  var img = file(input.files[0]);

  if (!img.is('image/*')) {
    alert('Images only!');
    return;
  }

  var reader = img.toDataURL(function(err, str){
    if (err) throw err;
    var img = document.createElement('img');
    img.src = str;
    img.height = 300;
    document.body.appendChild(img);
  });

  reader.on('progress', function(e){
    console.log(e.percent);
  });
};
```

## API
  
### file(file)

  Wraps a `File` object:

```js
var file = require('file');
file(input.files[0]);
```

### File#is(type)

  Returns a boolean if the file's mime type matches `type`:

```js
var file = require('file');
file(input.files[0]);
file.is('image/*');
file.is('image/jpeg');
file.is('*/json');
```

### File#toArrayBuffer(fn)

  Convert to an `ArrayBuffer` and invoke `fn(err, result)`,
  returns a `Reader`.

### File#toText(fn)

  Convert to text and invoke `fn(err, result)`,
  returns a `Reader`.

### File#toDataURL(fn)

  Convert to a data uri string and invoke `fn(err, result)`,
  returns a `Reader`.

## License

  MIT
