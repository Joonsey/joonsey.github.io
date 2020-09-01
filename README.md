## Welcome to my GitHub page

I'm Johannes I was born in Trondheim, Norway. I am now 18 years old and i'm an aspiring software developer who likes to program, been learning ``` python ``` for a while and like to work in it.
Made some funny small projects like a [keybot](https://joonsey.github.io/Keybot/), and [flappybird!](https://github.com/Joonsey/FlappybirdAi) (with an integrated NEURAL NETWORK AI) with lots more to come.

### Why Python?

Python is easy to learn and very comprehensible, and was by far the best choice to learn as a beginner.
It's also easy to find documentation and usefull modules from other people and use them.

### Have you done any large scale projects?

Not yet, but i like to work on some intertemdiate projects like neural network flappy bird and socketing (i.e server and client hosting).
Although most of repositories are private as of now i'll publish more as i see them improve and become more comfortable with publishing them.

I have done some html and set up a website on a local host, but as i have moved into a new flat i haven't port forwarded my port yet so i am unavailable to host the server as of now. front-end is developed with ```html``` and ```css```, and back end is entirely made with the [Flask](https://flask.palletsprojects.com/en/1.1.x/) module in python.

### Do have any other hobbies?

Yes! I play World of Warcraft at a competetive level, among many other games.
I have a Steam library of around 600 games.
I tend to want to become very good at almost every competetive game i play.
I qualify as top 0.5% - 15% in most of the games i play


### My most recent projects

You can find all my published projects and repositories over at my [git hub](https://github.com/Joonsey)
Where you can also track my projects and contributions!

## How i work or aproach projects

i usually find something that spikes my interest as i see it's eithet interesting or would be overall helpfull with something, then try do research to find differen aproaches to make a solution. I am very comfortable picking up new modules and finding proper documentation as i'm very comfortable with Python syntax. I usually like to work really hard on something in one sitting, don't usually take a lot of breaks. Prefer to do alot of work at once to not miss or forget something. Don't like to sit and wait for something while doing nothing. 

### How did you go about making the flappy bird?

I decided one day at 5 am i wanted to learn neural network as i felt like i was ready for the task. I found a nice tutorial for the "neat" module and sat down developing the game classes and loop for about 9 hours straight. Then i proceeded to implement the Neural network and tempered with differen weights/values until i had something i was very comfortable with.

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
I made functions that draws the bird on the screen to avoid any complication and for easy accessability.
I also made a function to get the mask of the bird to check for colission. which i further improved to only check for colored pixels making the hitbox pixel-perfect.

This class is run 50 times (by default) until every bird is dead and then it will repeat using the best bird as it's main 'genome'. This ai is very succesfull and will go on indefinatly after a few (if not the first) generations.
