<!-- 
.. title: KBFS On Linux
.. slug: kbfs-on-linux
.. date: 2016-02-16 11:16:54 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

By default, the KBFS will only run on linux. This is a short guide on how to setup KBFS on Linux (tested on Ubuntu 15.10 with a BTRFS root). Note that this is unsupported and takes a little bit of work to get it to work. 

Start by making sure you have the most recent version of Keybase. Assuming you installed from the ```.deb```, run ```sudo apt-get upate``` then ```sudo apt-get install keybase```. 

So now we need to set up the filesystem for KBFS. Start by killing keybase so it doesn't mess with anything as we go: ```sudo killall keybase```. So now you need to create the ```/keybase``` folder so run ```sudo mkdir /keybase```. Then we need to change the owner of ```/keybase``` to your user (from root) so that keybase can modify this. So run ```sudo chown username:username /keybase```. Once that is done you can test it by ```cd```ing into the directory. 

So now just start the keybase daemon by running ```run_keybase```. A box will pop up asking you to unlock your device key so KBFS can run. From here you can ```cd``` into ```/keybase/``` to play around. 

Note that ```ls``` and ```cd``` have some weird behavior in this folder. Since it is a FUSE it doesn't follow all the normal specifications. For example, if you ```cd /keybase/public/``` and ```ls``` you will not see a ```dworken``` folder, but if you ```cd dworken``` you will enter my public folder. So when playing around don't expect KBFS to follow your normal expectations on how ```cd``` and ```ls``` work.
