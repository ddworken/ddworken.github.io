<!-- 
.. title: Website Hosting with KBFS
.. slug: website-hosting-with-kbfs
.. date: 2016-02-18 17:56:33 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

KBFS is great not only for storing and signing files, but also for hosting a signed mirror of a website. By default keybase.pub is configured to look for a index.html or a index.md. So to mirror your static website in KBFS, just copy it all over into a folder in your public directory. For example, my [blog](https://dworken.keybase.pub/blog/) and my [website](https://dworken.keybase.pub/website/index.html) are both mirrored in KBFS. 

To set this up with Nikola (which I use to host my blog), you just need to modify ```conf.py``` to set up the ```nikola deploy``` command. To do so: 

```
DEPLOY_COMMANDS = {
     'default': [
         "nikola github_deploy",
         "nohup cp -a blog /keybase/public/dworken/ &",
     ]
 }
```

So now when I run nikola deploy it will automatically deploy to both Github Pages ([ddworken.github.io](https://ddworken.github.io)) and KBFS ([dworken.keybase.pub/blog](https://dworken.keybase.pub/blog/index.html)). 
