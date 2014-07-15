Bitz
====

Raspberry Pi Primary School

Raspberry Pi Picamera Photobooth Fortune Teller

Photobooth code from pastebin: http://pastebin.com/download.php?i=Bj2mCs2x

import picamera
from time import sleep
import pygame
import random

WIDTH=800
HEIGHT=600
FONTSIZE=50

def quote():
    options = ["Strange person",
               "You should have smiled",
               "you will break the camera",
               "you need a hair cut",
               "You should try SnapChat",
               "Are you a model?",
               "You've grown an inch",
               "Have you shrunk?"
               ]
    return random.choice(options)

# INIT CAMERA
camera = picamera.PiCamera()
camera.vflip = False
camera.hflip = False
camera.brightness = 60

# BUILD A SCREEN
pygame.init()
screen = pygame.display.set_mode((WIDTH,HEIGHT))
black = pygame.Color(0, 0, 0)
textcol = pygame.Color(255, 255, 0)
screen.fill(black)
n=0

while True:
    # TAKE A PHOTO
    name="image"+str(n)+".jpeg"
    n+=1
    camera.start_preview()
    sleep(0.5)
    camera.capture(name, format='jpeg', resize=(WIDTH,HEIGHT))
    screen.fill(black)
    pygame.display.update()    
    camera.stop_preview()

    #READ IMAGE AND PUT ON SCREEN
    img = pygame.image.load(name)
    screen.blit(img, (0, 0))

    #OVERLAY CAPTIONS AS TEXT
    text = quote()
    font = pygame.font.Font('freesansbold.ttf', FONTSIZE)
    font_surf = font.render(text, True, textcol)
    font_rect = font_surf.get_rect()
    font_rect.left = 100
    font_rect.top = 100
    screen.blit(font_surf, font_rect)
    pygame.display.update()

    # WAIT A BIT
    sleep(3)

# CLOSE CLEANLY AND EXIT
pygame.quit()


...

#Ideas

Change font from yellow
Shorter fortune messages
Give children the code so they can add their own message ideas

Now, can the pic and fortune message be published to twitter?

We used this:

http://raspi.tv/2013/how-to-create-a-twitter-app-on-the-raspberry-pi-with-python-tweepy-part-1#install

http://raspi.tv/2014/tweeting-with-python-tweepy-on-the-raspberry-pi-part-2-pi-twitter-app-series

#We had this error message:

https://github.com/tweepy/tweepy/issues/15

Top tip - don't name your .py code file the same name as the relevant software file e.g. Tweepy

#Error 32

We had problems with the twitter API codes. Regenerating the authentication codes didn't solve it though.

http://discuss.tweepy.org/t/authentication-failed-error-code-32/36



