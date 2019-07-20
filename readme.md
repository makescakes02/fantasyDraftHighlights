# Fantasy Draft AutoHighlight Viewer

Real simple python program that reads clickydraft or sleeperbot draft boards to enhance your draft party by automatically playing a highlight video of the player who just got selected.

Works best with Chromecast devices, but can be viewed in a youtube browser on your computer if you like.

## Getting Started

This only will work with:

draftboards: clickydraft and sleeperbot (For now) 

display: youtube on your chromecast device or computer/HDMI out

browser: chrome web browser 


Download the files in my git repository to a directory anywhere you like.

This hasn't been super thoroughly tested and there could be bugs, but I've tested it quite a bit while creating it and I'm pretty sure I got everything.  If you find a bug please contact me. 

### Prerequisites

OS: I ran this on my raspberry pi, ubuntu, windows 7, and windows 10 systems no problem. 
Software: Chrome browser
Python Version 3
Packages.....

Package: requests. json. You will need requests and json. Install them if you don't have them. 
```
pip install requests
pip install json
```
Package: selenium. You will also need to install selenium for most configurations.  (If you are using chromecast with sleeper, then this is not needed)  
```
pip install selenium
```
Selenium requires a specific "webdriver" for the version of chrome that you're running. Simple google search should help you find this and the instructions for what to do with the webdriver when you get it. 
```
https://sites.google.com/a/chromium.org/chromedriver/downloads
```


Package: The following packages are necessary if you're going to use chromecast. If not, you can skip past these. 

```
pip install pychromecast
pip install protobuf
pip install zeroconf
pip install casttube
```


### Installing

Download all the files and put them all in the same folder.

After you've created your clickydraft or sleeperbot draft board, you will need to edit the config.py file.
Open it up with any text editor.  
That file is small and only contains a few lines.  Here's how it looks when you download it.

```

site="sleeper"
teams=12
rounds=16
boardNum=12345
chromeCast=False
chromeCastName="YOUR CHROMECAST NAME HERE"
clickySiteVisible=False
autoSearch=True
```
#### site

If you're using clickydraft then enter site="clicky"
If you're using sleeperbot then enter site="sleeper"
If you have anything else in there, the app won't run correctly.  

#### teams/rounds

Super simple stuff here. Change your teams and rounds to the number of teams and rounds in your draft.  

#### boardNum

BoardNum is the number on the end of your clickydraft or sleeperbot URL.

```
https://clickydraft.com/draftapp/board/12345
https://sleeper.app/draft/nfl/12345
```

If this is what your URL looks like then the boardNum is 12345

Sleeper boardNum's are pretty long, like 18 digits.  Best to copy/paste it.

#### chromeCast

chromeCast True or False.. If True then your vids will cast to a chromecast.  If False then they'll play on a youtube screen on your laptop.  
If you set this to True then you also need to list your chromecast's name in the next line.  The name needs to be typed perfectly in order for it to work correctly, including all spaces, punctuation, and capitalization.
If the application cannot find your specific chromecast then it will auto-switch to using youtube on the computer.  If you're not sure why this is happening then please check whether that computer can access that specific chromecast and if so, make sure the chromecast name is typed correctly.

#### clickySiteVisible

The variable "clickySiteVisible" is only used for clickydraft drafts, and can be set to True or False (capitalization is important). Default is False.

If you set it to True then the draft site will pop up on your screen.  If you set it to False then it won't.  
If you aren't going to use chromecast to display the vids then False is probably the best choice here because the point of this app is to display highlight videos. 
If you are using chromecast, then you can set this to True if you want.

#### autoSearch

The last option is "autoSearch" which can be either True or False.

If it's set to True, the program will go out and search youtube for the first highlight reel it can find for that player name.  

This is going to work fine for most players, however some players have common names so the youtube search might return a vid for a different player in a different sport.

You can change this behavior by placing a specific youtube video link of your choice in the vDict file for either sleeperbot or clickydraft. 

```
vDictClicky.py
vDictSleeper.py
```

Both of these files are in your folder already.  The code will look in the correct file and grab whatever link you have placed in that player's entry in the dictionary.  

If there is no link, then it will auto search on youtube.

You can stop the auto search functionality altogether with autoSearch=False .  If you do this, then the code will ONLY play videos for the links that you provide in the dictionary. 

Here's how the first few lines of the dictionary files look after you download...
(using the vDictSleeper.py sleeperbot file since most of the users are on sleeper and not clicky)

```
vDictSleeper ={
    "RBNYGSaquonBarkley":"",
    "RBARIDavidJohnson":"",
    "RBNOAlvinKamara":"",
    "RBDALEzekielElliott":"8CJvUpV2jp0",
    "WRHOUDeAndreHopkins":"",
    "RBCARChristianMcCaffrey":"",

```

As you can see, there's one line for each player, and I've included an example of what the link should look like for Ezekiel Elliot.   Do NOT change the first part of each line before the colon. The app uses that part to lookup each player as it's picked. If you change that part, the code will not be able to find anything for that player. It's very picky.

The capitalization here also matters.  I've taken out all non-alphabetic characters out of the players' names like apostrophes, spaces, dashes, etc.

Going back to the Zeke example:  

```
    "RBDALEzekielElliott":"8CJvUpV2jp0",
```

That will tell the code that when zeke is picked, it will pull up the following link:
```
https://youtube.com/tv#/watch?v=8CJvUpV2jp0
```

If you don't want a specific vid for a player, and you WANT the auto search, then you need to delete everything between the quotes. So a player without a specific vid link will have two double quotes at the end, followed by a comma. 
Like this:

```
    "RBDALEzekielElliott":"",
```
Any change in that will probably cause problems.

If you don't want ANY vid for that player, no matter what, then either delete his entry or put a hashtag at the beginning of the line. 
Like this:
```
#    "RBDALEzekielElliott":"",
```


I've included over 600 possible players that you're allowed to draft in the apps. So you are set even if you have up to 32 team, 18 round draft :)

And I've already assigned specific links for all defensive team highlights.  Honestly some teams didn't have a lot of defensive highlights from last year so I did the best I could on minimal effort.

## To Run

Before running, make sure you've closed out of all of your open chrome windows. 

At your command line, in your installed directory, type: 

```
python draftvid.py
```

If you're using chromecast, you'll get a message stating whether you connected to your device correctly or not.

If you connected then you're ready to draft!

If you didn't connect, or aren't using chromecast, then a chrome window will pop up in fullscreen, ready to display your youtube vids.  In this scenario, this app is best used when you output the video (HDMI) to a big screen TV.  Then enter the picks on a different device, like your phone or another laptop.  Makes the experience a lot cooler.

One thing I should mention is that the first time you run this in a chrome browser, youtube will play an ad.  For whatever reason it always does this on fresh installs and the first time you run it every day. But then afterwards, the ad doesn't pop up very often. I guess it depends on youtube's mood at the time but sometimes you're gonna get an ad here and there.  If you can figure out how to block youtube ads, please IM me lol.  The ads don't seem to pop up as often when you use chromecast, so I guess that's another good reason to use chromecast for this.

## Author

I am thedaynos and I have a patreon if you feel like donating to my "i don't code for free (actually i guess i do) foundation"
https://www.patreon.com/thedaynos

Feel free to report issues here on github if you have questions or find a bug. 
