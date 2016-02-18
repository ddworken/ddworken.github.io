<!-- 
.. title: pyWMATA
.. slug: pywmata
.. date: 2015-02-07 11:08:10 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

For a while now I've been wanting to make my own interface to WMATA's API. WMATA (Washington Metropolitan Area Transit Authority) has a pretty good API that allows for you to get anything from current train locations, a path between two stations on the same line, elevator/escalator/rail incidents, even an API endpoint for stations near a location. 

The one thing that is lacking is an API to go from any one station to another. Their API does have an endpoint to get a list of stations between any two given stations with the caveat that this only works if the supplied stations are on the same line. 

So I wrote my own wrapper around their API in python that implements this and much much more. 

https://github.com/ddworken/pyWMATA
