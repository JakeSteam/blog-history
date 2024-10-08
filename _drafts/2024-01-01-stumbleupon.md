---
title: StumbleUpon export
author: Jake Lee
layout: post
image: /assets/images/2023/
tags:
  -
---

Top rated: https://web.archive.org/web/20110301003451/http://www.stumbleupon.com/discover/toprated

322 captures, plus scraping all the "topics". Each capture has 10x links, each with:

- title, URL, ID, view count (real in source), review count.

Ideally would scrape all possible data, with useful extracts:

- Which users frontpaged most often (over time)?
- Which domains frontpaged most often (over time)?

The URLs could then be analysed (similar to million dollar homepage) for whether they work / 404 / domain bought out / other error.

## Programmatic access

### Scrape all

Tool already exists: https://github.com/hartator/wayback-machine-downloader

- Use -e (exact URL)
- Use -s (all snapshots)
- Use -c (concurrency)

OR one dedicated to multiple versions: https://github.com/jsvine/waybackpack

1. Full list of URLs: http://web.archive.org/cdx/search/cdx?url=http://www.stumbleupon.com/discover/toprated/
2. Build each URL from this (`id_` suffix strips out wayback): https://web.archive.org/web/20101125161218id_/http://www.stumbleupon.com/discover/toprated/
3. Download every result
4. Repeat for subpages

Can it be scraped from Google archive too?

### Analyse

Work out what analysis is wanted, use that to guide the data format

### Extra info

- Scraping tips: https://wiki.archiveteam.org/index.php?title=Restoring

## Misc SU info

https://www.theverge.com/2012/8/1/3207443/stumbleupon-struggles-relevant-social-traffic
