'''
Sehajveer Dhillon
2D Lists
Tile-Based Game
'''
from processing import *
from random import randint
width = 540
height = 450
tileSize = 30
numCol = width/tileSize
numRow = height/tileSize

#starting position
player = {
    'row' :0,
    'col' :1
    }
# 0 = maze 1 = walls 2 = fire 3 = teleport 5 = start 6 = end 
# 8 colums, 15 rows
maze = [
    [1,5,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,0,0,3,0,2,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,1,1,0,1,3,0,0,0,0,0,3,0,0,1,1,1],
    [1,0,0,0,2,1,0,1,1,0,1,1,1,1,0,0,2,1],
    [1,1,0,1,1,1,0,1,1,0,0,1,2,1,0,1,0,1],
    [1,1,0,1,1,1,0,1,1,1,3,0,0,1,0,1,0,1],
    [1,1,0,1,1,1,0,1,1,1,0,1,1,1,0,1,3,1],
    [1,1,3,0,0,0,0,0,0,0,0,1,1,1,0,1,0,1],
    [1,1,1,1,1,0,1,1,1,1,0,1,1,1,0,1,0,1],
    [1,1,1,1,1,3,1,0,0,1,0,2,0,0,3,0,2,1],
    [1,3,0,1,1,0,0,1,0,1,3,1,1,1,0,1,1,1],
    [1,1,2,1,1,1,1,1,0,1,0,1,1,1,0,1,1,1],
    [1,1,0,0,0,0,0,0,0,0,0,1,1,1,0,1,1,1],
    [1,1,0,1,1,1,1,1,1,1,0,3,0,0,3,1,1,1],
    [1,1,6,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
    ]
def setup():
    global playerPic
    size(width,height)
    playerPic = loadImage('https://oyohub.s3.amazonaws.com/spriteeditor/projects/59b6efd3ca292c67c0996e7f/Charcter.gif')
    findTeleports()
def findTeleports():
    global teleports
    teleports = []
    for r in range(len(maze)):
        for c in range(len(maze[r])):
            if maze[r][c] == 3:
                t = {
                    'row' : r,
                    'col' : c
                    }
                teleports.append(t)
    
    #If screen is grey then the URL is wrong
def drawGrid():
    stroke(0,107,179)
    for x in range(0,width,tileSize):
        line(x,0,x,height)
    for y in range(0,height,tileSize):
        line(0,y,width,y)
def drawWalls():
    for row in range(numRow):
        for col in range(numCol):
            if maze[row][col] == 1:        #Walls
                stroke(0,0,0)
                fill(200,200,200)
                rect(tileSize*col,tileSize*row,tileSize,tileSize)
            if maze[row][col] == 2:        #Fire
                stroke(255,0,0)
                fill(15,15,15)
                rect(tileSize*col,tileSize*row,tileSize,tileSize)
            if maze[row][col] == 3:        #Teleport
                stroke(0,0,0)
                fill(255,255,0)
                rect(tileSize*col,tileSize*row,tileSize,tileSize)
            if maze[row][col] == 5:        #Start
                stroke(0,0,0)
                fill(0,150,0)
                rect(tileSize*col,tileSize*row,tileSize,tileSize)
            if maze[row][col] == 6:        #End
                stroke(0,0,0)
                fill(0,150,0)
                rect(tileSize*col,tileSize*row,tileSize,tileSize)
def movePlayer(direction):
    if direction == UP:
        newR = player['row'] - 1
        newC = player['col']
        if newR >= 0 and maze[newR][newC] != 1:
            player['row'] = newR
    if direction == DOWN:
        newR = player['row'] + 1
        newC = player['col']
        if newR >= 0 and maze[newR][newC] != 1:
            player['row'] = newR
    if direction == RIGHT:
        newR = player['row']
        newC = player['col'] + 1
        if newC >= 0 and maze[newR][newC] != 1:
            player['col'] = newC
    if direction == LEFT:
        newR = player['row']
        newC = player['col'] - 1
        if newC >= 0 and maze[newR][newC] != 1:
            player['col'] = newC
    checkTeleports(player['row'],player['col'])
def checkTeleports(row,col):
    myT = None
    for i in range(len(teleports)):
        t = teleports[i]
        if (t['row'] == row and t['col'] == col):
            myT = i
    if myT is not None:
        r = randint(0,len(teleports) - 1)
        while r == myT:
            r = randint(0,len(teleports) - 1)
        player['row'] = teleports[r]['row']
        player['col'] = teleports[r]['col']
def keyPressed():
    if keyboard.keyCode in [UP,DOWN,LEFT,RIGHT]:
        movePlayer(keyboard.keyCode)
def win():
    fill(0,255,255)
    textSize(40)
    text('You Win!!',200,200)
    exitp()
def gameOver():
    fill(0,255,255)
    textSize(40)
    text('You Lose:(',175,200)
    text('You Hit The Fire',130,240)
    exitp()
def draw():
    background(0,0,0)
    drawGrid()
    drawWalls()
    image(playerPic,player['col']*tileSize,player['row']*tileSize)
    if maze[player['row']][player['col']] == 6:    #End of the maze
        win()
    if maze[player['row']][player['col']] == 2:    #Die
        gameOver()
run()
