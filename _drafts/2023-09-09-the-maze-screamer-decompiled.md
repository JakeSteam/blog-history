---
title: 20 years ago today 'The Maze' was released, a screamer that scarred millions
author: Jake Lee
layout: post
image: /assets/images/2022/
tags:
    - 
---

intro

## How does the detection work?

A level is failed when your mouse leaves the blue area. You might think this means the game logic is to fail when you are no longer on blue but... nope! It's actually the opposite: You fail when you touch a black area.

These black areas are actually multiple giant rectangles, each of which has their own mouseover detection. Here's a walkthrough of what happens when you touch one of these black rectangles, using part of level 1 as an example:

| Component | Explanation | Screenshot |
| --- | --- | --- |
| Failure rectangle | "Wall3" is a rectangle at the top of "frame 4", highlighted in red. | [![the maze game failure area](/assets/images/2023/maze-walkthrough-1-thumbnail.png)](/assets/images/2023/maze-walkthrough-1.png) |
| Mouseover event | The `frame4()` function sets a `MOUSE_OVER` event listener on "Wall3", so that `Level1Wall_MouseOverHandler` is triggered when the mouse touches it. | [![the maze game mouseover](/assets/images/2023/maze-walkthrough-2.png)](/assets/images/2023/maze-walkthrough-2.png) |
| Reset | `Level1Wall_MouseOverHandler` removes the "dot" (player) from the screen, and sends the player back to frame 3. | [![the maze game failure event](/assets/images/2023/maze-walkthrough-3.png)](/assets/images/2023/maze-walkthrough-3.png) |
| Retry | Frame 3 is the main game screen. | [![the maze game main screen](/assets/images/2023/maze-frame-3-thumbnail.png)](/assets/images/2023/maze-frame-3.png) |

## Is there a level 4?

Despite the many claims online (e.g., a video from 2008 with 1.4m views[^level-4]) there is no level 4. This can be proven definitively in the game's files:

| Proof | Screenshot |
| --- | --- |
| The ActionScript code that handles failing a level only has code for levels 1-3. | [![the maze game no level 4 code](/assets/images/2023/maze-3-levels-thumbnail.png)](/assets/images/2023/maze-3-levels.png) |
| In Flash files, any unused font characters are removed. The font used for level titles (Arial Black) only includes the numbers 1-3. | [![the maze game no level 4 fonts](/assets/images/2023/maze-3-font-thumbnail.png)](/assets/images/2023/maze-3-font.png) |
| All the strings within the game's files can be shown at once. There is no "Level 4". | [![the maze game no level 4 text](/assets/images/2023/maze-3-text-thumbnail.png)](/assets/images/2023/maze-3-text.png) |

[^level-4]: [https://www.youtube.com/watch?v=NedCSuGt0eg](https://www.youtube.com/watch?v=NedCSuGt0eg)

## Is there anything hidden?

Using the list of frames in the game, we can see everywhere the player could possibly go:

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

https://scarymazegameanthology.wordpress.com/
https://videogaming.fandom.com/wiki/The_Maze_(Winterrowd)
https://knowyourmeme.com/memes/scary-maze-game#fn5
https://spartanink.org/6772/showcase/the-origins-of-the-scary-maze-game/

https://web.archive.org/web/20180220231406/http://www.winterrowd.com/maze/

---

# PUT INTO A PROGRAMMING BLOG POST

https://github.com/jindrapetrik/jpexs-decompiler

* Installing decompiler
* Talk about looking at fonts to see used characters
* Talk about looking at actionscript

