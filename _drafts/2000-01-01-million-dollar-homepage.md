---
title: 17 years ago today, the Million Dollar Homepage was completed
author: Jake Lee
layout: post
image: /assets/images/2022/milliondollarhomepage.png
tags:
    - 2005
    - 2006
    - Advertising
---

When I was at school in the early 2000s, the internet was a very different place. Bizarre dotcom ideas were exploding everywhere, online shopping was taking over, and digital entrepreneur's moneymaking creativity was unbounded. One outcome of this that I strongly remember being covered in mainstream news back in 2005 was the Million Dollar Homepage.

## What was the Million Dollar Homepage?

 The concept was simple: A page with 1,000,000 pixels, $1 each, anyone can purchase blocks of them for advertising, and once they're gone they're gone.

This basic idea, simple execution, and astonishing success truly embodied the "novel idea makes thousands overnight" vibe a lot of the early internet had. There was no reason for the website to be of any value to advertisers besides the fact... it was there. There was no product, no investors, no corporate backing, just 1,000,000 pixels of unused advertising space. 

Of course, this was back when online adverts were a beautiful wild west, with gambling, dating, free software (or malware) and illegal video downloads were all fair game. The end result is a beautiful montage of mid-2000s internet, preserved in a 1000 x 1000 pixel bubble. Whilst I'd recommending visiting [the eye burning original](http://www.milliondollarhomepage.com/) for a pixel-perfect version, here's a smaller version (click to view full size):

[![million dollar homepage](/assets/images/2022/milliondollarhomepage.png)](/assets/images/2022/milliondollarhomepage.png)

So how on earth did this ~~monstrosity~~ masterpiece happen?

## What's the timeline?

* 2005-08-26: Site is launched
* 2005-08-29: First sale
* 2005-09-22: Covered on BBC
* 2005-10-26: Over half of all pixels sold
* 2006-01-01: Auction opened for final 1000 pixels
* 2006-01-10: Final pixels sold

## What's the backstory?

https://web.archive.org/web/20120311152809/http://milliondollarhomepage.com/faq.php

## Do all the links still work?

* 2017: 37% of links broken. (from Harvard: https://lil.law.harvard.edu/blog/2017/07/21/a-million-squandered-the-million-dollar-homepage-as-a-decaying-digital-artifact/)
* 2019: 40% of links broken. (from BBC: https://www.bbc.com/future/article/20190401-why-theres-so-little-left-of-the-early-internet)
* 2021: 40% of links broken, as per Internet History's investigation below:

### Overview 

In total the 1,000,000 pixels have 3,306 different adverts. Many of these are by the same websites or companies, but this is the number defined on the page.

Out of these, 143 were "pending", "reserved", or otherwise never valid URLs for one reason or another. This leaves us with 3,163 valid adverts. However, some of these are for the same domains (e.g. myspace), so we end up with 2,804 unique domains that our adverts point to.

Out of these 2,804 domains, 550 completely fail to respond or don't exist, 29 give server errors, and 531 give other errors, usually that the content is forbidden or can't be found. 

**In conclusion, 1694 of our 2804 advert domains are still alive and responding properly!**.

### Detailed results

| Result | Count | Response Code Breakdown |
| --- | --- | --- |
| 2XX Success | 1694 (60.4%) | 200 OK: 1682<br>204 No Content: 12 |
| 4XX Client Error | 531 (19.0%) | 400 Bad Request: 9<br>401 Unauthorized: 1<br>403 Forbidden: 203<br>404 Not Found: 158<br>405 Method Not Allowed: 88<br>406 Not Acceptable: 63<br>409 Conflict: 1<br>410 Gone: 1<br>412 Precondition Failed: 5<br>429 Too Many Requests: 2 |
| 5XX Server Error | 29 (1.0%) | 500 Internal Server Error: 12<br>501 Not Implemented: 1<br>502 Bad Gateway: 2<br>503 Service Unavailable: 11<br>521: 1<br>530: 1<br>999: 1 |
| Timed out / unreachable | 550 (19.6%) | |

### HTTPS

Interestingly, only 8 of these domains are HTTPS addresses on the site, whereas now almost all sites use it by default. 

I had a theory that many of the errors above might be due to HTTPS redirects not working properly. To test this, I changed the list of 2,804 domains to all use HTTPS by default, and ran my checker again. 

I was wrong however, and the 2,257 / 2,804 domains that could at least be connected to enough to throw an error dropped to a rather awful 1,498 / 2,804. Further investigation showed that this was likely due to my tool using an outdated HTTPS (technically SSL) protocol however, with the failed sites consisting of a mixture of very outdated (doesn't support HTTPS) to very up to date (only supports modern HTTPS).

## Have there been sequels?

Mention failed billion dollar etc, mention /r/place

## For programming post

How calculated:
* Grab source clickmap
* Replace pretext `^.*?(href=")`
* Replace posttext `(" title).*$`
* Sort ascending `Ctrl+P and type the greater than sign ( > ). Next type sort and choose Sort Lines Ascending or choose the Descending option.`
* Skim through, remove any immediately broken / reserved etc
* Search for "delete duplicate"
* To check domains https://www.ilovefreesoftware.com/26/programming/how-to-bulk-check-http-status-codes-for-urls-from-command-line.html
    * vl domains.txt --debug > domain-status.txt
    * 10m to process
* Sort ascending again
* Search [400] etc
