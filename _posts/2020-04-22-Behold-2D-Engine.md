---
layout: post
title: "Behold! A Custom 2D Game Engine"
date: 2020-04-22 06:09:00 -0700
comments: true
---

Since about July of 2019, I’ve been making a 2D game engine entirely in the Java Programming language and it’s native libraries. You may think why I would use Java of all languages. I chose Java mainly because of it’s simplicity. This game engine is also not meant for “top of the line” 2D game making. It was mainly designed for simple 8 or 16 bit graphics. This whole project was mainly for fun and to teach myself a little more about game programming. If you would like to see the source, it’s linked [here](https://github.com/JudgeGlass/JGameEngine)

```
// A basic Example
public class Main{
    private static SpriteSheet spriteSheet = new SpriteSheet("file.png");

    public static Main(String args[]){
        Screen gameScreen = new Screen(600, 480, "Tile Game v0.0.1 (Hunter Wilcox)"); // Makes the main window with renderer
        gameScreen.setClearColor(0x0000FF); // Sets the Background color to blue
        
        TestBlock testBlock = new TestBlock(20, 20); // A custom GameObject that renders a block
        
        PlayerMovement playerMovement = new PlayerMovement(new Player(0, 0)); // A custom GameObject that spawns a player
        
        gameScreen.getRenderer().setKeyListener(playerMovement); // Adds a KeyListener to the renderer
        gameScreen.getRenderer().setThreadSleep(28); // Locks the frame rate to 30 FPS
    }
}
```

![Tetris.PNG](https://www.zicron.net/images/Tetris.png "Tetris Example")
