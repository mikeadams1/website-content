Skip to content
 
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@mikeadams1 
3
16 75 flaviocopes/website-content
 Code  Issues 1  Pull requests 2  Security  Insights
You’re editing a file in a project you don’t have write access to. Submitting a change to this file will write it to a new branch in your fork mikeadams1/website-content, so you can send a pull request.
website-content
/
post
/
web-platform-api
/
webrtc
/
index.md
 

26
​
27
It is supported by all the modern browsers (with partial support from Edge which does not support `RTCDataChannel` - see later):
28
​
29
![](browsers.png)
30
​
31
WebRTC implements the following APIs:
32
​
33
- **`MediaStream`** gets access to data streams from the user's end, like the camera and the microphone
34
- **`RTCPeerConnection`** handles communication of audio and video streaming between peers
35
- **`RTCDataChannel`**: handles communication of other kinds of data (arbitrary data)
36
​
37
With video and audio communication you'll use `MediaStream` and `RTCPeerConnection`.
38
​
39
Other kind of application, like gaming, file sharing and others rely on `RTCDataChannel`.
40
​
41
In this article I'll create an example using WebRTC to connect two remote webcams, using a [Websockets](/websockets/) server using [Node.js](/nodejs/).
42
​
43
> Tip: in your projects you'll likely use a library that abstracts away many of those details. This tutorial aims to explain the WebRTC technology, so you know what is going on under the hood.
44
​
45
## MediaStream
46
​
47
This API lets you access the camera and microphone stream using JavaScript.
48
​
49
Here is a simple example that asks you to access the video camera and plays the video in the page:
50
​
51
<p data-height="265" data-theme-id="0" data-slug-hash="rqRqpX" data-default-tab="js,result" data-user="flaviocopes" data-pen-title="WebRTC MediaStream simple example" data-preview="true" class="codepen">See the Pen <a href="https://codepen.io/flaviocopes/pen/rqRqpX/">WebRTC MediaStream simple example</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
52
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
53
​
54
We add a button to get access to the camera, then we add a `video` element, with the `autoplay` attribute.
55
​
56
We also add the [WebRTC Adapter](https://github.com/webrtchacks/adapter) which helps for cross-browser compatibility:
57
​
58
```html
59
<button id="get-access">Get access to camera</button>
60
<video autoplay></video>
61
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
62
```
63
​
64
The JS listens for a click on the button, then calls `navigator.mediaDevices.getUserMedia()` asking for the video. Then we access the name of the camera used by calling `stream.getVideoTracks()` on the result of the call to `getUserMedia()`.
65
​
66
The stream is set to be the source object for the `video` tag, so that playback can happen:
67
​
68
```js
69
document.querySelector('#get-access').addEventListener('click', async function init(e) {
70
  try {
71
    const stream = await navigator.mediaDevices.getUserMedia({
72
      video: true
73
    })
74
    document.querySelector('video').srcObject = stream
75
    document.querySelector('#get-access').setAttribute('hidden', true)
76
    setTimeout(() => { track.stop() }, 3 * 1000)
77
  } catch (error) {
78
    alert(`${error.name}`)
79
    console.error(error)
80
  }
81
})
82
```
@mikeadams1
Propose file change
Commit summary 
Update index.md
Optional extended description
Add an optional extended description…
 
© 2019 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
