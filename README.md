## node-walker

This module allows you to specify a directory and then walk over each file in that directory and its subdirectories. You may specify a callback function which is called for each file.

You could use this for example to require all modules in a given folder.

### Installation

You can download the repository or simply install this module through npm:

    npm install node-walker

### Usage

Include the module through `require`. 

    var walker = require('node-walker');

You then have a reference to a function, which takes the following arguments:

    walker ( path, callback );
    
The callback function should take the following arguments:

    function callback ( errorObject, fileName, fnNext ) { }
    
Whereas `errorObject` is `null` whenever no error occurred and `fileName` will be either a `string` or `null` in case of an error or when all files have been read. You then must call `fnNext();` in order to read the next file.

Note that `fileName` will hold the absolute file names, and again, it will only hold names of real files.

### Example

You may also run `example.js` through node.

```javascript
    // include the module
    var walker = require('node-walker');

    // start walking over all files in a given folder
    walker( 'path/to/folder', 
    
        function (errorObject, fileName, fnNext) {
    
	        // an error occurred
	        if (errorObject) throw errorObject;
	        
	        // a filename has been provided
	        if (fileName !== null) {
	        
	            // do something with that filename
	            console.log('File: ' + fileName);
	        }
	        
	        // all files have been read, fileName is null
	        if (fileName === null) {
	        
	            // continue with some other task
	            return;
	        }
	        
	        // call next(); when you want to proceed
	        if (fnNext) fnNext();
        }
    );
```

If you prefer relative file names, you can do something like this:

```javascript

    // define the path from which paths will be relative
    var root = __dirname;

    // remove the first n characters of the filename,
    // where n is the length of that path
    fileName = fileName.substr(root.length +1);
```

### License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)

Copyright (C) 2012 Geerten van Meel

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.