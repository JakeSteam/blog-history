---
title: 23 years ago today, StumbleUpon was founded. What happened to all that content?
author: Jake Lee
layout: post
image: /assets/images/2023/
tags:
  - StumbleUpon
  - Web
  - 2001
---

intro

more intro

## Timeline

- **October 2001**: StumbleUpon founded
- **February 2002**: StumbleUpon prototype released
- **June 2018**: Stumbleupon shut down
- **30th May 2007**: StumbleUpon sold to eBay for >$75m

## What was StumbleUpon?

## Extracting StumbleUpon's archived content

- Top rated: https://web.archive.org/web/20110301003451/http://www.stumbleupon.com/discover/toprated
- 322 captures, plus scraping all the "topics". Each capture has 10x links, each with:
  - title, URL, ID, username, view count (real in source), review count, source URL.

Tool already exists: https://github.com/jsvine/waybackpack

### All top rated

waybackpack ^
http://www.stumbleupon.com/discover/toprated ^
-d "/Documents/Projects/StumbleUpon-extract/toprated" ^
--from-date 20091010 ^
--to-date 20120312 ^
--user-agent "waybackpack jake@jakelee.co.uk"

### By interest

http://www.stumbleupon.com/discover/animation/
http://www.stumbleupon.com/discover/arts/
http://www.stumbleupon.com/discover/bizarre/
http://www.stumbleupon.com/discover/books/
http://www.stumbleupon.com/discover/business/
http://www.stumbleupon.com/discover/cats/
http://www.stumbleupon.com/discover/computer-graphics/
http://www.stumbleupon.com/discover/computers/
http://www.stumbleupon.com/discover/drawing/
http://www.stumbleupon.com/discover/food/
http://www.stumbleupon.com/discover/fun/
http://www.stumbleupon.com/discover/graphic-design/
http://www.stumbleupon.com/discover/health/
http://www.stumbleupon.com/discover/humor/
http://www.stumbleupon.com/discover/internet-tools/
http://www.stumbleupon.com/discover/internet/
http://www.stumbleupon.com/discover/lifestyle/
http://www.stumbleupon.com/discover/movies/
http://www.stumbleupon.com/discover/music/
http://www.stumbleupon.com/discover/news/
http://www.stumbleupon.com/discover/online-games/
http://www.stumbleupon.com/discover/photography/
http://www.stumbleupon.com/discover/politics/
http://www.stumbleupon.com/discover/psychology/
http://www.stumbleupon.com/discover/satire/
http://www.stumbleupon.com/discover/science/
http://www.stumbleupon.com/discover/self-improvement/
http://www.stumbleupon.com/discover/sports/
http://www.stumbleupon.com/discover/technology/
http://www.stumbleupon.com/discover/travel/
http://www.stumbleupon.com/discover/videos/

- Scraping tips: https://wiki.archiveteam.org/index.php?title=Restoring

## Analysing extracted links

### The data

- Information on what data is contained, link to programming blog info on _how_.
- Spreadsheet (or CSV) of raw data

### User analysis

- Extract usernames over time, see if anything interesting

### Topic analysis

- Perhaps average votes for each category over time

### Domain analysis

- Investigate which domains were popular over time

### Link analysis

Analyse links for whether they work / 404 / domain bought out / other error, plus ideas for future posts

## What happened to StumbleUpon?

- Misc info: https://www.theverge.com/2012/8/1/3207443/stumbleupon-struggles-relevant-social-traffic
- Google Trends
