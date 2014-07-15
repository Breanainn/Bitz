Bitz
====

Raspberry Pi Primary School

Raspberry Pi

Photobooth code from pastebin:

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

Ideas

Change font from yellow
Shorter fortune messages
Give children the code so they can add their own message ideas
