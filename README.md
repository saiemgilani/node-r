# node-r

### Experimental

Node.js module for running R scripts

## Installation

R needs to already be installed, and [jsonlite](https://cran.r-project.org/web/packages/jsonlite/index.html) R library needs to be installed.

`yarn add node-r` or `npm install node-r`

## Usage

In an R file:

```R
input[[1]] + input[[2]]
```

In node:

```javascript
const { R } = require('node-r')

let r = new R('./add.R')

// optionally pass an options object used in child_process spawn calls
let r = new R('./add.R', {env: {PATH: '/bin:/location/to/R/bin'}})

// data is converted to a list variable `input` in the R script
r.data(2, 3)

// call the script async
r.call()
  .then(response => response === 5) // true
  .catch(e => console.log('error : ', e))

// OR call the script async

let result = r.callSync() // could raise an exception
result === 5 // true
```
