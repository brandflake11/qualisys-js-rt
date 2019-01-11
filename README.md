# Real-time api for QTM
This is a javascript implementation of the real-time protocol used by Qualisys
Track Manager (QTM). 

It is used to stream data from a computer running QTM. The real-time api can
also be used to start and stop measurements, setting events and more.

# Installation
1. npm install qualisys-rt

# Example

```javascript
var Api = require('qualisys-rt').Api;

var api = new Api({ debug: true });

// Set up an event handler.
api.on('frame', function(data) {
	console.log('Received frame:'.green);
	console.log(data);
});

// Connect to host (defaults to 'localhost')
// and start streaming 3d data.
api.connect()
	.then(function() { return api.streamFrames({ components: ['3D'] }) })
	.catch(console.log)
;
```

# Getting started
There is not much documentation yet so the best way to get started is by
examining demo.js, which contains example code for common tasks. 

<img src="https://github.com/qualisys/qualisys-rt/blob/dev/docs/connecting.png" title="Example output" width="600" height="191">

## Viewer 2D
You can view 2D data in your terminal by using the Viewer2D class.
```javascript
api.connect(22223, 'localhost')
	.then(function() { return api.qtmVersion(); })
	.then(function() {
		var viewer = new Viewer2d(api);
		return viewer.render(1, { color: 'red' });
	})
```
<img src="https://github.com/qualisys/qualisys-rt/blob/dev/docs/viewer2d.png" title="Example output" width="600" height="448">

For a reference of what's possible with the real-time protocol, refer to the
[QTM Real-time Server Protocol Documentation](http://qualisys.github.io/rt-protocol/).