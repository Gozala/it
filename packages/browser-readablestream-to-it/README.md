# browser-readablestream-to-it

[![Build status](https://travis-ci.org/achingbrain/it.svg?branch=master)](https://travis-ci.org/achingbrain/it?branch=master) [![Coverage Status](https://coveralls.io/repos/github/achingbrain/it/badge.svg?branch=master)](https://coveralls.io/github/achingbrain/it?branch=master) [![Dependencies Status](https://david-dm.org/achingbrain/it/status.svg?path=packages/it-all)](https://david-dm.org/achingbrain/it?path=packages/it-all)

> Turns a browser readable stream into an async iterable

## Install

```sh
$ npm install --save browser-readablestream-to-it
```

## Usage

```javascript
const toIt = require('browser-readablestream-to-it')
const all = require('it-all')

const content = [0, 1, 2, 3, 4]

const stream = new ReadableStream({
  start(controller) {
    for (let i = 0; i < content.length; i++) {
      controller.enqueue(content[i])
    }

    controller.close()
  }
})

// An optional object which may have the following keys:
const options = {
  // Unless `true` stream will be cancelled when consumed partially (e.g. break
  // in for await loop). Default to `false`.
  preventCancel: false
}

const arr = await all(toIt(stream, options))

console.info(arr) // 0, 1, 2, 3, 4
```

