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

## What happened to StumbleUpon?

- Misc info: https://www.theverge.com/2012/8/1/3207443/stumbleupon-struggles-relevant-social-traffic
- Google Trends

## Extracting StumbleUpon content

- Link to programming article

## Analysing extracted data

### User analysis

As with any social media platform, StumbleUpon had "powerusers" who would frequently submit popular links. By using the following Python code to count submissions per author, then find the most frequently appearing (and from which course), we can get an estimate of the most influential users.

We also need to remove "Unavailable" and "StumbleUpon" as they are typically used for sponsored posts or those where the user's information wasn't present for whatever reason (perhaps privacy?).

```py
df = pd.read_csv('data-parsed/parsed-cleaned.csv')
df_filtered = df[~df['user_name'].isin(['Unavailable', 'StumbleUpon'])]
user_name_counts = df_filtered.groupby('user_name').size().reset_index(name='count')
top_20_users = user_name_counts.sort_values(by='count', ascending=False).head(20)
def most_frequent_source_with_count(user):
    user_sources = df_filtered[df_filtered['user_name'] == user]['source']
    most_frequent_source = user_sources.mode()[0]
    count = user_sources.value_counts().loc[most_frequent_source]
    return f"{most_frequent_source} ({count})"
top_20_users['most_frequent_source'] = top_20_users['user_name'].apply(most_frequent_source_with_count)
print(top_20_users.to_markdown(index=False))
```

#### Data

| Username        | # Submissions | Most frequent topic   |
| :-------------- | ------------: | :-------------------- |
| barryr666       |            73 | science (9)           |
| bart-gatsby     |            43 | graphic-design (8)    |
| yobaba          |            26 | politics (11)         |
| thewhizzer      |            26 | internet (3)          |
| Crnii           |            25 | bizarre (5)           |
| RiggyRiggs      |            25 | videos (12)           |
| bec-hi          |            18 | music (3)             |
| charistsevis    |            18 | drawing (5)           |
| smackinthecrack |            18 | bizarre (10)          |
| ElDave          |            17 | computers (4)         |
| Suzumiya-Haruhi |            16 | toprated (4)          |
| hiskeyd         |            16 | bizarre (11)          |
| Brukhar         |            15 | computer-graphics (9) |
| Serinadruid     |            15 | animation (2)         |
| ManiacMegan     |            15 | movies (4)            |
| lekahe          |            14 | graphic-design (3)    |
| saboma          |            14 | arts (2)              |
| ToeTagJaneDoe   |            13 | toprated (4)          |
| drdoalot714     |            13 | arts (2)              |
| bhartzer        |            12 | toprated (11)         |

#### Analysis

It's worth noting that only analysing the topic-specific pages (excluding top rated) returns slightly different results, but most of the top 5 are the same (including the top 2) so they're similar enough.

From the data, we can see "barryr666" is miles ahead of anyone else, and "bart-gatsby" is also far ahead of 3rd place. Of course, this analysis only covers the data available in Wayback Machine archives, so it's possible these users just coincidentally posted shortly before backups were taken! Given the multi-year span of the data however, this seems unlikely.

"barryr666" is notable for being a generalist, and having many popular posts in almost all categories. This contrasts with "smackinthecrack" and "hiskeyd", who clearly mostly submitted bizarre links.

Whilst I did analyse the first and last posts from these users, perhaps unsurprisingly they were mostly active throughout the reporting period (2009-2012). A particularly notable exception is "bart-gatsby", who despite having the 2nd most popular submissions, was only seen between October 2009 and December 2010!

### Topic analysis

When the data was extracted, the "source" was included. Whilst a large portion of the data is from the "top rated" page, there's 4.2k links from specific topic pages!

This can be used to get an estimate for how popular these categories were. Before getting into the data, it's important to highlight the "count" is only how many unique links were _available_ in the backup, not how many links of that category were submitted. Additionally, the average uses median to avoid outliers.

These were obtained by analysing the `parsed-nontoprated.csv` using pandas with this Python code (replacing `view_count` with `review_count` for comments):

```py
df = pd.read_csv('data-parsed/parsed-nontoprated.csv')
view_count_stats = df.groupby('source')['view_count'].agg(['count', 'median', 'max'])
print(view_count_stats.to_markdown(floatfmt=".0f"))
```

#### Data

