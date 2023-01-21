---
title: 20 years ago today, the 'Most Annoying Webpage' was launched, forcing victims to click "OK" for a few minutes
author: Jake Lee
layout: post
image: /assets/images/2023/annoying-header.png
tags:
    - 2003
    - 2004
    - 2005
    - Pranks
---

In 2003, the internet was a lot more innocent. People happily clicked suspicious looking links, browsers trusted websites implicitly, and instead of malware we had pranks and time-wasters. "Most Annoying Webpage" was one of these, taking a few precious minutes out of any victim's day. 

## What was it?

The "Most Annoying Webpage" realistically wasn't *that* annoying. It queued up 151 alerts, forcing the user to click "OK" on each one individually. Due to browsers being a bit too trusting of websites in the early internet, there was no way to change tab, dismiss all remaining alerts or any similar workaround. Additionally, as many users weren't expert computer users, many manually clicked the "OK" button.

You can view an [archived version of the site here](https://web.archive.org/web/20030402051520/http://www.mostannoyingwebpage.com/v1/) and click "Yes, I'm Sure" to begin displaying the alerts. On any modern browser they won't cause any issues, and can be dismissed by just changing tab. 

Once a victim makes their way through all the alerts, they are prompted to send their friends a link via "TAF Master", an advertising link manager (similar to adf.ly today). Considering this link was active throughout the site's lifetime, it's likely advertising revenue was the main goal of the developer. The preticked boxes for the referral form[^referral-form] give a good indicator of how much spam you'd likely receive!

[![](/assets/images/2023/annoying-spam.png)](/assets/images/2023/annoying-spam.png)

## Timeline

* **20th March 2003**: Most Annoying Webpage created and launched[^registered].
* **1st April 2003**: First Wayback Machine archive of Most Annoying Webpage, appropriately on April Fool's Day[first-archive].
* **14th April 2003**: First mention of Most Annoying Webpage online, on Slashdot[^first-mention]
* **May 2003**: Most Annoying Webpage spreads through technology forum's threads (Anandtech[^anandtech], Howard Forums[^howard-forums], Blender Artists[^blender-artists])
* **July 2003**: Most Annoying Webpage spreads through general forum's threads (Digital Photography Challenge[^dpchallenge], Airliners.net[^airliners])
* **11th July 2003**: First and only mention of Most Annoying Webpage in a (political) news site[^national-review].
* **20th March 2005**: Most Annoying Webpage enters a chain of advertising / parking services[^full-dns-records].
* Between **17th May - 14th October 2014**, Most Annoying Webpage begins hosting a german spam blog[^german-spam], and continues to this day.

[^first-mention]: [https://developers.slashdot.org/story/03/04/14/1154210/java-for-the-gameboy-advance](https://developers.slashdot.org/story/03/04/14/1154210/java-for-the-gameboy-advance)
[^first-archive]: [https://web.archive.org/web/20030401194229/http://mostannoyingwebpage.com/](https://web.archive.org/web/20030401194229/http://mostannoyingwebpage.com/)
[^registered]: March 2003 date from DNS records[^full-dns-records], exact date from [Domain IQ](https://www.domainiq.com/domain?mostannoyingwebpage.com).
[^full-dns-records]: [DNS records](/assets/images/2023/annoying-dns.png) according to [Complete DNS](https://completedns.com/dns-history/).
[^german-spam]: [http://mostannoyingwebpage.com/](http://mostannoyingwebpage.com/)
[^anandtech]: [https://forums.anandtech.com/threads/mostannoyingwebpage.1054836/](https://forums.anandtech.com/threads/mostannoyingwebpage.1054836/)
[^howard-forums]: [https://howardforums.com/showthread.php/137149-good-old-mindless-fun](https://howardforums.com/showthread.php/137149-good-old-mindless-fun)
[^blender-artists]: [https://blenderartists.org/t/weird-web-sites/305796](https://blenderartists.org/t/weird-web-sites/305796)
[^dpchallenge]: [https://www.dpchallenge.com/forum.php?action=read&FORUM_THREAD_ID=32387&page=1#352609](https://www.dpchallenge.com/forum.php?action=read&FORUM_THREAD_ID=32387&page=1#352609)
[^airliners]: [https://airliners.net/forum/viewtopic.php?t=1082967](https://airliners.net/forum/viewtopic.php?t=1082967)
[^national-review]: [https://www.nationalreview.com/corner/most-annoying-site-jonah-goldberg/](https://www.nationalreview.com/corner/most-annoying-site-jonah-goldberg/)
[^referral-form]: [https://web.archive.org/web/20040207121316/http://tafmaster-v.focalex.com/taf/1641/250646/?cookie_refresh=1&focalex_aa_f=os=,id=8dO148cOwHUuFabddZmLKQ&gatherer_id=http://www.MostAnnoyingWebpage.com](https://web.archive.org/web/20040207121316/http://tafmaster-v.focalex.com/taf/1641/250646/?cookie_refresh=1&focalex_aa_f=os=,id=8dO148cOwHUuFabddZmLKQ&gatherer_id=http://www.MostAnnoyingWebpage.com)

## Alert analysis

The site's source code is available at [annoying-source.txt](/assets/txt/annoying-source.txt), and the plaintext alerts can be viewed at [annoying-alerts.txt](/assets/txt/annoying-alerts.txt). 

### Dynamic alerts 

In the plaintext alert file, there are 2 sets of messages that I have annotated with `(DYNAMIC)`. In the original source code these are small JavaScript functions that accept input from the user (for their name and a topic suggestion) before lightly mocking them.

### Alert miscount 

Despite the creator's claim of 150 alerts, there are actually 151! This miscount seems to creep in between alerts #105 and #116:

[![](/assets/images/2023/annoying-miscount.png)](/assets/images/2023/annoying-miscount.png)

### Metadata

According to an online text analyser[^text-analyser]:

* There are **893 words**.
* The most used word is **you**, with **59 occurrences**.
* The most used phrase is **you know** with **11 occurrences**.
* The longest reused phrases are **alert after alert after alert** and **to get through 150 alerts**, both used twice.

Whilst this was perhaps obvious from reading a few dialogs, basic online automated readability tools[^readability-tools] agreed the writing was very, very simple and easy to read for almost all ages:

[![](/assets/images/2023/annoying-readability.png)](/assets/images/2023/annoying-readability.png)


[^readability-tools]: [https://readabilityformulas.com/freetests/six-readability-formulas.php](https://readabilityformulas.com/freetests/six-readability-formulas.php)
[^text-analyser]: [https://www.online-utility.org/text/analyzer.jsp](https://www.online-utility.org/text/analyzer.jsp)

## Legacy

Evidence it blocks: 
    https://bugzilla-dev.allizom.org/show_bug.cgi?id=253239
    https://bugzilla.gnome.org/show_bug.cgi?id=112636

There are still a few copies of the site available online, since it's very simple to copy the basic JavaScript & HTML. It is available on the previously popular Albino Blacksheep[^albino], as well as direct copies without referral links[^non-referral], and with[^with-referral].

[^albino]: [https://www.albinoblacksheep.com/text/#:~:text=Annoying%20Joey%20Kilaita](https://www.albinoblacksheep.com/text/#:~:text=Annoying%20Joey%20Kilaita)
[^non-referral]: [http://www.vipergc.com/annoying.html](http://www.vipergc.com/annoying.html)
[^with-referral]: [http://www.justanotherpc.com/annoyance/alerts/alerts.htm](http://www.justanotherpc.com/annoyance/alerts/alerts.htm)

## Conclusion

## Notes

### Author 

I tried to find the creator behind this site, and completely failed:

* Original DNS records have privacy protection.
* No contact details are provided, the only name in the source code is for a free-to-use code snippet.
* The referral link[^referral-link] is on the now defunct "TAFMaster", which appears to have disappeared sometime between 2011 and 2017, with very little trace. It does not appear to have had any customer lookup / database leak.

### Technical

It's unlikely the creator had much JavaScript experience. The source code shows the only non-trivial JavaScript (using text from the user) is copied from elsewhere. More tellingly, the exact same code is used both times the site asks for user feedback, even down to the variable names! Storing both the user's name and their conversation topic in `namePrompt` for no reason is unlikely to be the work of an experienced programmer.

[^referral-link]: (Dead) `http://tafmaster.com/taf/1641/250646/`

## References

