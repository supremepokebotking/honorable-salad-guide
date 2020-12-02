# honorable-salad-guide
Instructions on container locations and installers.

Try out the World's Strongest Pokemon Ai.

the docker compose has two containers in it. You can get an idea of what's inside by looking at these repos.
Keep in mind the Video capture repo is incomplete since the container has secret optimizations.
Honorable Salad Ai Tensorflow:  https://github.com/supremepokebotking/public-honorable-salad-ai-tensorflow
Video Capture Container Sample Structure:  https://github.com/supremepokebotking/public-sword-capture

Current Discord link. https://discord.gg/wx6tnUPRWx
Warning: Very little hand holding. You must already be somewhat competent at this.

Suggested Hardware:
- Raspberry Pi or Jetson nano
- Nintendo Switch (Not Lite)
- Pokemon Sword/Shield
- Arduino Teensy2.0
- HDMI Splitter
- Hdmi USB Capture device
- Serial USB Adapter example: (https://cdn-shop.adafruit.com/1200x900/954-02.jpg)

Using Jetson Base Image 2GB. / Raspberry Pi 4gb Noobs
Install VLC to verify video feed
sudo apt-get install vlc

Open vlc and verify you can view video feed. Example /dev/video0

Install docker-compose.
Jetson doesnt ship with docker compose.
https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-jetson-nano-4gb-2gb-in-2-simple-steps-1f4i

Raspberry pi docker/docker compose
https://devdojo.com/bobbyiliev/how-to-install-docker-and-docker-compose-on-raspberry-pi

Arduino
If you have Arduino Teensy 2.0+
Flash it with Joystick_atmega32u4.hex

Arduino: https://www.arduino.cc/en/software
Teensyduino: https://www.pjrc.com/teensy/teensyduino.html

Useful docker commands. Check Usb Serial ports
sudo docker run --privileged -v /dev:/dev supremepokebotking/public-sword-capture-arm64 available_serial.py

['/dev/ttyUSB0', '/dev/ttyGS0', '/dev/ttyTHS2', '/dev/ttyTHS1', '/dev/ttyS0']

Hop inside container and use webcam test. Note Jetson uses gstreamer so use gstreamer option.
If device not set correctly, use nano to edit file. No output should be given from the script. It just shouldnt crash if loads video capture device.

# Hop in container
sudo docker run -it --entrypoint bash --privileged -v /dev:/dev supremepokebotking/public-sword-capture-arm64

#edit web cam file to use correct
nano webcam_test.py

You can change this to use correct device
cap = cv2.VideoCapture("/dev/video0") # check this

if using gstreamer, you can use this line instead.
#cap = open_cam_usb("0")

Make sure one of those lines are commented out.

On your host machine download or create your config file.
You can use the rpi file or jetson file as the template. The big difference is the jetson has gstreamer on by default.

Update the serial port and video device.
Also make your device readable and writable.
chmod 777 /dev/ttyUSB0 # or whatever yours is.



Usage:
Edit your config file to use the correct video, correct serial
Then select the battle type of wild or network depending on battle type.

If model crashes crashes locally, use remote server for model or switch to rando for ai style.
If using docker-compose, it is as simple as: docker-compose up

