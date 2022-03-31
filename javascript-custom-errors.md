# Custom Error class in JavaScript or NodeJs

1. Using vanilla JavaScript syntax
```js

function CustomError(message, extra) {
  var instance = new Error(message);
  instance.name = 'CustomError';
  instance.extra = extra;
  Object.setPrototypeOf(instance, Object.getPrototypeOf(this));

  // NOTE: Only available on V8, It is not JavaScript standard function, It will creates the `stack` property
  if (Error.captureStackTrace) {
    Error.captureStackTrace(instance, CustomError);
  }
  return instance;
}

CustomError.prototype = Object.create(Error.prototype, {
  constructor: {
    value: Error,
    enumerable: false,
    writable: true,
    configurable: true
  }
});

if (Object.setPrototypeOf){
  Object.setPrototypeOf(CustomError, Error);
} else {
  CustomError.__proto__ = Error;
}
```
2. Using ES6 syntax
```ES6
class CustomError extends Error {
  constructor(message, extra) {
    super(message);
    Error.captureStackTrace(this, this.constructor);
    this.name = 'CustomError';
    this.message = message;
    if (extra) this.extra = extra;
  }
}
```
