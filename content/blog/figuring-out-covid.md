---
title: "Figuring Out Covid"
date: 2020-04-21T02:16:59-07:00
draft: true
---

# Context

It has been a few months since I have used React, and I've grown rusty. Considering that there' a quarantine, and I have nothing better to do, what else to do but to jump on the COVID-19 bandwagon and create a visualization website. I don't like the idea of creating a map from scratch (not in the mood for inventing the wheel at 2 AM on a damn Tuesday), so I tinkered around with a few and found one I liked...aaaaand it requires a datapoint. Immediately, I ran into a few issues.

**Issue: No single data source, and/or insufficient data points**

The reported COVID-19 data seems to be scattered across various Github repositories. Not all of it is up to date, and since I am solely focusing on the data for these United States, I need to have the [FIPS](https://en.wikipedia.org/wiki/FIPS_county_code) codes for the counties, parishes, and boroughs. Not all datapoints provide this, but behold, Johns Hopkins does!

But wait, we run into another issue there.

**Issue: Johns Hopkins creates a new csv file every evening around 7 PM, with a different name.**

So, Johns Hopkins data includes FIPS information for US counties, updates everyday, which is good. But then, the everyday updates are stored into their own individual files. eg. 04-20-2020.csv, 04-21-2020.csv

Huh, this would be an issue as I can't just point a single csv URL to the application.

**Possible Solution**

I do own a free tier of AWS subscription. Which means I get certain instances of virtual machines for free. What I was originally thinking was, to run a cron job on the instance, to download the JHU COVID-19 csv file, rename it to have always a consistent name, replacing any previous files since I am in no need of the data of previous x days, and

1. Serve it directly to the application, which in turn could be embedded into my own Single Page Application. _or_
2. Upload it to a repository on Github, where I could possibly use it directly for my other projects as well, and anyone else who wanted to have a source without digging into JHU git repo.

---

I'll...update after I've figured out at least one of the things.
