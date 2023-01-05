---
title: 20 years ago today, 'The Scary Maze Game' was released, a screamer game that terrified millions
author: Jake Lee
layout: post
image: /assets/images/2023/maze-header.png
tags:
    - 
---

If you're reading this and *don't* know the blue & black "scary maze game" from the mid 2000s, congratulations on escaping a horrific experience. This short "game" by Jeremy Winterrowd required moving your mouse through a maze. The difficulty increases, and inevitable failure causes a loud scream to play and Linda Blair from The Exorcist appears. It's scarier than it sounds, so consider this post me getting revenge on it!

Before I dive into how the game works, here's some helpful links:

* If you'd like to download the game to play yourself, [here's a link](/assets/other/scary-maze-game.swf). Remember it's intentionally a scary game! There's a few ways to play SWF files, I used JPEXS decompiler[^jpexs]. 
* If you'd like more of an overview, [Videogaming wiki has a summary](https://videogaming.fandom.com/wiki/The_Maze_(Winterrowd)).
* If you'd like to see more reaction videos, [KnowYourMeme has lots](https://knowyourmeme.com/memes/scary-maze-game).

## Timeline

Like many early viral games / sites from the early 2000s, the timeline of "The Scary Maze Game" is very hard to determine with any certainty. The release date was either 2003[^2003] or 2004[^2004], but it didn't achieve much success until 2006-2007 when reaction videos on YouTube and other sites helped it spread extremely quickly.

Using archive.org, we can at least determine the following:
* **January 2006**: "scary maze game" starts being searched Googled a non-negligible amount (see trend chart below).
* **8th April 2006**: The maze is first visible on the creator's site[^first-visible].
* **7th July 2007**: "Scary Maze Game" is uploaded on YouTube, a simple playthrough that eventually amasses >48m views[^youtube] (warning: jumpscare).
* **8th June 2008**: "Scary Maze Game (official version)" is uploaded on YouTube, one of the first reaction videos that amasses >43m views[^youtube2] (warning: jumpscare).
* **30th October 2010**: "Scary Maze Game" is used / parodied on Saturday Night Live, albeit with the copyrighted image replaced[^snl].

[![the maze game popularity trend](/assets/images/2023/maze-trend-740w.png)](/assets/images/2023/maze-trend.png)
*Interest over time for "scary maze game", from Google Trends[^trends].*