| Topic             | # results | Average views | Max views | Average comments | Max comments |
| :---------------- | --------: | ------------: | --------: | ---------------: | -----------: |
| animation         |        94 |         99368 |   1187855 |               20 |          457 |
| arts              |       164 |        279054 |   4411488 |               46 |         2564 |
| bizarre           |       176 |         38538 |    567355 |               10 |           92 |
| books             |        73 |        167291 |   1300010 |               25 |          376 |
| business          |       124 |         16323 |    213283 |               10 |          144 |
| cats              |       132 |         34343 |    240907 |                7 |          184 |
| computer-graphics |        63 |         72276 |    376401 |               18 |          170 |
| computers         |       190 |         36966 |   1207375 |               12 |          329 |
| drawing           |       108 |        101184 |   1412303 |               16 |          245 |
| food              |        71 |         62819 |    496477 |               33 |          327 |
| fun               |       136 |         11464 |    943193 |                7 |          327 |
| graphic-design    |       171 |         38871 |    829360 |                9 |           92 |
| health            |       130 |         14330 |   1626138 |                8 |          183 |
| humor             |       243 |         59496 |   2072391 |               12 |          319 |
| internet          |       173 |         41966 |    625869 |               15 |          187 |
| internet-tools    |        64 |        167245 |    581672 |               39 |          418 |
| lifestyle         |       152 |         32795 |   1948169 |               12 |         1102 |
| movies            |       188 |        140309 |   1683522 |               24 |          179 |
| music             |       151 |        106151 |   2699084 |               20 |          620 |
| news              |       148 |         21418 |    253559 |               12 |          275 |
| online-games      |        81 |         96886 |    806271 |               19 |          192 |
| photography       |       139 |         37714 |   1252090 |               14 |          265 |
| politics          |       170 |          5438 |    284892 |                6 |          170 |
| psychology        |       102 |         64021 |   1041421 |               16 |          286 |
| satire            |       156 |         47578 |    574336 |               13 |          167 |
| science           |       132 |         95410 |   1166009 |               22 |          399 |
| self-improvement  |        80 |        110878 |    643471 |               22 |          146 |
| sports            |       103 |         14500 |    863036 |                4 |           50 |
| technology        |       149 |         48063 |   1198425 |                9 |          271 |
| travel            |       100 |         75958 |   1288878 |               17 |          289 |
| videos            |       250 |          1355 |   2561293 |                2 |          713 |

#### Analysis

There's some interesting statistics! At a glance, "arts" has the highest average _and_ maximum views, and average _and_ maximum comments, clearly showing it was a key category.

This was pretty surprising, as I assumed topics like "videos" and "humor" would be popular, essentially what social media is full of today. However, videos is actually the _least_ viewed category by far, as well as the least commented! This is despite having the 3rd highest max comments, presumably implying this category is dominated by a few outliers.

