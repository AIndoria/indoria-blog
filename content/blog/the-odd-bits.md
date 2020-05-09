---
title: "The Odd Bits"
date: 2020-04-22T01:25:30-07:00
draft: false
---

So, continuing on from [yesterday's dilemma](https://blog.aindoria.com/blog/figuring-out-covid/), here's where we stand. I essentially went with the second route, which included me using a curl command to download the file, and using git to upload it to one of [my repos](https://github.com/AIndoria/COVID-19-data/). The interesting issue which annoyed me was that the file name changed every day, so I had to do a bit of tinkering, and it kept giving me weird errors despite everything seeming to be perfectly written.

Turns out, it isn't me, but it's you, fish. The command works perfectly in bash, but any derivatives of it laugh at you in fish.

    curl https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/$(date +%m-%d-%Y).csv -o covid_current.csv

which gives me the date in mm-dd-yyyy format, which is the only second best format after the yyyymmdd format. Suck it, Redcoats.

Now, all that was needed was to automate it. We come to a trusty cronjob for it. I created a bash script which did this.

    #!/bin/bash

    cd /home/TRAIANVS/COVID-19-data
    curl https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/$(date +%m-%d-%Y).csv -o covid_current.csv
    git add .
    git commit -m "Update Current COVID-19 numbers"
    git push

and it was done. For the cronjob, I set a time for 20:00 as the Johns Hopkins data usually gets updated around 19-19:30 MST anyway. This was the sole line in my cron file:

    00 20 * * * /home/TRAIANVS/cronfile.sh

---

**Issue: The mapping application only accepts "FIPS-CODE" column name as an index for the FIPS county data, and JHU csv file has it as "FIPS."**

Should be interesting, but I'm sure I can figure this out and modify it in the bash script before pushing it to my repo. For now, let's just edit it in real time just to see if it even works.

---

**Preliminary result**

Well, at least it works. Step 1 complete. Now to add other types of data. I'll...get back to you later.

![US COVID-19 MAP](https://c-v.sh/WgBfLOXfwGCS#c)
