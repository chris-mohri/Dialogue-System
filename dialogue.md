## An Overview of Dialogue Systems in Games
Consuming narrative in games often requires some form of system by which the player (us) listens to, or reads, the dialogue between characters. In this post, we will discuss text-based dialogue systems as seen in games like <i>Fallout 4</i>, <i>The Witcher 3: Wild Hunt</i>, and others. These dialogue system will vary in both functionality and display which provide their own features for their game. This post seeks to understand the decisions, along with any necessary implementation details, made by developers when designing their dialogue system in order to pave a direction for when I implement a working system of my own. As such, I will discuss multiple topics relevant to dialogue systems down below. 

### Basic Design 
Although dialogue systems in games can vary widely depending on the needs of the game, many aspects will remain the same. 

These commonalities include:
```
1. A way to display the text onto the screen (UI)
2. The need to store the text somewhere
3. Reading through the dialogue continues story progresion
```

However, there are many features that are present in some games but not others. These features are made to enhance the current game's experience, but may not necessarily be relevant or necessary if present in another game.

These optional features include:
```
1. Player Choice in Dialogue
2. Skip Feature
3. Log (being able to see a log of what was said so far in the current conversation)
```

These decisions will be visited in the later discussion but should lay down a foundation for what one can expect from the dialogue systems discussed. 

### Player Choice - ໒(⊙ᴗ⊙)७✎▤
An important aspect in many narrative-heavy games is allowing the player to decide the choices made by the protagonist whether it be which quest to take next or how you speak to another character. Take the Witcher 3's decision tree for instance.
<br/><br/><img src="images/witcher_2.jpg" alt="image" width="500" style="margin-left:60px;"/><br/>
Or Fallout New Vegas's decision tree:
<br/><br/><img src="images/fallout.jpg" alt="image" width="500" style="margin-left:60px;"/><br/>
<br/>
Both are examples of how, in a RPG game where the player is encouraged to experience varying playstyles, having dialogue choices that can affect the story is a vital part of creating the experience CD Projekt Red and Bethesda envisioned. 

This feature can be further explored in games like Fallout New Vegas where making choices may require the player to pass a stat check, such as <b>Speech</b>. As shown above, the player may only choose that option if they leveled up their Speech stat enough. In RPG games like the Fallout series, it is very relevant to the game mechanics that this be a feature that is included in the dialogue system. However, other games like The Legend of Zelda: Twilight Princess, may not have conditional choices like this. 

A player-choice implementation can be roughly sketched as follows:
```
1. Have a data structure that tracks the varying branches of dialogue where each branch is the product of the player having made a decision
2. Prompt the player with a series of options mid-dialogue. This prompt should pause the rest progression of the rest of the dialogue until the player has clicked their choice. Alternatively, have a timer (as seen in the Witcher 3 image above) where the dialogue will continue down a particular path even if the player has yet to make their choice
3. Include a condition check, which would require reading the player's stat to determine if a particular choice is available for choosing by the player 
4. Remember which choices were made (possibly have flag variables) if the choices are vital in determining the ending of the game
```

### How Text is Stored - (づ ◕‿◕ )づ
Yes this is very obvious (of course the text in a dialogue system has to be stored somewhere (－_－) zzZ), but this is actually quite interesting to think about. When typically writing a script for character dialogue, should the writer just use Microsoft Word or Google Docs to do this and then retype it all into the game? Or should the text on the screen just read it from a text file stored in some folder? It very much depends on the scope of the game and how much dialogue there is (sorry for the boring answer). One method for writing this dialogue is with <a href="https://store.steampowered.com/app/1273620/Dialogue_Designer/">Dialogue Designer</a>that looks like this:

<br/><br/><img src="images/example_implementation_name.jpg" alt="image" width="500" style="margin-left:60px;"/><br/>
<br/>

It seeks to handle the whole dialogue system's internal logic, including storing and maintaining the branching dialogue paths as explained previously. However, as shown in the picture, the developer must manually enter the whole script into this data structure, which may be impractical or inefficient. For small projects, it can be a quick solution, but for larger projects with thousands of pages of dialogue, there may be a better solution. 

Given the variance in project size and requirements, how the actual text in dialogue is stored can vary. It could be a regular text file, XML, or some variation or database. So long as the information can be parsed, its implementation should not be a huge concern. However, one important thing to note is that a text file, for example, can be easily accessed and read by anyone who ventures into the game's directory. One solution to this is to encrypt the files so that someone cannot spoil the ending of the game for themselves.  

### Other Features
Features like skipping the current conversation or opening a log of the current conversation are quality of life features that, while not necessary, can enhance the experience for some players. We will look at Arknights' implementation of these features as shown below:
<br/><br/><img src="images/ak1.jpg" alt="image" width="500" style="margin-left:60px;"/><br/>
<br/><br/><img src="images/ak2.jpg" alt="image" width="500" style="margin-left:60px;"/><br/>
<br/>
Although 

### User Interface - (っ˘ڡ˘ς)
(The most interesting topic of this post!) The way that the dialogue system looks is 