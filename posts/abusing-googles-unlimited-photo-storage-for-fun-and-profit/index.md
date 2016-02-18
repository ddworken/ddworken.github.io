<!-- 
.. title: (Ab)using Google’s Unlimited Photo Storage for Fun and Profit
.. slug: abusing-googles-unlimited-photo-storage-for-fun-and-profit
.. date: 2015-08-06 11:14:20 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

#'Unlimited' Storage
Google has recently made unlimited free storage available on google photos. At first glance this seems truly amazing (and ripe for abuse). The one caveat to this claim is that all photos uploaded to Google Photos are compressed with lossy compression. This means that any photos uploaded to Google Photos are automatically compressed thereby loosing some detail. 

At first glance, it would appear that this would prevent people from abusing their service since it would make it impossible to upload arbitrary files to their servers since lossy compression would destroy any files uploaded. This also means that many types of steganography would fail if one were to try to store arbitrary data on Google Photos. 

#The Workaround
By uploading images of text to Google Photos, we are able to upload arbitrary data. This is because whatever type of lossy image compression Google is using will leave all text in photos intact (as would be expected by the users of Google Photos). 

So this means that in order to store arbitray data on Google Photos, all you have to do is:

1. Base64 encode a file. 
2. Create a series of images containing the above text (Google Photos only allows images under 16 megapixels)
3. Upload the images

And conversely, when retrieving the data from Google Photos, all that has to be done is:

1. Run image recognition on each photo to get the text.
2. Base64 decode the text
3. Concatenate the base64 decoded text from each image into one big file

#The Code 

I have written a custom python program to implement the above. The code for it is [here](https://github.com/ddworken/GooglePhotosStorage). To use it import is as a library and call getImages('fileToBackup') and it will generate the photos for you to upload to Google Photos. To recover the file, download the images from Google Photos into your current dir and call getMessage('fileToBackup'). 

#So What?

There are two main uses of this. The first use would be to use this to scheme to upload images to Google Photos thereby preventing Google from running their lossy compression algorithm on your photos. 

The other use of this would be as a true back up service. Since one can upload arbitray files to Google Photos, one can use this as a long term backup solution. One could even write a FUSE filesystem so as to allow for Google Photos to be mounted onto a computer as an external hard drive.
