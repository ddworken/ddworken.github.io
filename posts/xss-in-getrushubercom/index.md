<!-- 
.. title: XSS in getrush.uber.com
.. slug: xss-in-getrushubercom
.. date: 2016-04-17 18:58:50 UTC-04:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

The first vulnerability I found for Uber's bug bounty was a reflected XSS in ```getrush.uber.com```. It was caused by Uber not escaping the ```utm_campaign```, ```utm_medium```, and ```utm_source``` parameters at ```getrush.uber.com/business```. It could be exploited by injecting ```</script><script>alert(0)</script>``` into any of those parameters. 

I reported this to Uber on March 22nd, it was triaged the same day, and patched on the 23rd. A 3000 dollar bounty was awarded on April 6th. You can see the original report (including a few markdown errors...) [here](https://hackerone.com/reports/125112). 
