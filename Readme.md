*This repository is a mirror of the [component](http://component.io) module [component/worker](http://github.com/component/worker). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/component-worker`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*

# worker

  Web worker API wrapper.

## Installation

    $ component install component/worker

## API

### Worker(script)

  Initialize a worker with the given `script`.

### Worker#send(msg)

  Send a message to the worker.

```js
var upper = new Worker('uppercase.js');

upper.on('message', function(msg){
  console.log(msg.string);
});

upper.send({ string: 'hello' });
upper.send({ string: 'world' });
```

### Worker#send(msg, callback[, transferables])

  Send a request message to the worker with the given `callback`. When
  using the request/response paradigm you should pass the `e.data.id` property
  back with your response so that the correct callback may be invoked:

worker:

```js
onmessage = function(e) {
  setTimeout(function(){
    postMessage({ id: e.data.id, string: e.data.string.toUpperCase() });
  }, 500);
};
```

client:

```js
upper.send({ string: 'hello' }, function(msg){
  console.log(msg.string);
});
```

### Worker#close()

  Terminate the worker.

## License

  MIT
