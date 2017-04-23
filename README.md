# node-sloc
A small tool written in node for counting source lines of code.

## Installation
Can be used as either a command line application or as a module.

### As a command line application
```
npm install -g node-sloc
```
### As a node module
```sh
npm install --save node-sloc
```
# Usage
## Command Line
``` node-sloc [path] [options] ```
### Options
```
usage:
           node-sloc [path] [options]
options:
           -h, --help                         Prints usage information (the one you're reading right now)

           -l, --list-extensions              Lists all default file extensions

           -e, --include-extensions <list>    Include non-default file extensions,
                                              specified by a comma separated string of extensions

           -i, --ignore-extensions <list>     Include list of file extensions to ignore,
                                              specified by a comma separated string of extensions

           -x, --ignore-paths <list>          Include a list of folders to exclude

           -d, --ignore-default               Ignore the default file extensions

           -v, --verbose                      Output extra information during execution

```
## Examples
```
 node-sloc "../app"
 node-sloc "../app" --include-extensions "aaa, bbb, ccc" --ignore-extensions "xml, yaml"
 node-sloc "../app" --ignore-paths "node_modules"
 node-sloc file.js
```

## Module
```
const sloc = require('node-sloc')

const options = {...}

sloc(options).then((res) => {...})
```

### Options
The options object the function takes as a parameter has the following properties:
```
path             Required. The path to walk or file to read.
extensions       Additional file extensions to look for. Required if ignoreDefault is set to true.
ignorePaths      Optional. A list of directories to ignore.
logger           Optional. Outputs extra information to if specified.
```
### Resolved object
The object returned when executing the function has the following structure:
```js
{
  paths,        // An array of all filepaths counted
  sloc: {       // Object containing the data
    loc,        // Lines of code (SLOC + comments)
    sloc,       // Source lines of code
    blank,      // Number of blank lines
    comments,   // Lines of comments
    files,      // Number of files counted
  }
}
```

### Example
```js
const sloc = require('node-sloc')

const options = {
  path: '../app',                      // Required. The path to walk or file to read.
  extensions: ['aaa', 'bbb', 'ccc'],   // Additional file extensions to look for. Required if ignoreDefault is set to true.
  ignorePaths: ['node_modules'],       // A list of directories to ignore.
  logger: console.log,                 // Optional. Outputs extra information to if specified.
}

sloc(options).then((res) => {
  console.log(res.paths, res.sloc.sloc, res.sloc.comments)
})

```
