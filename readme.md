# Remote Control Car

The car is assumed to be controlled by client-server protocol.

## Objectives

 - Connection-independent protocol: machines should not care of connection type, whether it's Bluetooth, WiFi or Mobile Network
 - Automatic connection through the list of available options. User should not spend time on choosing a remote node between launches
 - Flexible message protocol. Communication should be implemented in such a way that it would be easy to adopt the project for any kind of remote control (e.g. RC helicopter, ship etc.)
 - Video stream (only output). Optionally, user should be able to interact with environment using video capture 
 - Audio stream (input/output)
 - Text-to-speech as a part of Audio input
 - Desktop GUI to control
 - User-friendly client device: plug to charge, switch on to drive

## Requirements

Here are requirements to implement the project completely. However, one may use the parts of the project for personal purposes.
*(The lists are not final).
Server side:*
 - Python 3.8+

*Client side:*
 - Raspberry Pi (3b+ is used for the specific implementation)
 - Camera Module (v.1.3 is used for the specific implementation)
 - Python 3.8+
 - [Optional] USB-stick modem to connect through mobile network

## TODO:

Here is the list of challenges we'll potentially have to solve:

 - Set up a lightweight OS onto Raspberry Pi
 - Provide ssh/remote desktop connection
 - How to launch specific script on startup (to provide user-friendliness)
 - Autoscan of available networks on startup
 - How to capture and play audio
 - How to capture video (see notes below)
 - Develop a connection-independent message protocol
 - USB stick internet connection. How it should be handled to work in a PlugNPlay way

**NOTE: This is a hobby project. Please, do not expect a perfect code quality and engineering decisions**

### Notes/ideas on video capturing:

At the moment we do have several opportunities:
- picamera module
- raspivid h264 On the Computer, one can stream with VLC: vlc tcp/h264://192.168.66.154:3333
- opencv capture
- https://github.com/EbenKouao/pi-camera-stream-flask/blob/master/camera.py
- capturing video like Streamer, I chose to go down a different path and work to utilize FFmpeg. ffmpeg -ar 44100 -ac 2 -f alsa -i hw:1,0 -f v4l2 -codec:v h264 -framerate 30 -video_size 1920x1080 -itsoffset 0.5 -i /dev/video0 -copyinkf -codec:v copy -codec:a aac -ab 128k -g 10 -f flv rtmp://a.rtmp.youtube.com/live2/(Your Stream Key Here)
-Official V4L2 Driver. https://raspberrypi.stackexchange.com/questions/23182/how-to-stream-video-from-raspberry-pi-camera-and-watch-it-live
- Take a look onto how the data is streamed from drone cameras

 
