# terrible-hls-usb-livestreaming-server
High latency usb camera implementation of a hls live streaming server.

#installation instructions

These steps are only for debian based distributions, but with some common sense could be adapted for other linux distros. 

1.) Clone the repository git clone

2.) Create virtual environment: python3 -m venv env

3.) Find your usb camera device: gst-device-monitor-1.0 | grep /dev/
 
You will get output results like the following. Choose either of the values on the right side of the video that 
do not have the string "v4l2" in the value. 
( 
  api.v4l2.path = /dev/video0
  object.path = v4l2:/dev/video0
  api.v4l2.path = /dev/video2
  object.path = v4l2:/dev/video2
) 

For example my camera path is "/dev/video2"

4.) Type your relative filepath from your home to cloned repo directory in a place where you can easily copy and paste it. 
   For example mine is /home/danie/Cabinet/Projects/terrible-hls-usb-livestreaming-server
   Use it to create two other filepaths: 
      One where you append "/video-files/playlist.m3u8". For example: /home/danie/Cabinet/Projects/terrible-hls-usb-livestreaming-server/video-files/playlist.m3u8
      One where you append "/video-files/segment_%05d.ts". For example /home/daniel/Cabinet/Projects/terrible-hls-usb-livestreaming-server/video-files/segment_%05d.ts

5.) In the directory of the git repository, after editing the filepaths with the ones you generated in the previous step, run the command below: 
   
gst-launch-1.0 v4l2src device="/dev/video0" ! videoconvert ! \x264enc tune=zerolatency ! mpegtsmux ! \hlssink playlist-location=/home/daniel/Cabinet/Projects/terrible-hls-usb-livestreaming-server/video-files/playlist.m3u8 location=/home/daniel/Cabinet/Projects/terrible-hls-usb-livestreaming-server/video-files/segment_%05d.ts target-duration=1 max-files=4

Note: More commands will follow. If you are unable to use create multiple terminal tabs add an & after the command.

6.) Open a new terminal tab, OR gracefully exit the previous commands grip on the terminal via ctrl+ d. 





