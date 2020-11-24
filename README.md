# Welcome to my GitHub page

I'm Johannes I was born in Trondheim, Norway. I am now 18 years old and i'm an aspiring software developer who likes to code, been learning ``` python ``` for a while and like to work in it.
Made some funny small projects like a [keybot](https://joonsey.github.io/Keybot/), [flappybird!](https://github.com/Joonsey/FlappybirdAi) and [a discord bot named Snowden](https://joonsey.github.io/Snowden/) with lots more to come.

## Blog
* [week 37](#firstweek)
* [week 38](#secondweek)
* [week 39](#thirdweek)
* [week 40](#fourthweek)
* [week 41](#fifthweek)
* [week 42](#sixthweek)
* [week 43](#seventhweek)
* [week 44](#eightweek)
* [week 45](#ninthweek)
* [week 46](#tenthweek)
* [week 47](#eleventhweek)
### Why Python?

Python is easy to learn and very comprehensible, and was by far the best choice to learn as a beginner.
It's also easy to find documentation and useful modules from other people and use them.

### Have you done any large scale projects?

Not yet, but I like to work on some intermediate projects like neural network flappy bird and socketing (i.e server and client hosting).
Although most of repositories are private as of now i'll publish more as I see them improve and become more comfortable with publishing them.

I have done some html and set up a website on a local host, but as I have moved into a new flat I haven't port forwarded my port yet so I am unavailable to host the server as of now. front-end is developed with ```html``` and ```css```, and back end is entirely made with the [Flask](https://flask.palletsprojects.com/en/1.1.x/) module in python.

### Do you have any other hobbies?

Yes! I play World of Warcraft at a competitive level, among many other games.
I have a Steam library of around 600 games.
I aspire to become proficient in almost every competitive enviornment I am in.
I qualify as top 0.5% - 20% in most of the games I play


### My most recent projects

You can find all my published projects and repositories over at my [git hub](https://github.com/Joonsey)
Where you can also track my projects and contributions!

## How I work or approach projects

I usually find something that piqued my interest as I see it's either interesting or would be overall helpful with something, then try do research to find different approaches to make a suiteable program. I am very comfortable picking up new modules and finding proper documentation as I'm very comfortable with Python syntax. 

I usually like to work really hard on something in one sitting, don't usually take a lot of breaks. Prefer to do a lot of work at once to not miss or forget something. Don't like to sit and wait for something while doing nothing. 

### How did you go about making the flappy bird?

I decided one day at 5 am I wanted to learn neural network as I felt like I was ready for the task. I found a nice tutorial for the "neat" module and sat down developing the game classes and loop for about 9 hours straight. Then I proceeded to implement the neural network and tempered with different weights/values until I had something I was very comfortable with.

**bird class** 

```python
class Bird:
    IMGS = BIRD_IMGS
    MAX_ROTATION = 25
    ROT_VEL = 20
    ANIMATION_TIME = 5
    
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.tilt = 0
        self.tick_count = 0
        self.v = 0
        self.height = self.y
        self.img_count = 0
        self.img = self.IMGS[0]

    def jump(self):
        self.v = -10.5 
        self.tick_count = 0
        self.height = self.y
    
    def move(self):
        self.tick_count += 1

        d = self.v*self.tick_count + 1.5*self.tick_count**2
        
        if d >= 16:
            d = 16
        
        if d < 0:
            d -= 2

        self.y = self.y + d

        if d < 0 or self.y < self.height + 50:
            if self.tilt < self.MAX_ROTATION:
                self.tilt = self.MAX_ROTATION
        else:
            if self.tilt > -90:
                self.tilt -= self.ROT_VEL

    def draw(self, win):
        self.img_count += 1

        if self.img_count < self.ANIMATION_TIME:
            self.img = self.IMGS[0]
        elif self.img_count < self.ANIMATION_TIME*2:
            self.img = self.IMGS[1]
        elif self.img_count < self.ANIMATION_TIME*3:
            self.img = self.IMGS[2]
        elif self.img_count < self.ANIMATION_TIME*4:
            self.img = self.IMGS[1]
        elif self.img_count == self.ANIMATION_TIME*4+1:
            self.img = self.IMGS[0]
            self.img_count = 0
        
        if self.tilt <= -80:
            self.img = self.IMGS[1]
            self.img_count = self.ANIMATION_TIME*2

        rotated_image = pygame.transform.rotate(self.img, self.tilt)
        new_rect = rotated_image.get_rect(center=self.img.get_rect(topleft = (self.x, self.y)).center)
        win.blit(rotated_image, new_rect.topleft)

    def get_mask(self):
        return pygame.mask.from_surface(self.img) 
```
I made functions that draw the bird on the screen to avoid any complications and for easy accessability.
I also made a function to get the mask of the bird to check for colission. Which I further improved to only check for colored pixels making the hitbox pixel-perfect.

This class is run 50 times (by default) until every bird is dead and then it will repeat using the best bird as it's main 'genome'. This ai is very succesful and will go on indefinetly after a few (if not the first) generations.

## How did you make Snowden?

Had some time to spend and wanted to practie some python. __Sadly a discord bot doesn't really use any python, it's almost entirely decorators and pre-made functions like:__
```python
@client.command()
async def ping(ctx):
    await ctx.send(f'{round(client.latency * 1000)}ms')
    await ctx.trigger_typing()
```
**or things like**
```python
@client.command()
async def whatever_you_want_the_bot_to_react_to(ctx) 
    await ctx.send('Whatever you want the bot to send')
```
### I want to know more about this Snowden bot!

Sure! [here](https://joonsey.github.io/Snowden/) is the page I made for it. 


# Blog
#### first week {#firstweek}
I have gotten into a weird sleep schedule where i sleep from 5-9pm and stay up for the rest of the day/night. Althought i'm content with it as i'm atleast able to show up in class now. I have spent alot of time researching `css` and `html`. As well as learning some fundamentals of a secure back-end query and process made with SQL and `JavaScript` from a Turk.  

I'm some what dissatisfied with my progress however, been alot of researching but my physical practise has been lackluster. I find implementing`css` in `html` being unnaturaly hard which is strange considering how easy they are suppose to be. I did watch a [really good presentation about css grid](https://www.youtube.com/watch?v=7kVeCqQCxlk&ab_channel=CodingTech). (I recommend everyone to watch, even people who don't have a general interests in IT.) Which was extremely helpful and simple, was also fun to practise with.

### second week {#secondweek}
Remained the same sleep schedule, learned some more api calls but lost alot of progress due to being incompetent. Gotten some offers on Fiverr but declined all of them as most of them seemed criminal or malicious.

Tried to some Web-dev but didn't get too far. Understand HTML and CSS even better now though

### 3rd week {#thirdweek}
Didn't really do alot, just played video games. Although tried to learn about 0auth but that seems overcomplicated and i am contracting a migrane just thinking about it.

Tried to practise webscraping! So i made a script that finds a movie on IDMB and returns the rating of the said movie in a script. Pretty cool. (might link to that later when it's fully operational)

### 4th week {#fourthweek}
Vacation, video game rampage

### 5th week {#fifthweek}
Back in a rythm where i sleep all day but code mostly during the morning before school. I have again implemented new API's on my Discord bot and made some new funny functions as well as making it display weather information in my area using YR's Weather API. Having alot of fun with that. 

Alot of trial and error with 0Auth to attempt to implement World Of Warcraft Data on my discord bot. Again, it's [Snowden](https://joonsey.github.io/Snowden/) i'm talking about.

### 6th week {#sixthweek}
Got sick alot but just did some silly projects regarding some practise for school so I could help myself practise for school tests.
Was especially helpful to stay motivated and subconsciously learn while having fun.

### 7th week {#seventhweek}
No longer sick and playing alot of World of warcraft because of the pre-patch to the new expansion.

### 8th week {#eightweek}
Done alot of scripting and trying automation where i can. Making bots and scripts to play games or parse images.

### 9th week {#ninthweek}
Parsing images still, just managed to install tensorflow and learning Keras, trying to understand how it works, with moderate success.
Also made a discord bot to give inputs on my computer, successfully made the discord bot play slay the spire through parsing images on my screen and recieveing direction from inputs in discord. Both through reactions and messages.

### 10th week {#tenthweek}
Looking into interesting algorythms like boids algorythm which simulates "flock" in animals.

### 11th week {#eleventhweek}
Fixing some scripts and helping some friend practise for a Python test, went very succesfull. Learning the use dictionairies.

### 12th week {#twelvthweek}
Made a nosql database and i am managing it with python code, also made a website template. So now i just have to integrate them...
