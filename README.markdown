# WebNoise
A noise generator for WebAudio.  

### Installation

Include `src/web-noise.js` in your HTML document:

	<script type="text/javascript" src="<path-to-web-noise>/src/web-noise.js"></script>

### Usage:

WebNoise requires an AudioContext:

	// Create an AudioContext:
	var context = null;
	if (typeof window.AudioContext != 'undefined') {
		context = new AudioContext();
	} else if (typeof window.webkitAudioContext != 'undefined') {
		context = new webkitAudioContext();
	}

	if (!context) {
		console.log('Web Audio API is not supported.');
		return;
	}

	// Create a noise generator and call configureNode() to prepare it:
	var noise = new WebNoise(context);
	noise.configureNode();

You can specify the buffer size, input channel count and output channel count by passing them to `configureNode()`:

	noise.configureNode({
		bufferSize: 256,
		inputChannels: 1,
		outputChannels: 1
	});

After calling `configureNode()`, the node can be accessed via the `.node` property:

	// Connect the noise generator node to the context destination (output):
	noise.node.connect(context.destination);

You can adjust the noise character by setting the block size. This changes the rate at which the noise is generated. The block size is an integer with a minimum value of `1`.

	// Set the block size:
	noise.blockSize(8);

	// Get the current block size:
	var size = noise.blockSize();

### License:
WebNoise is made available under the MIT License. See LICENSE.txt for details.  

### Credits:
WebNoise was created by [Tony Wallace](http://tonywallace.ca).  