[^2003]: [https://knowyourmeme.com/memes/scary-maze-game#fn5:~:text=Jeremy%20Winterrowd%20in-,2003,-.%20Upon%20completion%20of](https://knowyourmeme.com/memes/scary-maze-game#fn5:~:text=Jeremy%20Winterrowd%20in-,2003,-.%20Upon%20completion%20of)
[^2004]: [https://videogaming.fandom.com/wiki/The_Maze_(Winterrowd)#:~:text=Winterrowd%20in%20October-,2004,-%2C%20which%20was%20later](https://videogaming.fandom.com/wiki/The_Maze_(Winterrowd)#:~:text=Winterrowd%20in%20October-,2004,-%2C%20which%20was%20later)
[^first-visible]: [https://web.archive.org/web/20060408211659/http://www.winterrowd.com/maze/](https://web.archive.org/web/20060408211659/http://www.winterrowd.com/maze/)
[^youtube]: [https://www.youtube.com/watch?v=0WjDrQ0IhBw](https://www.youtube.com/watch?v=0WjDrQ0IhBw)
[^youtube2]: [https://www.youtube.com/watch?v=W2R9YTXJeWE](https://www.youtube.com/watch?v=W2R9YTXJeWE)
[^trends]: [https://trends.google.com/trends/explore?date=all&q=scary%20maze%20game](https://trends.google.com/trends/explore?date=all&q=scary%20maze%20game)
[^snl]: [https://youtu.be/4CD0ZbvIyQE?t=38](https://youtu.be/4CD0ZbvIyQE?t=38)
[^jpexs]: [https://github.com/jindrapetrik/jpexs-decompiler/releases](https://github.com/jindrapetrik/jpexs-decompiler/releases)

## Decompiling The Maze

Later in this post I'll mention how I decompiled the scary maze game, but if you'd like to view the game's source code I've [made it available as a GitHub Gist](https://gist.github.com/JakeSteam/fc1614c3f5a92b281dba55f6081e7288).

### How does the detection work?

A level is failed when your mouse leaves the blue area. You might think this means the game logic is to fail when you are no longer on blue but... nope! It's actually the opposite: You fail when you touch a black area.

These black areas are actually multiple giant rectangles, each of which has their own mouseover detection. Here's a walkthrough of what happens when you touch one of these black rectangles, using part of level 1 as an example:

| Component | Explanation | Screenshot |
| --- | --- | --- |
| Failure rectangle | "Wall3" is a rectangle at the top of "frame 4", highlighted in red. | [![the maze game failure area](/assets/images/2023/maze-walkthrough-1-thumbnail.png)](/assets/images/2023/maze-walkthrough-1.png) |
| Mouseover event | The `frame4()` function sets a `MOUSE_OVER` event listener on "Wall3", so that `Level1Wall_MouseOverHandler` is triggered when the mouse touches it. | [![the maze game mouseover](/assets/images/2023/maze-walkthrough-2.png)](/assets/images/2023/maze-walkthrough-2.png) |
| Reset | `Level1Wall_MouseOverHandler` removes the "dot" (player) from the screen, and sends the player back to frame 3. | [![the maze game failure event](/assets/images/2023/maze-walkthrough-3.png)](/assets/images/2023/maze-walkthrough-3.png) |
| Retry | Frame 3 is the main game screen. | [![the maze game main screen](/assets/images/2023/maze-frame-3-thumbnail.png)](/assets/images/2023/maze-frame-3.png) |

### Is there a level 4?

Despite the many claims online (e.g., a video from 2008 with 1.4m views[^level-4]) and the game's original description (below) there is no level 4:

> The Maze! Test your skills! Try to reach the goal without touching the walls! How steady is your hand? Let's find out! Try and beat all four levels! Play NOW!

This can be proven definitively in the game's files:

| Proof | Screenshot |
| --- | --- |
| The ActionScript code that handles failing a level only has code for levels 1-3. | [![the maze game no level 4 code](/assets/images/2023/maze-3-levels-thumbnail.png)](/assets/images/2023/maze-3-levels.png) |
| In Flash files, any unused font characters are removed. The font used for level titles (Arial Black) only includes the numbers 1-3. | [![the maze game no level 4 fonts](/assets/images/2023/maze-3-font-thumbnail.png)](/assets/images/2023/maze-3-font.png) |
| All the strings within the game's files can be shown at once. There is no "Level 4". | [![the maze game no level 4 text](/assets/images/2023/maze-3-text-thumbnail.png)](/assets/images/2023/maze-3-text.png) |

[^level-4]: [https://www.youtube.com/watch?v=NedCSuGt0eg](https://www.youtube.com/watch?v=NedCSuGt0eg)

### Is there anything hidden?

Short answer: No.

Longer answer: Using the list of frames in the game, we can see everywhere the player could possibly go. There's nothing besides what you'll see on a normal playthrough:

| Frame # | Content | Screenshot |
| --- | --- | --- |
| 1 | The initial loading screen. | [![the maze game frame 1](/assets/images/2023/maze-frame-1-thumbnail.png)](/assets/images/2023/maze-frame-1.png) |
| 2 | The splash screen, once all content is loaded. | [![the maze game frame 2](/assets/images/2023/maze-frame-2-thumbnail.png)](/assets/images/2023/maze-frame-2.png) |
| 3 | The main game screen, this is also where failing on level 1 takes players. | [![the maze game frame 3](/assets/images/2023/maze-frame-3-thumbnail.png)](/assets/images/2023/maze-frame-3.png) |
| 4 | Level 1 | [![the maze game frame 4](/assets/images/2023/maze-frame-4-thumbnail.png)](/assets/images/2023/maze-frame-4.png) |
| 5 | Level 2 | [![the maze game frame 5](/assets/images/2023/maze-frame-5-thumbnail.png)](/assets/images/2023/maze-frame-5.png) |
| 6 | Level 3 | [![the maze game frame 6](/assets/images/2023/maze-frame-6-thumbnail.png)](/assets/images/2023/maze-frame-6.png) |
| 7 | The initial screamer, adds the face image and the scream sound. | [![the maze game frame 7](/assets/images/2023/maze-frame-7-thumbnail.png)](/assets/images/2023/maze-frame-7.png) |
| 8 - 112 | Scream sound plays. | [![the maze game frame 8](/assets/images/2023/maze-frame-8-thumbnail.png)](/assets/images/2023/maze-frame-8.png) |
| 113 - 163 | Scream sound continues to play, whilst "www.winterrowd.com" slides down the screen. | [![the maze game frame 113](/assets/images/2023/maze-frame-113-thumbnail.png)](/assets/images/2023/maze-frame-113.png) |
| 164 | Ending screen, with options to share the maze and contact the creator. | [![the maze game frame 164](/assets/images/2023/maze-frame-164-thumbnail.png)](/assets/images/2023/maze-frame-164.png) |

### Final technical notes

#### How was it decompiled?

I used [JPEXS Decompiler v18.3.0](https://github.com/jindrapetrik/jpexs-decompiler/releases/tag/version18.3.0) for all of this post, it's open source and very easy to use. I recommend using the "Mute frame sounds" button to avoid accidentally falling for the screamer repeatedly whilst navigating the the game files!

[![JPEXS decompiler mute](/assets/images/2023/maze-mute.png)](/assets/images/2023/maze-mute.png)

#### Multiple versions?

The game file's metadata after downloading it from multiple independent sources shows it has a SWF version of 9. This maps to Flash Player 9.0.115.0[^flash-mapping], which was released December 2007[^flash-release], seemingly... a year and a half after the game was released.

Initially I wondered how this was possible, then I realised the first time the game appeared on the author's site it was called "v1.1"[^first-visible]. Since this version also contains advertising, I can only assume this version was released *after* v1.0's success. 

[^flash-mapping]: [https://stackoverflow.com/a/10900792/608312](https://stackoverflow.com/a/10900792/608312)
[^flash-release]: [https://en.wikipedia.org/wiki/Adobe_Flash_Player#:~:text=Adobe%20Flash%20Player%209%20Update%203](https://en.wikipedia.org/wiki/Adobe_Flash_Player#:~:text=Adobe%20Flash%20Player%209%20Update%203)

## Impact

"The Scary Maze Game" might not have entirely hit the mainstream (besides the SNL appearance), but for those who experienced the shock first hand it has a lasting impact! 

Speaking personally, I discovered this game whilst I was alone through one of the free online game sites I frequented when I was around 12-13. Even ~15 years later I can still remember the cold spike of fear and clammy hands that immediately followed, and how it absolutely stuck with me for weeks afterwards. Those that played it in a shared context (pranked by friends) might have had a less memorable shock, but for me it was easily one of the scariest things I've experienced.

## Who created it?

Jeremy Winterrowd. 

He's a pretty elusive guy, with the in-game linked Twitter inactive since 2012[^twitter]. Whilst I did find more up-to-date social media (only inactive for 3 years!), I won't link them in case they are private.

[^twitter]: [https://twitter.com/winterrowd](https://twitter.com/winterrowd)

## Conclusion


