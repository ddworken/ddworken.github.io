<!-- 
.. title: Building Signal Desktop In Docker (And Skipping The Line for the Beta!)
.. slug: building-signal-desktop-in-docker
.. date: 2016-02-26 23:03:54 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Be warned, Signal Desktop is in a closed beta. This program pulls from master and builds Signal Desktop so is in no way guaranteed to work or to be secure. **Use at your own risk.** 

Why? Signal Desktop is in beta and there are over 10,000 people ahead of me in line to join the beta. Open Whisper Systems wants me to invite people in order to jump ahead in line, which I'd rather not do so this is my solution.

First, make sure you have Docker installed. Then ```git clone https://github.com/ddworken/signalDesktopDocker.git```. To build Signal Desktop: ```docker build -t signal .```. 

Currently this Dockerfile is setup to build Signal Desktop then set it up to work with NW but the NW version is stateless (so you have to login every time you use it) so it is recommended to import it as a Chrome extension. To do so, run the container: ```docker run -ti --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --cidfile=temp.cid signal```. Then ```cat temp.cid``` to get the ID of the container. Then we need to copy the extension so ```docker cp [Container ID]:/SignalDesktop.zip ./```. Then unzip SignalDesktop.zip into a folder. Open ```chrome://extensions``` in Chrome and click on "Load unpacked extension..." to load the extension. 

Make sure to re-build the container periodically to keep Signal Desktop up to date. 

I uploaded a copy of Signal Desktop to my KBFS folder [here](https://keybase.pub/dworken/SignalDesktop.zip). 

To view the Dockerfile, go [here](https://github.com/ddworken/signalDesktopDocker). 

Credit to Tim Taubert for his [original post](https://timtaubert.de/blog/2016/01/build-your-own-signal-desktop/) on building Signal Desktop. 

