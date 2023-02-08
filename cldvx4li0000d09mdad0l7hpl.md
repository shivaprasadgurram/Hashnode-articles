# Coupling in software engineering

***<mark>Coupling is a measure of how much work is involved in changing something.</mark>***

Being an engineer, we have certain rules and principles to follow when creating outstanding software. Coupling is even more important in building great software.

The only thing constant in technology is **<mark>change</mark>**

* Business requirements change
    
* Frameworks change
    
* Code changes
    

We want to make functional changes with as less code changes as possible, isn't it?

Before diving into an understanding of the aforementioned concepts, let's look at some examples of coupling that have been used in real life.

1. An engine is tightly coupled to a car
    
    1. The process of changing a car's engine takes a long time.
        
2. A wheel is loosely coupled to a car
    
    1. With the very little disruption to the fundamental operation of the car, changing a wheel is a quick process.
        
3. A laptop is loosely coupled to a specific area
    
    1. It is not strongly connected to a particular location, so we may take it wherever we choose.
        
4. A computer is tightly coupled to a specific area
    
    1. Compared to a laptop, it takes up more room and is difficult to transport.
        

I believe, you now understand the difference between tight coupling and loose coupling.

### Types

1. Tight coupling
    
2. Loose coupling
    

### Tight coupling

Tight coupling means that the degree of dependency between two components is very high. In general, tight coupling is usually not good because it reduces the flexibility and re-usability of the code.

### Loose coupling

Loose coupling means that the degree of dependency between two components is very low. So it increases the flexibility and re-usability of the code.

Let's move on to the coding section to learn more about things in-depth.

Let's say we are creating a game application. A primary app main class should come first, then a class for game runner.

**App.java**

```java
public class App {
    public static void main(String[] args) {
        var marioGame = new MarioGame();
        var gameRunner = new GameRunner(marioGame);
        gameRunner.run();
    }
}
```

**GameRunner.java**

```java
public class GameRunner {
    MarioGame marioGame;
    public GameRunner(MarioGame marioGame) {
        this.marioGame = marioGame;
    }
    public void run() {
        System.out.println("Running game: " + marioGame);
        marioGame.up();
        marioGame.down();
        marioGame.left();
        marioGame.right();
    }
}
```

**MarioGame.java**

```java
public class MarioGame {
    public void up() {
        System.out.println("Jump");
    }
    public void down() {
        System.out.println("Go into a hole");
    }
    public void left() {
        System.out.println("Go back");
    }
    public void right() {
        System.out.println("Accelerate");
    }
}
```

If we look closely, the GameRunner class and MarioGame are inextricably linked.

Consider that a new game called PUBG comes out tomorrow. Wouldn't a lot of changes then be necessary?

**PubgGame.java**

```java
public class PubgGame {
     public void up() {
        System.out.println("Jump into forest");
    }
    public void down() {
        System.out.println("Hide in hole");
    }
    public void left() {
        System.out.println("Kill enemy");
    }
    public void right() {
        System.out.println("Accelerate");
    }
}
```

What adjustments are now necessary to make this game work?

1) In the GameRunner class, you require another data member similar to MarioGame. How about adding 10 more games to our collection tomorrow?

2) You must create a parameterized constructor to handle the caller, am I correct? The constructor should be generated anytime a new game needs to be run, right?

As we previously discussed, "In technology, the only constant is change," this programme is quite awful.

So far, we've seen that our software is closely tied to a certain game, correct?

So what is the best way to create loosely coupled software?

In this situation, Java Interfaces aids us in resolving this problem.

### *Solution to solve tight coupling problem*

Our game classes will implement the **<mark>GamingConsole </mark>** interface that we will be introducing.

**GamingConsole.java**

```java
public interface GamingConsole {
    void up();
    void down();
    void left();
    void right();
}
```

Instead of various game classes like the ones listed above, GameRunner class should have GamingConsole.

**GameRunner.java**

```java
public class GameRunner {
    private GamingConsole gamingConsole;
    public GameRunner(GamingConsole gamingConsole) {
        this.gamingConsole = gamingConsole;
    }
    public void run() {
        System.out.println("Running game: " + gamingConsole);
        gamingConsole.up();
        gamingConsole.down();
        gamingConsole.left();
        gamingConsole.right();
    }
}
```

Both MarioGame and PubgGame classes should implement GamingConsole and override abstract methods.

**MarioGame.java**

```java
public class MarioGame implements GamingConsole{

    @Override
    public void up() {
        System.out.println("Jump");
    }

    @Override
    public void down() {
        System.out.println("Go into a hole");
    }

    @Override
    public void left() {
        System.out.println("Go back");
    }

    @Override
    public void right() {
        System.out.println("Accelerate");
    }
}
```

**PubgGame.java** also going to be similar.

That's all; in contrast to our earlier iteration, our software is now loosely coupled. Now, one need not worry about updating the logic in the GameRunner class if tomorrow brings a new game.

It will be as easy as described here. Assume SubwaySurfers is a new game.

```java
var subwaySurfers = new SubwaySurfers();
var gameRunner = new GameRunner(subwaySurfers);
gameRunner.run();
```

That is the entirety of the tightly and loosely coupled concepts in software engineering. In addition, I've included the graphic below for visual illustration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675873604122/8b0ec39c-4a23-442a-a216-b4ef76ab0819.png align="center")

Please connect with me if you enjoyed this article.

\[LinkedIn\]([https://www.linkedin.com/in/shivaprasadgurram/](https://www.linkedin.com/in/shivaprasadgurram/)).

\[Telegram group\]([https://t.me/+764RyZ8uGVw3MzQ1](https://t.me/+764RyZ8uGVw3MzQ1))

Thanks,

Shiva Prasad Gurram