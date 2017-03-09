
# nyce

[![Circle CI](https://circleci.com/gh/recursivefunk/nyce.png?circle-token=b1d0d5b046161f60cc5816afb82b741db7163344)](https://circleci.com/gh/recursivefunk/nyce)

### JavaScript component interface definition and adherence utility

```javascript

// in someModule.js
exports.index = (foo, bar) => { /* ... */ };
exports.aProp = {};

// elsewhere
const nyce = require('nyce')();
const someModule = require('./someModule');

const myInterface = {
  index: {
    type: 'function',
    args: [ 'foo', 'bar' ],
    // By default, for function validation, nyce will only check the number
    // of arguments present with no regard to naming. If you would like to
    // fail validation if the names of the function arguments don't match the names
    // of the the interface arguments set this to true
    enforceArgNaming: true
  },
  aProp: {
    type: 'object'
  }
};

nyce
  .define('resource', myInterface)
  .then(nyce.assertImplements('resource', someModule))
  .then(() => {
    console.log( 'yay!' );
  })
  .catch((e) => {
    console.log('oh no!')
  });

```
