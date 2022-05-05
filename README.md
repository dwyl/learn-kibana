# learn *kibana*

![kibana-logo](https://cloud.githubusercontent.com/assets/194400/10302959/2fb98d1a-6c08-11e5-9a64-69594fff14da.png)

[**Kibana**](https://www.elastic.co/products/kibana) is ***awesome***!
If you don't *agree*, we *can't* be friends anymore.
Sorry.  
But seriously, if you've never *heard* of Kibana,
you're in the *right place*, *prepare* for "***wow***"!

In the next 30 mins you will learn how use Kibana to visualize your data and unlock the insight with real-time updates!

## Why?

Having data and not *analysing* it for *insights* is like
paying for a *gym* membership and not using it.
The *potential* is locked away while you sit on the couch
eating cookies and crisps and drinking cola...

Getting *insights* from *data* is the difference between
success and mediocirty.


Even the smallest amount of data can yield insights
when displayed visually; you don't *need* to have "*Big Data*" ...

## What?

I ***highly recommend*** watching the "***What’s New in Kibana 4***" video
on the elastic website: https://www.elastic.co/webinars/whats-new-in-kibana-4
(*tip: use a fake email to register to avoid spam!*)

## How?

By the end of this tutorial you will have something resembling:

![kibana-4-screenshot](https://cloud.githubusercontent.com/assets/194400/10303313/c27c089c-6c0a-11e5-92b9-c9b702b1ed39.png)

### Installation

There are a few tutorials for how to intall ElasticSearch and Kibana
floating around the Internet.

> We recommend you use [***Vagrant***](https://github.com/dwyl/learn-vagrant)
in which case you can run:

```sh
git clone https://github.com/nelsonic/learn-kibana.git
cd learn-kibana
vagrant up
```
That's *it*! After a few minutes you will have a working Kibana instance!
access your Kibana by visiting: http://localhost:5601/ in your browser.

You should *epect* to see something like this:

![kibana running on localhost](https://cloud.githubusercontent.com/assets/194400/10338354/822377dc-6cfd-11e5-8dce-2e3ed7d8f749.png)

It will automatically show the setting page because it has not been configured
to show any data... (*we'll do that next!*)



## Background Reading

+ install (*Just*) Elastic + Kibana on Linux: https://www.unixmen.com/install-kibana-ubuntu-14-04/
+ How to install Logstash + Kibana 4 on Digital Ocean:
https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-4-on-ubuntu-14-04