Within "arts", the most popular category, the most viewed and most commented link are the same thing! It's a link "sidewalk chalk guy", going to the now defunct link: <https://gprime.net/images/sidewalkchalkguy/>. Whilst there isn't a backup from the day it was submitted, the Internet Archive does have a backup [from a few days beforehand](https://web.archive.org/web/20120120130651/https://gprime.net/images/sidewalkchalkguy/). I'm a little baffled what could have caused over 2,500 comments here, although it is impressive art! My best guess is the StumbleUpon link itself went "viral", being shared elsewhere on the internet.

The lack of comments on sports links (2nd lowest average, lowest maximum by far) is unexpected initially, but perhaps reflects the typically more technology-focused audience of StumbleUpon.

Overall these results really highlight how different the internet was even 15 years ago. Whilst StumbleUpon did have less of a commenting culture than sites like Reddit today (due to many users just using the toolbar, not the StumbleUpon site itself), the extremely low numbers of comments are still surprising. It's hard to imagine the most viewed video (yet another [art based link](https://www.youtube.com/watch?v=dY1Lr-yGtd8)) on any other platform having 2.5 million views without even bothering to give the submission a title, it's just the URL itself!

### Domain analysis

By taking the root domain of each link, and removing inconsistent prefixes like `www.`, we can get an analysis of the highest average views per domain, and the most frequently submitted domains. We also need to ensure links are _unique_, since the same link can (and frequently is) submitted multiple times.

Of course, as always this only includes links that ended up on the "popular" pages, so it's entirely possible other domains had thousands of unpopular submissions! I also only included domains that had > 5 submissions, as domains with 2-3 submissions are too small a sample size.

The code to obtain this data is:

```py
df = pd.read_csv('data-parsed/parsed-cleaned.csv')
df_unique = df.drop_duplicates(subset='url')
df_unique['domain'] = df_unique['url'].apply(lambda url: urlparse(url).netloc.replace('www.', ''))

domain_stats = df_unique.groupby('domain')['view_count'].agg(['count', 'median']).reset_index()

domain_stats_filtered = domain_stats[domain_stats['count'] > 5]

highest_avg_view_count = domain_stats_filtered.sort_values(by='median', ascending=False).head(10)
print(highest_avg_view_count.to_markdown(index=False, floatfmt=".0f"))

most_frequent_domains = domain_stats.sort_values(by='count', ascending=False).head(10)
print(most_frequent_domains.to_markdown(index=False, floatfmt=".0f"))
```

#### Highest average views

##### Data

| Domain            | Count | Median views |
| :---------------- | ----: | -----------: |
| zadan.nl          |     6 |       389406 |
| marcandangel.com  |     6 |       313002 |
| wonderfl.net      |     6 |       309949 |
| mymodernmet.com   |    16 |       191400 |
| newgrounds.com    |     6 |       180574 |
| techeblog.com     |     6 |       142934 |
| lifehacker.com    |     9 |       132097 |
| listal.com        |    12 |       128312 |
| twistedsifter.com |     6 |       125023 |
| yankodesign.com   |    11 |       121044 |

##### Analysis

Topping the list are sites focused on generic images (e.g. zadan.nl's "Ninja Squirrel takes it all"), listicles (e.g. marcandangel.com's "50 Questions That Will Free Your Mind"), and flash games (e.g. wonderfl.net's "\[Stardust\] KiraKira Waypoints").

Most of the top sites are pretty typical for the era (I remember Newgrounds and Lifehacker!), but I was surprised to see "mymodernmet.com" having so many submissions, many of which are popular. The site seems focused on arts, with topics such as "Van Goghs Paintings Get Tilt-Shifted". Higher brow entertainment than I expected!

#### Most frequently submitted

##### Data

| Domain             | Count | Median views |
| :----------------- | ----: | -----------: |
| youtube.com        |   426 |        13512 |
| buzzfeed.com       |    45 |        27898 |
| flickr.com         |    34 |        31128 |
| gizmodo.com        |    30 |        47466 |
| boingboing.net     |    26 |        28746 |
| telegraph.co.uk    |    25 |        14897 |
| metacafe.com       |    24 |        37656 |
| dailymail.co.uk    |    23 |        31550 |
| funnyjunk.com      |    21 |        20643 |
| huffingtonpost.com |    19 |         9873 |

##### Analysis

Even 15 years ago, YouTube's dominance on entertainment was absurd. With almost 10x as many popular submissions as the 2nd place Buzzfeed, the overwhelming volume means the lower median is expected. Interestingly, 4 of these sites (YouTube, Flickr, Metacafe, Funnyjunk) are primarily driven by _user_ submissions, with the remaining 6 being journalism (of varying standards admittedly).

This perhaps makes sense, as users will be motivated to submit their own videos (YouTube / Metacafe), images (Flickr) and memes (Funnyjunk), whilst news is always popular content. This is especially true for online-focused journalism like Buzzfeed, Gizmodo, and BoingBoing.

### Link analysis

Using the same technique as the [Million Dollar Homepage article](/million-dollar-homepage/#how-were-the-domains-checked), we can check how many of these submitted URLs are still valid.

Unlike that project, where the domains were at least vaguely intended to persist, submissions to StumbleUpon did not have that intention. Additionally, many of these "funny picture" or listicle sites fold after a few years. Counteracting that however is all the YouTube links, which by default will persist forever.

Once [all the URLs](https://github.com/JakeSteam/StumbleUpon-extract/blob/main/data-parsed/parsed-cleaned-urlsonly.csv) have been [checked for their current status](https://github.com/JakeSteam/StumbleUpon-extract/blob/main/parsed-cleaned-urlschecked.txt), we get the following results.

#### Data

Note that there's a few non-standard status codes returned (e.g. 556, 523), plus pages that to load entirely (671 of them!), these have all been included in the counter for 5XX. Similarly, errors like 409 or 421 are included in the count for 4XX.

| Status code |   Meaning    | Count |
| :---------: | :----------: | :---: |
|     200     |  Successful  | 1657  |
|     4XX     |  Not found   | 2290  |
|     5XX     | Server error |  765  |

#### Analysis

Most of these links are broken now!

These numbers are also inflated by YouTube returning a 200, even when the video itself is actually unavailable. Given how many sites have a similar scenario, it's even more concerning that over 60% of links are completely broken.

Of course, it's likely that the Wayback Machine managed to grab many of these (since they were linked to by pages it has archived), but the link rot in under 15 years is pretty high.

## Conclusion
