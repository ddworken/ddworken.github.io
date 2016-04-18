<!-- 
.. title: XSS in pypi (and Uber!)
.. slug: xss-in-pypi-and-uber
.. date: 2016-04-17 19:41:05 UTC-04:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Uber's bug bounty program just went public, so it is time to write up some of the vulnerabilities I found in Uber. One of the more interesting ones was an XSS in ```archive.uber.com``` due to MIME sniffing. Uber hosts a mirror of pypi (using the same software as pypi) at ```archive.uber.com/pypi/simple/```. So then the question became, is there a vulnerability here. Pypi doesn't allow package names including any of the characters we would need for a normal XSS (```"```, ```'```, ```<```, or ```>```) so we can't get an XSS via the package names. So what about the files?

When uploading a package to pypi, you simply upload a ```.tar.gz``` of all the requisite files (```setup.py```, etc). Pypi does not verify that what we upload is a valid ```.tar.gz```, instead they simply check the file signature (the first few bytes of the file) to ensure that they are correct. 

When downloading the ```.tar.gz``` from pypi, it is sent with a MIME type of ```application/octet-stream```. Since ```application/octet-stream``` is a very vague designation, browsers will automatically try to determine the type of the file. Chrome and Firefox both do so by looking the first few bytes of the file (so they will see it as a ```.tar.gz``` and open a download prompt). Internet explorer scans the first 256 bytes of the file for ```html``` and if it finds ```html``` it will interpret the file as HTML. 

So we can combine the fact that the ```.tar.gz``` files are not verified for validity and the vague MIME type to get a persistent XSS. We do so by creating a ```.tar.gz``` that contains ```<html><script>alert(0)</script></html>``` one can inject javascript into the page. This can be done simply by opening the file in any text editor and adding the text. 

The final step we have to overcome is that the normal method of uploading to pypi doesn't give us a chance to edit the ```.tar.gz```. So we build it (```python setup.py sdist```) and then upload it with Twine (```pip install twine``` to download it) by running ```twine upload dist/evil.tar.gz```. 

I uploaded it to pypi and it was then mirrored from pypi to ```archive.uber.com```. 

I reported this to pypi on March 26th and it was fixed on March 28th. 

I reported this to Uber's bug bounty on March 26th, it was triaged on the 28th, and patched on April 1st. A 750 dollar bounty was awarded on the 6th. You can see the report [here](https://hackerone.com/reports/126197). 
