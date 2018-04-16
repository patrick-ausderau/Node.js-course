# WebRTC
  * RTC = Real Time Communications
  * [Getting started](https://www.html5rocks.com/en/tutorials/webrtc/basics/)
  * [WebRTC tutorial](https://codelabs.developers.google.com/codelabs/webrtc-web/#0)
  * [Browser support](http://iswebrtcreadyyet.com/)
  
  
#### Excercise: Create a simple videochat on localhost
  1. Write a simple express.js server to serve content over [https](https://ilkkamtk.github.io/SSSF-course/Slides/Week3/W3-4-https-passport.html)
     * create following folder structure
     ```
     -index.js
     public
       -videochat.html
        js
            -rtc.js
     ```
     
     * serve public folder `app.use(express.static('public'));`
      
      videochat.html:
      ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>WebRTC example</title>
            <style>
                video {
                    height: 150px;
                }
            </style>
        </head>
        <body>
            <video id="localVideo" autoplay></video>
            <button type="button" id="btnMakeCall">Make Call</button>
            <script src="js/rtc.js"></script>
        </body>
        </html>
      ```
      rtc.js:
      ```javascript
          'use strict';
        
          const constraints = {audio: true, video: true};       
          navigator.mediaDevices.getUserMedia(constraints).then(mediaStream => {
            const video = document.querySelector('video');
            video.srcObject = mediaStream;
          }).catch(err => {
            console.log(err.name + ': ' + err.message);
          });
      ```
  1. Start server, open `https://localhost:3000/videochat.html`
     * You should see live video from your webcam
     
  1. Install socket.io
     * add socket.io server to index.js and socket.io client to videochat.html and rtc.js
     * note that you are using _https_
     * test connection: 
        ```javascript
        socket.on('connect', () => {
          console.log('socket.io connected!');
        });

        ```
     
  1. Add another `<video>` element to HTML for remote video.
  
  1. Start a signaling service with socket.io to broadcast call events between chatters:
        1. Now you should have videochat.html open in two browser windows/tabs 
        1. When user clicks 'Make call', emit message 'call' with 'hello' (or smthn) as value to the server
        1. Server receives 'call' and broadcasts the message to all clients except sender. Log 'call' value to console
        1. Client receives broadcasted 'call' and emits message 'answer' with value 'call answered' to all clients except sender. Log the answer value to console.
        1. At this point when 'Make call' is clicked in the first window, the second window logs 'hello' (or smthn) to the console, then 'call answered' is logged in the first browser window.
    
  1. Start RTC communications:
        1. In rtc.js initialize peer connection: `const caller = new RTCPeerConnection();`
        1. Add video stream to the peer connection after the videostream is added to `<video>` element: `caller.addStream(mediaStream);`
        1. Prepare `<video>` element for remote stream:
            ```javascript
            //onaddstream handler to receive remote feed and show in remoteview video element
            caller.onaddstream = evt => {
              console.log('onaddstream called');
              document.querySelector('#someID').srcObject = evt.stream;
            };
            ```
        1. Start call with [createOffer()](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/createOffer)
            * you already started a function in 5.ii. Continue that.
            * when promise is successful add local description to peer connection: `caller.setLocalDescription(new RTCSessionDescription(returnValueFromPromise));`  and then send the 'call message' which you did in 5.ii. Set it's value to `JSON.stringify({'call': returnValueFromPromise})`
            * as you can see we are using socket.io to send serialized description object between peers, so in server.js resend the returnValueFromPromise to other peer: 
                ```javascript
                socket.on('call', (msg) => {
                    console.log('call routed!');
                    socket.broadcast.emit('call', msg);
                  });
                ```
        1. To answer a call continue function you started in 5.iii: `caller.setRemoteDescription(
                                                                             new RTCSessionDescription(JSON.parse(msg).call));`                                                                 
        1. Listen for ICE Candidates and send them to remote peers
              ```javascript
               caller.onicecandidate = evt => {
                       if (!evt.candidate) return;
                       console.log('onicecandidate called');
                       onIceCandidate(evt);
                     };
               //Send the ICE Candidate to the remote peer
               const onIceCandidate = (evt) => {
                 socket.emit('candidate', JSON.stringify({'candidate': evt.candidate}));
               };
              ```
        1. In server.js receive 'candidate' and broadcast it forward:
            ```javascript
            socket.on('candidate', (msg) => {
                console.log('candidate message recieved!');
                socket.broadcast.emit('candidate', msg);
              });
            ```
        1. when client recieves 'candidate'-message (socket.on(.....)), add the candidate to peer connection: `caller.addIceCandidate(new RTCIceCandidate(JSON.parse(nameOfinputObject).nameOfMessage));`
         
  1. Add STUN & TURN servers to make calls between two computers.
    * Create account to [numb](http://numb.viagenie.ca/)
    * add this to your rtc.js:
            ```javascript
            const servers = {
              'iceServers': [
                {'urls': 'stun:stun.services.mozilla.com'},
                {'urls': 'stun:stun.l.google.com:19302'},
                {
                  'urls': 'turn:numb.viagenie.ca',
                  'credential': 'password',
                  'username': 'email',
                }],
            };
            ```
    * Make the neccessary modifications to server.js (https stuff) and deploy the app to Jelastic 
      
 
  
    
#### Excercise 2: Stylise video chat
  * [Instructions](https://simplewebrtc.com/notsosimple.html)
  * You can follow the instructions but try to do your own version. Like picture in picture, add nicknames etc.
  
### Extra links
  * [TURN server installation](https://github.com/alongubkin/phonertc/wiki/Installation)
