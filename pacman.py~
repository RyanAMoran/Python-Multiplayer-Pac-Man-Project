import sys, os, math, time, pygame
from pygame.locals import *
import random
from twisted.internet.protocol import Factory
from twisted.protocols.basic import LineReceiver
from twisted.internet import reactor, protocol
from twisted.internet.defer import DeferredQueue
from twisted.internet.defer import Deferred
from twisted.internet.task import LoopingCall
import cPickle as pickle


####networking stuff
class ConnectionHandler():
	def __init__(self):
		self.commandConnection='' #blue ghost
		self.redCommandConnection='' #red ghost
		self.pinkCommandConnection='' #pink ghost
		self.orangeCommandConnection='' #orange ghost

class Command(LineReceiver):

    def __init__(self, handler):
        self.handler = handler

    def connectionMade(self):
	gs.blueGhost.automate=0
	self.handler.commandConnection = self
	l=[gs.blueGhost.rect,gs.player.rect, gs.dotList,gs.big_dotList, gs.score]
	pd = pickle.dumps(l)
	self.handler.commandConnection.transport.write(pd)

    def dataReceived(self, data):
	newList = pickle.loads(data)
	if newList[0]=="blueGhost":
		gs.blueGhost.rect = newList[1]
		if newList[2]==1:
			gs.blueGhost.image = gs.blueGhost.image_left
		elif newList[2]==0:
			gs.blueGhost.image=gs.blueGhost.image_right
		elif newList[2]==2:
			gs.blueGhost.image=gs.blueGhost.image_down
		elif newList[2]==3:
			gs.blueGhost.image=gs.blueGhost.image_up
	return

class CommandFactory(Factory):

    def __init__(self, handler):
	self.handler = handler

    def buildProtocol(self, addr):
	return Command(self.handler)

class redCommand(LineReceiver):

    def __init__(self, handler):
        self.handler = handler

    def connectionMade(self):
	gs.redGhost.automate=0
	gs.redGhost.automate=0
	self.handler.redCommandConnection = self
	l=[gs.redGhost.rect,gs.player.rect, gs.dotList,gs.big_dotList, gs.score]
	pd = pickle.dumps(l)
	self.handler.redCommandConnection.transport.write(pd)

    def dataReceived(self, data):
	newList = pickle.loads(data)
	if newList[0]=="redGhost":
		gs.redGhost.rect = newList[1]
		if newList[2]==1:
			gs.redGhost.image = gs.redGhost.image_left
		elif newList[2]==0:
			gs.redGhost.image=gs.redGhost.image_right
		elif newList[2]==2:
			gs.redGhost.image=gs.redGhost.image_down
		elif newList[2]==3:
			gs.redGhost.image=gs.redGhost.image_up

class redCommandFactory(Factory):

    def __init__(self, handler):
	self.handler = handler

    def buildProtocol(self, addr):
	return redCommand(self.handler)





class pinkCommand(LineReceiver):

    def __init__(self, handler):
        self.handler = handler

    def connectionMade(self):
	gs.pinkGhost.automate=0
	gs.pinkGhost.automate=0
	self.handler.pinkCommandConnection = self
	l=[gs.pinkGhost.rect,gs.player.rect, gs.dotList,gs.big_dotList, gs.score]
	pd = pickle.dumps(l)
	self.handler.pinkCommandConnection.transport.write(pd)

    def dataReceived(self, data):
	newList = pickle.loads(data)
	if newList[0]=="pinkGhost":
		gs.pinkGhost.rect = newList[1]
		if newList[2]==1:
			gs.pinkGhost.image = gs.pinkGhost.image_left
		elif newList[2]==0:
			gs.pinkGhost.image=gs.pinkGhost.image_right
		elif newList[2]==2:
			gs.pinkGhost.image=gs.pinkGhost.image_down
		elif newList[2]==3:
			gs.pinkGhost.image=gs.pinkGhost.image_up

class pinkCommandFactory(Factory):

    def __init__(self, handler):
	self.handler = handler

    def buildProtocol(self, addr):
	return pinkCommand(self.handler)

class orangeCommand(LineReceiver):

    def __init__(self, handler):
        self.handler = handler

    def connectionMade(self):
	gs.orangeGhost.automate=0
	gs.orangeGhost.automate=0
	self.handler.orangeCommandConnection = self
	l=[gs.orangeGhost.rect,gs.player.rect, gs.dotList,gs.big_dotList, gs.score]
	pd = pickle.dumps(l)
	self.handler.orangeCommandConnection.transport.write(pd)

    def dataReceived(self, data):
	newList = pickle.loads(data)
	if newList[0]=="orangeGhost":
		gs.orangeGhost.rect = newList[1]
		if newList[2]==1:
			gs.orangeGhost.image = gs.orangeGhost.image_left
		elif newList[2]==0:
			gs.orangeGhost.image=gs.orangeGhost.image_right
		elif newList[2]==2:
			gs.orangeGhost.image=gs.orangeGhost.image_down
		elif newList[2]==3:
			gs.orangeGhost.image=gs.orangeGhost.image_up

class orangeCommandFactory(Factory):

    def __init__(self, handler):
	self.handler = handler

    def buildProtocol(self, addr):
	return orangeCommand(self.handler)


class Start(pygame.sprite.Sprite):
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/start.png"
		self.image = pygame.image.load(FILE)
		self.rect = self.image.get_rect()	
		self.rect.x = -50
		self.rect.y = 30
		self.image = pygame.transform.scale(self.image, (int(900),int(650)))
		
class Background(pygame.sprite.Sprite):
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/board.png"
		self.image = pygame.image.load(FILE)
		self.rect = self.image.get_rect()

class Dot_Small(pygame.sprite.Sprite):
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/dot.png"
		self.image = pygame.image.load(FILE)
		self.image = pygame.transform.scale(self.image, (int(10),int(10)))
		self.rect = self.image.get_rect()
		
		self.rect.x = 145
		self.rect.y = 85

class dot:
	def __init__(self, xPos, yPos):
		self.x = xPos
		self.y = yPos
		self.visible = 1;

class Dot_Big(pygame.sprite.Sprite):
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/dot.png"
		self.image = pygame.image.load(FILE)
		self.image = pygame.transform.scale(self.image, (int(20),int(20)))
		self.rect = self.image.get_rect()
		
		self.rect.x = 143
		self.rect.y = 82

class Life(pygame.sprite.Sprite):
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/life.png"
		self.image = pygame.image.load(FILE)
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.rect = self.image.get_rect()
		
		self.rect.x = 300
		self.rect.y = 18
		
class blueGhost(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.alive = 1
		self.num = 6
		self.gs = gs
		FILE1 = "images/blue_ghost_down.png"
		FILE2 = "images/blue_ghost_up.png"
		FILE3 = "images/blue_ghost_left.png"
		FILE4 = "images/blue_ghost_right.png"
		FILE5 = "images/possessed_ghost.png"
		self.image_possessed = pygame.image.load(FILE5)
		self.image = pygame.image.load(FILE1) #filled in pacman image
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_down = self.image # hold on to original ghost image facing down
		self.image_up = pygame.image.load(FILE2)
		self.image_right = pygame.image.load(FILE4)
		self.image_left = pygame.image.load(FILE3)
		self.image_right = pygame.transform.scale(self.image_right, (int(30),int(30)))
		self.image_up = pygame.transform.scale(self.image_up, (int(30),int(30)))
		self.image_left = pygame.transform.scale(self.image_left, (int(30),int(30)))
		self.image_possessed = pygame.transform.scale(self.image_possessed, (int(30),int(30)))

		self.last_key = "right"
		
		self.rect = self.image.get_rect()
		self.rect.x = 372
		self.rect.y = 353
		self.tempRectX = self.rect.x
		self.tempRectY = self.rect.y
		self.direction = "none"
		self.count = 0

		self.automate=1

	def validMove(self, x, y):
		#lower right half of board start
		if y>633:
			return 0
		elif x>476 and x<532 and y>333 and y<453:
			return 0
		elif x> 416 and x<532 and y>453 and y<513:
			return 0
		elif (y>453 and y<513 and x>536 and x<636) or (y>481 and y<573 and x>536 and x<596):
			return 0
		elif (y>513 and y<573 and x>596):
			return 0
		elif (y>573 and y<633 and x>416 and x<636) or (x<532 and x>476 and y>513 and y<609):
			return 0
		elif (y<633 and y>537 and x<416 and x>352) or (y>513 and y<572 and x>296 and x<476):
			return 0
		elif (x<416 and x>356 and y<513 and y>421) or (y>393 and y<453 and x>296 and x<476):
			return 0
		#lower right half of board end
		#lower left half of board start
		elif ((x<= 292 and x>= 237) and (y>= 332 and y <=449)):
			return 0
		elif ((x>=237 and x<=355) and (y>=454 and y<=512)):
			return 0
		elif ((x<=131) and (y>=452 and y<= 514)):
			return 0
		elif (( x>= 137 and x <=177) and (y>=454 and y<=512)):
			return 0
		elif ((x>=177 and x<=231) and (y>=454 and y<=572)):
			return 0
		elif ((x <= 171) and (y >= 516 and y<= 572)):
			return 0
		elif ((x<= 131) and (y >= 573)):
			return 0
		elif ((x >= 237 and x<= 291) and (y>= 516 and y<= 629)):
			return 0
		elif ((x>= 137 and x<=351) and (y<=632 and y>=578)):
			return 0
		#lower left half of board end
		#middle of board start
		elif ((x>=297 and x<=471) and (y>=274 and y<=392)):
			return 0
		#middle of board end
		#start upper left half
		elif ((x>= 237 and x <= 291) and (y<=326 and y>=154)):
			return 0
		elif ((x >=237 and x<= 349) and (y>=216 and y <=268)):
			return 0
		elif ((x>=137 and x <=231) and (y<=208 and y>=154)):
			return 0
		elif ((x>=137 and x<=231)and (y<=148 and y>=74)):
			return 0
		elif ((x>=237 and x<=351) and (y<=148 and y>=74)):
			return 0
		elif (y<=68):
			return 0
		elif ((x>=357 and x<= 411) and (y<= 148)):
			return 0
		#end upper left half
		#start upper right half of board
		elif ((x>=417 and x<=531) and (y<=148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y<= 148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y>=154 and y<=208)):
			return 0
		elif ((x>=297 and x<=471) and (y>=154 and y<=212)):
			return 0
		elif ((x>=357 and x<=411) and (y<=268 and y>=176)):
			return 0
		elif ((x>=477 and x<=531) and (y>=154 and y<=328)):
			return 0
		elif ((x>=417 and x<=512) and (y>=214 and y<=268)):
			return 0
		#right half board end
		elif ((x>= 644) and (y<= 218 and y >= 64 )):
			return 0
		#the side tunnels
		elif (((x>=-36 and x<= 230)or(x<= 800 and x >= 540)) and ((y>=214 and y<= 325 ) or ((y <= 452 )and y >= 334))):
			return 0
		elif ((x>= 640) and (y>= 417 and y <= 660 )):
			return 0
		elif ((x<= 131) and (y>= 60 and y<= 215 )):
			return 0
		else:
			return 1
		
				
	def move(self):

	
		randomNumber = random.randrange(0,4)
		
		if (self.rect.x>803):
			self.rect.x = -36
		
		if (self.rect.x < -38):
			self.rect.x = 800
		
		if self.rect.y<305 and self.rect.y>261 and self.rect.x>365 and self.rect.y<416:
			while randomNumber == 2 or randomNumber == 3:
				randomNumber = random.randrange(0,4)
		if self.count<70:
			self.count = self.count+1
		elif self.count==70:
			self.count=0
		if self.rect.x >298 and self.rect.x<378 and self.rect.y < 385 and self.rect.y>284:
			self.image = self.image_right
			self.rect.x = self.rect.x+4
		if self.rect.x>365 and self.rect.x<416 and self.rect.y < 395 and self.rect.y>272:
			self.image = self.image_up
			self.rect.y= self.rect.y-4
		else:
			if (self.count==0 and randomNumber == 0 and self.validMove(self.rect.x-1,self.rect.y)) or (self.count!=0 and self.direction=="left" and self.validMove(self.rect.x-1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_left
				self.rect.x = self.rect.x-4
				self.direction = "left"
			elif (self.count==0 and randomNumber == 1 and self.validMove(self.rect.x+1,self.rect.y))or (self.count!=0 and self.direction=="right"and self.validMove(self.rect.x+1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_right
				self.rect.x = self.rect.x+4
				self.direction="right"
			elif (self.count == 0 and randomNumber == 2 and self.validMove(self.rect.x, self.rect.y-1)) or (self.count!=0 and self.direction=="up"and self.validMove(self.rect.x, self.rect.y-1)):
				if self.gs.edible==0:
					self.image = self.image_up
				self.rect.y = self.rect.y-4
				self.direction="up"
			elif (self.count == 0 and randomNumber == 3 and self.validMove(self.rect.x,self.rect.y+1)) or (self.count!=0 and self.direction=="down"and self.validMove(self.rect.x,self.rect.y+1)):
				if self.gs.edible==0:
					self.image = self.image_down
				self.rect.y = self.rect.y+4
				self.direction="down"
			
				
		return
		
	def tick(self):
		if self.alive == 0:
			#ghost is dead
			if self.num < 11:
				#print "Here"
				if self.num !=7:
					#print "Here"
					self.image = pygame.image.load("images/death_%d.png" % self.num)
					self.image = pygame.transform.scale(self.image, (int(30),int(30)))
				self.num+=1
				
		if self.alive != 0: 
			if self.gs.edible>120:
				self.image = self.image_possessed
			elif self.gs.edible<120 and self.gs.edible>110:
				self.image = self.image_down
			elif self.gs.edible<110 and self.gs.edible>100:
				self.image = self.image_possessed
			elif self.gs.edible<100 and self.gs.edible>90:
				self.image = self.image_down
			elif self.gs.edible<90 and self.gs.edible>80:
				self.image = self.image_possessed
			elif self.gs.edible<80 and self.gs.edible>70:
				self.image = self.image_down
			elif self.gs.edible<70 and self.gs.edible>60:
				self.image = self.image_possessed
			elif self.gs.edible<60 and self.gs.edible>50:
				self.image = self.image_down
			elif self.gs.edible<50 and self.gs.edible>40:
				self.image = self.image_possessed
			elif self.gs.edible<30 and self.gs.edible>20:
				self.image = self.image_down
			elif self.gs.edible<20 and self.gs.edible>10:
				self.image = self.image_possessed
			elif self.gs.edible<10 and self.gs.edible!=0:
				self.image = self.image_down
			
			if self.automate==1:
				self.move()			

			

		if self.gs.edible != 0:
			self.gs.edible -= 1


			
		return

class orangeGhost(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.alive = 1
		self.num = 6
		self.gs = gs
		FILE1 = "images/orange_ghost_down.png"
		FILE2 = "images/orange_ghost_up.png"
		FILE3 = "images/orange_ghost_left.png"
		FILE4 = "images/orange_ghost_right.png"
		FILE5 = "images/possessed_ghost.png"
		self.image_possessed = pygame.image.load(FILE5)
		self.image = pygame.image.load(FILE1) #filled in pacman image
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_down = self.image # hold on to original ghost image facing down
		self.image_up = pygame.image.load(FILE2)
		self.image_right = pygame.image.load(FILE4)
		self.image_left = pygame.image.load(FILE3)
		self.image_right = pygame.transform.scale(self.image_right, (int(30),int(30)))
		self.image_up = pygame.transform.scale(self.image_up, (int(30),int(30)))
		self.image_left = pygame.transform.scale(self.image_left, (int(30),int(30)))
		self.image_possessed = pygame.transform.scale(self.image_possessed, (int(30),int(30)))

		self.last_key = "right"
		
		self.rect = self.image.get_rect()
		self.rect.x = 340
		self.rect.y = 353
		self.tempRectX = self.rect.x
		self.tempRectY = self.rect.y
		self.direction = "none"
		self.count = 0

		self.automate=1

	def validMove(self, x, y):
		#lower right half of board start
		if y>633:
			return 0
		elif x>476 and x<532 and y>333 and y<453:
			return 0
		elif x> 416 and x<532 and y>453 and y<513:
			return 0
		elif (y>453 and y<513 and x>536 and x<636) or (y>481 and y<573 and x>536 and x<596):
			return 0
		elif (y>513 and y<573 and x>596):
			return 0
		elif (y>573 and y<633 and x>416 and x<636) or (x<532 and x>476 and y>513 and y<609):
			return 0
		elif (y<633 and y>537 and x<416 and x>352) or (y>513 and y<572 and x>296 and x<476):
			return 0
		elif (x<416 and x>356 and y<513 and y>421) or (y>393 and y<453 and x>296 and x<476):
			return 0
		#lower right half of board end
		#lower left half of board start
		elif ((x<= 292 and x>= 237) and (y>= 332 and y <=449)):
			return 0
		elif ((x>=237 and x<=355) and (y>=454 and y<=512)):
			return 0
		elif ((x<=131) and (y>=452 and y<= 514)):
			return 0
		elif (( x>= 137 and x <=177) and (y>=454 and y<=512)):
			return 0
		elif ((x>=177 and x<=231) and (y>=454 and y<=572)):
			return 0
		elif ((x <= 171) and (y >= 516 and y<= 572)):
			return 0
		elif ((x<= 131) and (y >= 573)):
			return 0
		elif ((x >= 237 and x<= 291) and (y>= 516 and y<= 629)):
			return 0
		elif ((x>= 137 and x<=351) and (y<=632 and y>=578)):
			return 0
		#lower left half of board end
		#middle of board start
		elif ((x>=297 and x<=471) and (y>=274 and y<=392)):
			return 0
		#middle of board end
		#start upper left half
		elif ((x>= 237 and x <= 291) and (y<=326 and y>=154)):
			return 0
		elif ((x >=237 and x<= 349) and (y>=216 and y <=268)):
			return 0
		elif ((x>=137 and x <=231) and (y<=208 and y>=154)):
			return 0
		elif ((x>=137 and x<=231)and (y<=148 and y>=74)):
			return 0
		elif ((x>=237 and x<=351) and (y<=148 and y>=74)):
			return 0
		elif (y<=68):
			return 0
		elif ((x>=357 and x<= 411) and (y<= 148)):
			return 0
		#end upper left half
		#start upper right half of board
		elif ((x>=417 and x<=531) and (y<=148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y<= 148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y>=154 and y<=208)):
			return 0
		elif ((x>=297 and x<=471) and (y>=154 and y<=212)):
			return 0
		elif ((x>=357 and x<=411) and (y<=268 and y>=176)):
			return 0
		elif ((x>=477 and x<=531) and (y>=154 and y<=328)):
			return 0
		elif ((x>=417 and x<=512) and (y>=214 and y<=268)):
			return 0
		#right half board end
		elif ((x>= 644) and (y<= 218 and y >= 64 )):
			return 0
		#the side tunnels
		elif (((x>=-36 and x<= 230)or(x<= 800 and x >= 540)) and ((y>=214 and y<= 325 ) or ((y <= 452 )and y >= 334))):
			return 0
		elif ((x>= 640) and (y>= 417 and y <= 660 )):
			return 0
		elif ((x<= 131) and (y>= 60 and y<= 215 )):
			return 0
		else:
			return 1
		
				
	def move(self):

	
		randomNumber = random.randrange(0,4)
		
		if (self.rect.x>803):
			self.rect.x = -36
		
		if (self.rect.x < -38):
			self.rect.x = 800
		
		if self.rect.y<305 and self.rect.y>261 and self.rect.x>365 and self.rect.y<416:
			while randomNumber == 2 or randomNumber == 3:
				randomNumber = random.randrange(0,4)
		if self.count<70:
			self.count = self.count+1
		elif self.count==70:
			self.count=0
		if self.rect.x >298 and self.rect.x<378 and self.rect.y < 385 and self.rect.y>284:
			self.image = self.image_right
			self.rect.x = self.rect.x+4
		if self.rect.x>365 and self.rect.x<416 and self.rect.y < 395 and self.rect.y>272:
			self.image = self.image_up
			self.rect.y= self.rect.y-4
		else:
			if (self.count==0 and randomNumber == 0 and self.validMove(self.rect.x-1,self.rect.y)) or (self.count!=0 and self.direction=="left" and self.validMove(self.rect.x-1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_left
				self.rect.x = self.rect.x-4
				self.direction = "left"
			elif (self.count==0 and randomNumber == 1 and self.validMove(self.rect.x+1,self.rect.y))or (self.count!=0 and self.direction=="right"and self.validMove(self.rect.x+1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_right
				self.rect.x = self.rect.x+4
				self.direction="right"
			elif (self.count == 0 and randomNumber == 2 and self.validMove(self.rect.x, self.rect.y-1)) or (self.count!=0 and self.direction=="up"and self.validMove(self.rect.x, self.rect.y-1)):
				if self.gs.edible==0:
					self.image = self.image_up
				self.rect.y = self.rect.y-4
				self.direction="up"
			elif (self.count == 0 and randomNumber == 3 and self.validMove(self.rect.x,self.rect.y+1)) or (self.count!=0 and self.direction=="down"and self.validMove(self.rect.x,self.rect.y+1)):
				if self.gs.edible==0:
					self.image = self.image_down
				self.rect.y = self.rect.y+4
				self.direction="down"
			
				
		return
		
	def tick(self):
		if self.alive == 0:
			#ghost is dead
			if self.num < 11:
				#print "Here"
				if self.num !=7:
					#print "Here"
					self.image = pygame.image.load("images/death_%d.png" % self.num)
					self.image = pygame.transform.scale(self.image, (int(30),int(30)))
				self.num+=1
				
		if self.alive != 0: 
			if self.gs.edible>120:
				self.image = self.image_possessed
			elif self.gs.edible<120 and self.gs.edible>110:
				self.image = self.image_down
			elif self.gs.edible<110 and self.gs.edible>100:
				self.image = self.image_possessed
			elif self.gs.edible<100 and self.gs.edible>90:
				self.image = self.image_down
			elif self.gs.edible<90 and self.gs.edible>80:
				self.image = self.image_possessed
			elif self.gs.edible<80 and self.gs.edible>70:
				self.image = self.image_down
			elif self.gs.edible<70 and self.gs.edible>60:
				self.image = self.image_possessed
			elif self.gs.edible<60 and self.gs.edible>50:
				self.image = self.image_down
			elif self.gs.edible<50 and self.gs.edible>40:
				self.image = self.image_possessed
			elif self.gs.edible<30 and self.gs.edible>20:
				self.image = self.image_down
			elif self.gs.edible<20 and self.gs.edible>10:
				self.image = self.image_possessed
			elif self.gs.edible<10 and self.gs.edible!=0:
				self.image = self.image_down
			
			if self.automate==1:
				self.move()			

			

		if self.gs.edible != 0:
			self.gs.edible -= 1


			
		return

class redGhost(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.alive = 1
		self.num = 6
		self.gs = gs
		FILE1 = "images/red_ghost_down.png"
		FILE2 = "images/red_ghost_up.png"
		FILE3 = "images/red_ghost_left.png"
		FILE4 = "images/red_ghost_right.png"
		FILE5 = "images/possessed_ghost.png"
		self.image_possessed = pygame.image.load(FILE5)
		self.image = pygame.image.load(FILE1) #filled in pacman image
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_down = self.image # hold on to original ghost image facing down
		self.image_up = pygame.image.load(FILE2)
		self.image_right = pygame.image.load(FILE4)
		self.image_left = pygame.image.load(FILE3)
		self.image_right = pygame.transform.scale(self.image_right, (int(30),int(30)))
		self.image_up = pygame.transform.scale(self.image_up, (int(30),int(30)))
		self.image_left = pygame.transform.scale(self.image_left, (int(30),int(30)))
		self.image_possessed = pygame.transform.scale(self.image_possessed, (int(30),int(30)))
		
		self.last_key = "right"
		
		self.rect = self.image.get_rect()
		self.rect.x = 356
		self.rect.y = 357
		self.tempRectX = self.rect.x
		self.tempRectY = self.rect.y
		self.direction = "none"
		self.count = 0

		self.automate=1

	def validMove(self, x, y):
		#lower right half of board start
		if y>633:
			return 0
		elif x>476 and x<532 and y>333 and y<453:
			return 0
		elif x> 416 and x<532 and y>453 and y<513:
			return 0
		elif (y>453 and y<513 and x>536 and x<636) or (y>481 and y<573 and x>536 and x<596):
			return 0
		elif (y>513 and y<573 and x>596):
			return 0
		elif (y>573 and y<633 and x>416 and x<636) or (x<532 and x>476 and y>513 and y<609):
			return 0
		elif (y<633 and y>537 and x<416 and x>352) or (y>513 and y<572 and x>296 and x<476):
			return 0
		elif (x<416 and x>356 and y<513 and y>421) or (y>393 and y<453 and x>296 and x<476):
			return 0
		#lower right half of board end
		#lower left half of board start
		elif ((x<= 292 and x>= 237) and (y>= 332 and y <=449)):
			return 0
		elif ((x>=237 and x<=355) and (y>=454 and y<=512)):
			return 0
		elif ((x<=131) and (y>=452 and y<= 514)):
			return 0
		elif (( x>= 137 and x <=177) and (y>=454 and y<=512)):
			return 0
		elif ((x>=177 and x<=231) and (y>=454 and y<=572)):
			return 0
		elif ((x <= 171) and (y >= 516 and y<= 572)):
			return 0
		elif ((x<= 131) and (y >= 573)):
			return 0
		elif ((x >= 237 and x<= 291) and (y>= 516 and y<= 629)):
			return 0
		elif ((x>= 137 and x<=351) and (y<=632 and y>=578)):
			return 0
		#lower left half of board end
		#middle of board start
		elif ((x>=297 and x<=471) and (y>=274 and y<=392)):
			return 0
		#middle of board end
		#start upper left half
		elif ((x>= 237 and x <= 291) and (y<=326 and y>=154)):
			return 0
		elif ((x >=237 and x<= 349) and (y>=216 and y <=268)):
			return 0
		elif ((x>=137 and x <=231) and (y<=208 and y>=154)):
			return 0
		elif ((x>=137 and x<=231)and (y<=148 and y>=74)):
			return 0
		elif ((x>=237 and x<=351) and (y<=148 and y>=74)):
			return 0
		elif (y<=68):
			return 0
		elif ((x>=357 and x<= 411) and (y<= 148)):
			return 0
		#end upper left half
		#start upper right half of board
		elif ((x>=417 and x<=531) and (y<=148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y<= 148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y>=154 and y<=208)):
			return 0
		elif ((x>=297 and x<=471) and (y>=154 and y<=212)):
			return 0
		elif ((x>=357 and x<=411) and (y<=268 and y>=176)):
			return 0
		elif ((x>=477 and x<=531) and (y>=154 and y<=328)):
			return 0
		elif ((x>=417 and x<=512) and (y>=214 and y<=268)):
			return 0
		#right half board end
		elif ((x>= 644) and (y<= 218 and y >= 64 )):
			return 0
		#the side tunnels
		elif (((x>=-36 and x<= 230)or(x<= 800 and x >= 540)) and ((y>=214 and y<= 325 ) or ((y <= 452 )and y >= 334))):
			return 0
		elif ((x>= 640) and (y>= 417 and y <= 660 )):
			return 0
		elif ((x<= 131) and (y>= 60 and y<= 215 )):
			return 0
		else:
			return 1
		
				
	def move(self):
		if self.last_key == "right":
			self.last_key = K_RIGHT
		elif self.last_key == "left":
			self.last_key = K_LEFT
		elif self.last_key == "up":
			self.last_key = K_UP
		elif self.last_key == "down":
			self.last_key = K_DOWN
		
		randomNumber = random.randrange(0,4)
		
		if randomNumber == 0:
			keycode =K_LEFT
		elif randomNumber == 1:
			keycode = K_RIGHT
		elif randomNumber == 2:
			keycode = K_UP
		else:
			keycode = K_DOWN
		if (keycode == K_RIGHT and self.validMove(self.rect.x+6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_LEFT and self.validMove(self.rect.x-6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_UP and self.validMove(self.rect.x, self.rect.y-6) == 0):
			keycode = self.last_key
		elif (keycode == K_DOWN and self.validMove(self.rect.x, self.rect.y+6) == 0):
			keycode = self.last_key
		
		
		if (self.rect.x>803):
			self.rect.x = -36
		
		if (self.rect.x < -38):
			self.rect.x = 800
		
		if self.rect.y<305 and self.rect.y>261 and self.rect.x>365 and self.rect.y<416:
			while randomNumber == 2 or randomNumber == 3:
				randomNumber = random.randrange(0,4)
		if self.count<70:
			self.count = self.count+1
		elif self.count==70:
			self.count=0
		if self.rect.x >298 and self.rect.x<378 and self.rect.y < 385 and self.rect.y>284:
			self.image = self.image_right
			self.rect.x = self.rect.x+4
		if self.rect.x>365 and self.rect.x<416 and self.rect.y < 395 and self.rect.y>272:
			self.image = self.image_up
			self.rect.y= self.rect.y-4
		else:
			if (self.count==0 and randomNumber == 0 and self.validMove(self.rect.x-1,self.rect.y)) or (self.count!=0 and self.direction=="left" and self.validMove(self.rect.x-1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_left
				self.rect.x = self.rect.x-4
				self.direction = "left"
			elif (self.count==0 and randomNumber == 1 and self.validMove(self.rect.x+1,self.rect.y))or (self.count!=0 and self.direction=="right"and self.validMove(self.rect.x+1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_right
				self.rect.x = self.rect.x+4
				self.direction="right"
			elif (self.count == 0 and randomNumber == 2 and self.validMove(self.rect.x, self.rect.y-1)) or (self.count!=0 and self.direction=="up"and self.validMove(self.rect.x, self.rect.y-1)):
				if self.gs.edible==0:
					self.image = self.image_up
				self.rect.y = self.rect.y-4
				self.direction="up"
			elif (self.count == 0 and randomNumber == 3 and self.validMove(self.rect.x,self.rect.y+1)) or (self.count!=0 and self.direction=="down"and self.validMove(self.rect.x,self.rect.y+1)):
				if self.gs.edible==0:
					self.image = self.image_down
				self.rect.y = self.rect.y+4
				self.direction="down"
			
				
		return
		
	def tick(self):
		if self.alive == 0:
			#ghost is dead
			if self.num < 11:
				if self.num !=7:
					self.image = pygame.image.load("images/death_%d.png" % self.num)
					self.image = pygame.transform.scale(self.image, (int(30),int(30)))
				self.num+=1
				
		if self.alive != 0: 
			if self.gs.edible>120:
				self.image = self.image_possessed
			elif self.gs.edible<120 and self.gs.edible>110:
				self.image = self.image_down
			elif self.gs.edible<110 and self.gs.edible>100:
				self.image = self.image_possessed
			elif self.gs.edible<100 and self.gs.edible>90:
				self.image = self.image_down
			elif self.gs.edible<90 and self.gs.edible>80:
				self.image = self.image_possessed
			elif self.gs.edible<80 and self.gs.edible>70:
				self.image = self.image_down
			elif self.gs.edible<70 and self.gs.edible>60:
				self.image = self.image_possessed
			elif self.gs.edible<60 and self.gs.edible>50:
				self.image = self.image_down
			elif self.gs.edible<50 and self.gs.edible>40:
				self.image = self.image_possessed
			elif self.gs.edible<30 and self.gs.edible>20:
				self.image = self.image_down
			elif self.gs.edible<20 and self.gs.edible>10:
				self.image = self.image_possessed
			elif self.gs.edible<10 and self.gs.edible!=0:
				self.image = self.image_down
			
			if self.automate==1:
				self.move()			

			

		if self.gs.edible != 0:
			self.gs.edible -= 1


			
		return



class pinkGhost(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.alive = 1
		self.num = 6
		self.gs = gs
		FILE1 = "images/pink_ghost_down.png"
		FILE2 = "images/pink_ghost_up.png"
		FILE3 = "images/pink_ghost_left.png"
		FILE4 = "images/pink_ghost_right.png"
		FILE5 = "images/possessed_ghost.png"
		self.image_possessed = pygame.image.load(FILE5)
		self.image = pygame.image.load(FILE1) #filled in pacman image
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_down = self.image # hold on to original ghost image facing down
		self.image_up = pygame.image.load(FILE2)
		self.image_right = pygame.image.load(FILE4)
		self.image_left = pygame.image.load(FILE3)
		self.image_right = pygame.transform.scale(self.image_right, (int(30),int(30)))
		self.image_up = pygame.transform.scale(self.image_up, (int(30),int(30)))
		self.image_left = pygame.transform.scale(self.image_left, (int(30),int(30)))
		self.image_possessed = pygame.transform.scale(self.image_possessed, (int(30),int(30)))
		
		self.last_key = "right"
		
		self.rect = self.image.get_rect()
		self.rect.x = 352
		self.rect.y = 357
		self.tempRectX = self.rect.x
		self.tempRectY = self.rect.y
		self.direction = "none"
		self.count = 0

		self.automate=1

	def validMove(self, x, y):
		#lower right half of board start
		if y>633:
			return 0
		elif x>476 and x<532 and y>333 and y<453:
			return 0
		elif x> 416 and x<532 and y>453 and y<513:
			return 0
		elif (y>453 and y<513 and x>536 and x<636) or (y>481 and y<573 and x>536 and x<596):
			return 0
		elif (y>513 and y<573 and x>596):
			return 0
		elif (y>573 and y<633 and x>416 and x<636) or (x<532 and x>476 and y>513 and y<609):
			return 0
		elif (y<633 and y>537 and x<416 and x>352) or (y>513 and y<572 and x>296 and x<476):
			return 0
		elif (x<416 and x>356 and y<513 and y>421) or (y>393 and y<453 and x>296 and x<476):
			return 0
		#lower right half of board end
		#lower left half of board start
		elif ((x<= 292 and x>= 237) and (y>= 332 and y <=449)):
			return 0
		elif ((x>=237 and x<=355) and (y>=454 and y<=512)):
			return 0
		elif ((x<=131) and (y>=452 and y<= 514)):
			return 0
		elif (( x>= 137 and x <=177) and (y>=454 and y<=512)):
			return 0
		elif ((x>=177 and x<=231) and (y>=454 and y<=572)):
			return 0
		elif ((x <= 171) and (y >= 516 and y<= 572)):
			return 0
		elif ((x<= 131) and (y >= 573)):
			return 0
		elif ((x >= 237 and x<= 291) and (y>= 516 and y<= 629)):
			return 0
		elif ((x>= 137 and x<=351) and (y<=632 and y>=578)):
			return 0
		#lower left half of board end
		#middle of board start
		elif ((x>=297 and x<=471) and (y>=274 and y<=392)):
			return 0
		#middle of board end
		#start upper left half
		elif ((x>= 237 and x <= 291) and (y<=326 and y>=154)):
			return 0
		elif ((x >=237 and x<= 349) and (y>=216 and y <=268)):
			return 0
		elif ((x>=137 and x <=231) and (y<=208 and y>=154)):
			return 0
		elif ((x>=137 and x<=231)and (y<=148 and y>=74)):
			return 0
		elif ((x>=237 and x<=351) and (y<=148 and y>=74)):
			return 0
		elif (y<=68):
			return 0
		elif ((x>=357 and x<= 411) and (y<= 148)):
			return 0
		#end upper left half
		#start upper right half of board
		elif ((x>=417 and x<=531) and (y<=148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y<= 148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y>=154 and y<=208)):
			return 0
		elif ((x>=297 and x<=471) and (y>=154 and y<=212)):
			return 0
		elif ((x>=357 and x<=411) and (y<=268 and y>=176)):
			return 0
		elif ((x>=477 and x<=531) and (y>=154 and y<=328)):
			return 0
		elif ((x>=417 and x<=512) and (y>=214 and y<=268)):
			return 0
		#right half board end
		elif ((x>= 644) and (y<= 218 and y >= 64 )):
			return 0
		#the side tunnels
		elif (((x>=-36 and x<= 230)or(x<= 800 and x >= 540)) and ((y>=214 and y<= 325 ) or ((y <= 452 )and y >= 334))):
			return 0
		elif ((x>= 640) and (y>= 417 and y <= 660 )):
			return 0
		elif ((x<= 131) and (y>= 60 and y<= 215 )):
			return 0
		else:
			return 1
		
				
	def move(self):
		if self.last_key == "right":
			self.last_key = K_RIGHT
		elif self.last_key == "left":
			self.last_key = K_LEFT
		elif self.last_key == "up":
			self.last_key = K_UP
		elif self.last_key == "down":
			self.last_key = K_DOWN
		
		randomNumber = random.randrange(0,4)
		
		if randomNumber == 0:
			keycode =K_LEFT
		elif randomNumber == 1:
			keycode = K_RIGHT
		elif randomNumber == 2:
			keycode = K_UP
		else:
			keycode = K_DOWN
		if (keycode == K_RIGHT and self.validMove(self.rect.x+6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_LEFT and self.validMove(self.rect.x-6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_UP and self.validMove(self.rect.x, self.rect.y-6) == 0):
			keycode = self.last_key
		elif (keycode == K_DOWN and self.validMove(self.rect.x, self.rect.y+6) == 0):
			keycode = self.last_key
		
		
		if (self.rect.x>803):
			self.rect.x = -36
		
		if (self.rect.x < -38):
			self.rect.x = 800
		
		if self.rect.y<305 and self.rect.y>261 and self.rect.x>365 and self.rect.y<416:
			while randomNumber == 2 or randomNumber == 3:
				randomNumber = random.randrange(0,4)
		if self.count<70:
			self.count = self.count+1
		elif self.count==70:
			self.count=0
		if self.rect.x >298 and self.rect.x<378 and self.rect.y < 385 and self.rect.y>284:
			self.image = self.image_right
			self.rect.x = self.rect.x+4
		if self.rect.x>365 and self.rect.x<416 and self.rect.y < 395 and self.rect.y>272:
			self.image = self.image_up
			self.rect.y= self.rect.y-4
		else:
			if (self.count==0 and randomNumber == 0 and self.validMove(self.rect.x-1,self.rect.y)) or (self.count!=0 and self.direction=="left" and self.validMove(self.rect.x-1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_left
				self.rect.x = self.rect.x-4
				self.direction = "left"
			elif (self.count==0 and randomNumber == 1 and self.validMove(self.rect.x+1,self.rect.y))or (self.count!=0 and self.direction=="right"and self.validMove(self.rect.x+1,self.rect.y)):
				if self.gs.edible==0:
					self.image = self.image_right
				self.rect.x = self.rect.x+4
				self.direction="right"
			elif (self.count == 0 and randomNumber == 2 and self.validMove(self.rect.x, self.rect.y-1)) or (self.count!=0 and self.direction=="up"and self.validMove(self.rect.x, self.rect.y-1)):
				if self.gs.edible==0:
					self.image = self.image_up
				self.rect.y = self.rect.y-4
				self.direction="up"
			elif (self.count == 0 and randomNumber == 3 and self.validMove(self.rect.x,self.rect.y+1)) or (self.count!=0 and self.direction=="down"and self.validMove(self.rect.x,self.rect.y+1)):
				if self.gs.edible==0:
					self.image = self.image_down
				self.rect.y = self.rect.y+4
				self.direction="down"
			
				
		return
		
	def tick(self):
		if self.alive == 0:
			#ghost is dead
			if self.num < 11:
				if self.num !=7:
					self.image = pygame.image.load("images/death_%d.png" % self.num)
					self.image = pygame.transform.scale(self.image, (int(30),int(30)))
				self.num+=1
				
		if self.alive != 0: 
			if self.gs.edible>120:
				self.image = self.image_possessed
			elif self.gs.edible<120 and self.gs.edible>110:
				self.image = self.image_down
			elif self.gs.edible<110 and self.gs.edible>100:
				self.image = self.image_possessed
			elif self.gs.edible<100 and self.gs.edible>90:
				self.image = self.image_down
			elif self.gs.edible<90 and self.gs.edible>80:
				self.image = self.image_possessed
			elif self.gs.edible<80 and self.gs.edible>70:
				self.image = self.image_down
			elif self.gs.edible<70 and self.gs.edible>60:
				self.image = self.image_possessed
			elif self.gs.edible<60 and self.gs.edible>50:
				self.image = self.image_down
			elif self.gs.edible<50 and self.gs.edible>40:
				self.image = self.image_possessed
			elif self.gs.edible<30 and self.gs.edible>20:
				self.image = self.image_down
			elif self.gs.edible<20 and self.gs.edible>10:
				self.image = self.image_possessed
			elif self.gs.edible<10 and self.gs.edible!=0:
				self.image = self.image_down
			
			if self.automate==1:
				self.move()			

			

		if self.gs.edible != 0:
			self.gs.edible -= 1


			
		return




		
class Player(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.num = 1
		self.alive = 1
		self.gs = gs
		FILE = "images/pacman.png"
		FILE2 = "images/packman_full.png"
		self.image = pygame.image.load(FILE) #filled in pacman image
		self.image_full = pygame.image.load(FILE2)
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_full = pygame.transform.scale(self.image_full, (int(30),int(30)))
		self.orig_image = self.image # hold on to original pacman image facing right
		
		self.image_right = self.image
		self.image_left = pygame.transform.rotate(self.orig_image, 180)
		self.image_up = pygame.transform.rotate(self.orig_image, 90)
		self.image_down = pygame.transform.rotate(self.orig_image, 270)
		
		self.rect = self.image.get_rect()
		self.rect.x = 392
		self.rect.y = 513
		self.orientation = "full"
		self.last_key = "left"
		self.count = 0
		self.l = ["pacman", self.rect, self.image]

	def validMove(self, x, y):
		#lower right half of board start
		if y>633:
			return 0
		elif x>476 and x<532 and y>333 and y<453:
			return 0
		elif x> 416 and x<532 and y>453 and y<513:
			return 0
		elif (y>453 and y<513 and x>536 and x<636) or (y>481 and y<573 and x>536 and x<596):
			return 0
		elif (y>513 and y<573 and x>596):
			return 0
		elif (y>573 and y<633 and x>416 and x<636) or (x<532 and x>476 and y>513 and y<609):
			return 0
		elif (y<633 and y>537 and x<416 and x>352) or (y>513 and y<572 and x>296 and x<476):
			return 0
		elif (x<416 and x>356 and y<513 and y>421) or (y>393 and y<453 and x>296 and x<476):
			return 0
		#lower right half of board end
		#lower left half of board start
		elif ((x<= 292 and x>= 237) and (y>= 332 and y <=449)):
			return 0
		elif ((x>=237 and x<=355) and (y>=454 and y<=512)):
			return 0
		elif ((x<=131) and (y>=452 and y<= 514)):
			return 0
		elif (( x>= 137 and x <=177) and (y>=454 and y<=512)):
			return 0
		elif ((x>=177 and x<=231) and (y>=454 and y<=572)):
			return 0
		elif ((x <= 171) and (y >= 516 and y<= 572)):
			return 0
		elif ((x<= 131) and (y >= 573)):
			return 0
		elif ((x >= 237 and x<= 291) and (y>= 516 and y<= 629)):
			return 0
		elif ((x>= 137 and x<=351) and (y<=632 and y>=578)):
			return 0
		#lower left half of board end
		#middle of board start
		elif ((x>=297 and x<=471) and (y>=274 and y<=392)):
			return 0
		#middle of board end
		#start upper left half
		elif ((x>= 237 and x <= 291) and (y<=326 and y>=154)):
			return 0
		elif ((x >=237 and x<= 349) and (y>=216 and y <=268)):
			return 0
		elif ((x>=137 and x <=231) and (y<=208 and y>=154)):
			return 0
		elif ((x>=137 and x<=231)and (y<=148 and y>=74)):
			return 0
		elif ((x>=237 and x<=351) and (y<=148 and y>=74)):
			return 0
		elif (y<=68):
			return 0
		elif ((x>=357 and x<= 411) and (y<= 148)):
			return 0
		#end upper left half
		#start upper right half of board
		elif ((x>=417 and x<=531) and (y<=148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y<= 148 and y>=74)):
			return 0
		elif ((x>=537 and x<=631) and (y>=154 and y<=208)):
			return 0
		elif ((x>=297 and x<=471) and (y>=154 and y<=212)):
			return 0
		elif ((x>=357 and x<=411) and (y<=268 and y>=176)):
			return 0
		elif ((x>=477 and x<=531) and (y>=154 and y<=328)):
			return 0
		elif ((x>=417 and x<=512) and (y>=214 and y<=268)):
			return 0
		#right half board end
		elif ((x>= 644) and (y<= 218 and y >= 64 )):
			return 0
		#the side tunnels
		elif (((x>=-36 and x<= 230)or(x<= 800 and x >= 540)) and ((y>=214 and y<= 325 ) or ((y <= 452 )and y >= 334))):
			return 0
		elif ((x>= 640) and (y>= 417 and y <= 660 )):
			return 0
		elif ((x<= 131) and (y>= 60 and y<= 215 )):
			return 0
		else:
			return 1
		
				
	def move(self, keycode):
		currentx = self.rect.x
		currenty = self.rect.y
		if self.last_key == "right":
			self.last_key = K_RIGHT
		elif self.last_key == "left":
			self.last_key = K_LEFT
		elif self.last_key == "up":
			self.last_key = K_UP
		elif self.last_key == "down":
			self.last_key = K_DOWN
			
		if (keycode == K_RIGHT and self.validMove(self.rect.x+6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_LEFT and self.validMove(self.rect.x-6, self.rect.y) == 0):
			keycode = self.last_key
		elif (keycode == K_UP and self.validMove(self.rect.x, self.rect.y-6) == 0):
			keycode = self.last_key
		elif (keycode == K_DOWN and self.validMove(self.rect.x, self.rect.y+6) == 0):
			keycode = self.last_key
		
		if (keycode == K_RIGHT):
			self.last_key = "right"
			if self.validMove(self.rect.x+4, self.rect.y):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(4, 0)
				if self.orientation != "right":
					self.l = ["pacman",self.rect,0]
					self.image = self.orig_image
					self.orientation = "right"
				elif self.count==1:
					self.l = ["pacman",self.rect,4]
					self.image = self.image_full
					self.orientation = "full"
				if (self.rect.x>803):
					self.rect.x = -36
					
					
			
		if (keycode == K_LEFT):
			self.last_key = "left"
			if self.validMove(self.rect.x-4, self.rect.y):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(-4,0)
				if self.orientation != "left":
					self.l = ["pacman",self.rect,1]
					self.image = pygame.transform.rotate(self.orig_image, 180)
					self.orientation = "left"
				elif self.count==1:
					self.l = ["pacman",self.rect,4]
					self.image = self.image_full
					self.orientation = "full"
				if (self.rect.x < -32):
					self.rect.x = 800
			
		if (keycode == K_DOWN):
			self.last_key = "down"
			if self.validMove(self.rect.x, self.rect.y+4):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(0,4)
				if self.orientation!="down":
					self.l = ["pacman",self.rect,2]
					self.image = pygame.transform.rotate(self.orig_image, 270)
					self.orientation = "down"
				elif self.count == 1:
					self.l = ["pacman",self.rect,4]
					self.image = self.image_full
					self.orientation = "full"
			
		if (keycode == K_UP):
			self.last_key = "up"
			
			if self.validMove(self.rect.x, self.rect.y-4):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(0,-4)
				if self.orientation!="up":
					self.l = ["pacman",self.rect,3]
					self.image = pygame.transform.rotate(self.orig_image, 90)
					self.orientation="up"
				elif self.count == 1:
					self.l = ["pacman",self.rect,4]
					self.image = self.image_full
					self.orientation = "full"

		if self.gs.blueGhost.automate!=1:
			if self.rect.x != currentx or self.rect.y!= currenty:
				pd = pickle.dumps(self.l)
				self.gs.handler.commandConnection.transport.write(pd)

		if self.gs.redGhost.automate!=1:
			if self.rect.x != currentx or self.rect.y!= currenty:
				pd = pickle.dumps(self.l)
				self.gs.handler.redCommandConnection.transport.write(pd)
		return
		
	def tick(self):
		if self.alive == 0:
			if self.num < 9:
				self.image = pygame.image.load("images/death_%d.png" % self.num)
				self.image = pygame.transform.scale(self.image, (int(30),int(30)))
				self.num+=1
			else:
				time.sleep(2) # delays for 2 seconds
				reactor.stop()
		

		
class GameSpace:
	def __init__(self, handler):
		random.seed()
		pygame.init()
		self.stopFlag=0
		self.edible = 0
		self.deathCounter = 0
		self.myfont = pygame.font.SysFont("monospace", 25)

		self.handler = handler
		self.game_screen = 0
		

		#pygame.mixer.pre_init(44100, -16, 2, 2048) #initializing sound
		#pygame.mixer.music.load('./sounds/adjSiren.wav')
		#self.waka = pygame.mixer.Sound('./sounds/waka.wav')
		
		winTitle = pygame.display.set_caption("Paradigms Final Project: Multiplayer Pacman")
		
		self.size = self.width, self.height = 800, 800
		
		self.black = 0, 0, 0
		
		self.screen = pygame.display.set_mode(self.size)
		
		pygame.key.set_repeat(1, 50) #adjust this to make pacman move faster
		
		self.clock = pygame.time.Clock()
		
		self.player = Player(self)
		self.blueGhost = blueGhost(self)
		self.redGhost = redGhost(self)
		self.pinkGhost = pinkGhost(self)
		self.orangeGhost = orangeGhost(self)
		self.background = Background(self)
		self.dot_big = Dot_Big(self)
		self.dot_small = Dot_Small(self)
		self.dot_big = Dot_Big(self)
		self.life = Life(self)
		self.start = Start(self)
		self.dotList=[]
		self.big_dotList=[]
		self.dotCount = 0

		self.score = 0
		

		#Placing all dots
				
		#Row 1#
		i = 0
		while(i<8):
			if (i!=3):
				newdot = dot(self.dot_small.rect.x+3+32*i, self.dot_small.rect.y+0)
				self.dotList.append(newdot)
			if (i!=4):
				newdot = dot(self.dot_small.rect.x+283+30*i, self.dot_small.rect.y+0)
				self.dotList.append(newdot)
			i+=1
		#Row 1 End#
		#Row 2#
		newdot = dot(self.dot_big.rect.x+3, self.dot_big.rect.y+38)
		self.big_dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+219, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+280, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
		newdot = dot(self.dot_big.rect.x+305+32*6, self.dot_big.rect.y+38)
		self.big_dotList.append(newdot)
		#Row 2 End#
		#Row 3#
		i = 0
		while (i<17):
			if (i!=3 and i!= 13):
				newdot = dot(self.dot_small.rect.x+5+31*i, self.dot_small.rect.y+77)
				self.dotList.append(newdot)
			i+=1
		#Row 3 End#
		#Row 4 Start#
		newdot = dot(self.dot_small.rect.x+5, self.dot_small.rect.y+35*3)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+165, self.dot_small.rect.y+35*3)
		self.dotList.append(newdot)	
		newdot = dot(self.dot_small.rect.x+314+32, self.dot_small.rect.y+35*3)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+305+32*6, self.dot_small.rect.y+35*3)
		self.dotList.append(newdot)
		
		#Row 4 End#
		#Row 5 Start#
		i = 0
		while(i<4):
			if (i<3):
				newdot = dot(self.dot_small.rect.x+163+i*27, self.dot_small.rect.y+33*4)
				self.dotList.append(newdot)
				newdot = dot(self.dot_small.rect.x+283+i*32, self.dot_small.rect.y+33*4)
				self.dotList.append(newdot)
			if (i!=3):
				newdot = dot(self.dot_small.rect.x+5+i*32, self.dot_small.rect.y+33*4)
				self.dotList.append(newdot)
			if (i!=0):
				newdot = dot(self.dot_small.rect.x+314+31*(3+i), self.dot_small.rect.y+33*4)
				self.dotList.append(newdot)
			i+=1
		#Row 5 End#
			
		#Row 6 Start#
		newdot = dot(self.dot_small.rect.x+222, self.dot_small.rect.y+33*5)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+283, self.dot_small.rect.y+33*5)
		self.dotList.append(newdot)
		#Row 6 End#
				

		#Row 7
		i = 0
		while (i<8):
			if (i!=3):
				newdot = dot(self.dot_small.rect.x+3+31*i, self.dot_small.rect.y+33*11+16)
				self.dotList.append(newdot)
			if (i!=4):
				newdot = dot(self.dot_small.rect.x+283+31*i, self.dot_small.rect.y+33*11+16)
				self.dotList.append(newdot)				
			i+=1
			
		#Row 8
		newdot = dot(self.dot_small.rect.x+5, self.dot_small.rect.y+33*12+14)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+222, self.dot_small.rect.y+33*12+14)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+283, self.dot_small.rect.y+33*12+14)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+305+32*6, self.dot_small.rect.y+33*12+14)
		self.dotList.append(newdot)
		i = 0
		while(i<16):
			if (i!=2 and i!=3 and i!=8 and i!= 12 and i!=13):
				newdot = dot(self.dot_small.rect.x+5+i*32, self.dot_small.rect.y+33*13+12)
				self.dotList.append(newdot)
			i+=1

		newdot = dot(self.dot_small.rect.x+37, self.dot_small.rect.y+33*14+8)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+165, self.dot_small.rect.y+33*14+8)
		self.dotList.append(newdot)	
		newdot = dot(self.dot_small.rect.x+314+32, self.dot_small.rect.y+33*14+8)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+308+32*5, self.dot_small.rect.y+33*14+8)
		self.dotList.append(newdot)
		i = 0
		while (i<17):
			if (i!=3 and i!=4 and i!=8 and i!=12 and i!=13 ):
				if i==7:
					newdot = dot(self.dot_small.rect.x+i*32, self.dot_small.rect.y+33*15)
					self.dotList.append(newdot)
				elif i>=9:
					newdot = dot(self.dot_small.rect.x+i*32-7, self.dot_small.rect.y+33*15)
					self.dotList.append(newdot)
				else:
					newdot = dot(self.dot_small.rect.x+3+i*32, self.dot_small.rect.y+33*15)
					self.dotList.append(newdot)	
			i+=1

		newdot = dot(self.dot_big.rect.x+3, self.dot_big.rect.y+33*16)
		self.big_dotList.append(newdot)	
		newdot = dot(self.dot_small.rect.x+217, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+278, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)
		newdot = dot(self.dot_big.rect.x+300+32*6, self.dot_big.rect.y+33*16)
		self.big_dotList.append(newdot)
		i = 0
		while (i<17):
			newdot = dot(self.dot_small.rect.x+3+31*i, self.dot_small.rect.y+33*17)
			self.dotList.append(newdot)
			i+=1				
				
		i = 0
		while (i<17):
			newdot = dot(self.dot_small.rect.x+3+31*3, self.dot_small.rect.y+i*31)
			self.dotList.append(newdot)
			newdot = dot(self.dot_small.rect.x+3+31*13-7, self.dot_small.rect.y+i*31)
			self.dotList.append(newdot)
			i+=1
		
###done placing dots initially now need to blit them all

	
	def task(self):
		#check to see if pacman eats a dot
		for item in self.dotList:
			if self.player.rect.x+5>item.x-15 and self.player.rect.x+5<item.x+15 and self.player.rect.y+5<item.y+15 and self.player.rect.y+5>item.y-15 and item.visible==1:
				item.visible=0
				#self.waka.play()
				self.score = self.score+10

		for item in self.big_dotList:
			if self.player.rect.x+5>item.x-15 and self.player.rect.x+5<item.x+15 and self.player.rect.y+5<item.y+15 and self.player.rect.y+5>item.y-15 and item.visible==1:
				item.visible=0
				self.edible = 300 #27 seconds
				#self.waka.play()
				self.score = self.score+20
				
		
				
				
				
		if self.player.rect.x+5>self.blueGhost.rect.x-15 and self.player.rect.x+5<self.blueGhost.rect.x+15 and self.player.rect.y+5<self.blueGhost.rect.y+15 and self.player.rect.y+5>self.blueGhost.rect.y-15 and self.edible != 0 and self.blueGhost.alive ==1:
			#ghost dies
			self.blueGhost.alive = 0
			self.score = self.score+100
		elif self.player.rect.x+5>self.blueGhost.rect.x-15 and self.player.rect.x+5<self.blueGhost.rect.x+15 and self.player.rect.y+5<self.blueGhost.rect.y+15 and self.player.rect.y+5>self.blueGhost.rect.y-15 and self.edible == 0 and self.blueGhost.alive == 1:
			self.player.alive = 0
			#pacman dies

		if self.player.rect.x+5>self.redGhost.rect.x-15 and self.player.rect.x+5<self.redGhost.rect.x+15 and self.player.rect.y+5<self.redGhost.rect.y+15 and self.player.rect.y+5>self.redGhost.rect.y-15 and self.edible != 0 and self.redGhost.alive ==1:
			#ghost dies
			self.redGhost.alive = 0
			self.score = self.score+100
		elif self.player.rect.x+5>self.redGhost.rect.x-15 and self.player.rect.x+5<self.redGhost.rect.x+15 and self.player.rect.y+5<self.redGhost.rect.y+15 and self.player.rect.y+5>self.redGhost.rect.y-15 and self.edible == 0 and self.redGhost.alive == 1:
			self.player.alive = 0
			#pacman dies

		if self.player.rect.x+5>self.pinkGhost.rect.x-15 and self.player.rect.x+5<self.pinkGhost.rect.x+15 and self.player.rect.y+5<self.pinkGhost.rect.y+15 and self.player.rect.y+5>self.pinkGhost.rect.y-15 and self.edible != 0 and self.pinkGhost.alive ==1:
			#ghost dies
			self.pinkGhost.alive = 0
			self.score = self.score+100
		elif self.player.rect.x+5>self.pinkGhost.rect.x-15 and self.player.rect.x+5<self.pinkGhost.rect.x+15 and self.player.rect.y+5<self.pinkGhost.rect.y+15 and self.player.rect.y+5>self.pinkGhost.rect.y-15 and self.edible == 0 and self.pinkGhost.alive == 1:
			self.player.alive = 0
			#pacman dies

		if self.player.rect.x+5>self.orangeGhost.rect.x-15 and self.player.rect.x+5<self.orangeGhost.rect.x+15 and self.player.rect.y+5<self.orangeGhost.rect.y+15 and self.player.rect.y+5>self.orangeGhost.rect.y-15 and self.edible != 0 and self.orangeGhost.alive ==1:
			#ghost dies
			self.orangeGhost.alive = 0
			self.score = self.score+100
		elif self.player.rect.x+5>self.orangeGhost.rect.x-15 and self.player.rect.x+5<self.orangeGhost.rect.x+15 and self.player.rect.y+5<self.orangeGhost.rect.y+15 and self.player.rect.y+5>self.orangeGhost.rect.y-15 and self.edible == 0 and self.orangeGhost.alive == 1:
			self.player.alive = 0
			#pacman dies
			
		#if pygame.mixer.music.get_busy()==False:
		#	pygame.mixer.music.play()
		#self.clock.tick(60)
		inside = 0
		self.blueGhost.tick()
		self.redGhost.tick()
		self.pinkGhost.tick()
		self.orangeGhost.tick()
		for event in pygame.event.get():
			if (event.type == KEYDOWN ):
				inside = 1
				self.player.move(event.key)
			
			if (event.type == pygame.QUIT):
				reactor.stop()
		self.player.tick()
		
		if inside != 1 and pygame.event.get() == [] and self.player.alive != 0:
			self.player.move(self.player.last_key)
			self.player.move(self.player.last_key)
		
		
				

		self.screen.fill(self.black)	
		self.screen.blit(self.background.image, self.background.rect)	
		##blitz all visible dots
		smallDots_eaten = 1
		for item in self.dotList:
			if item.visible==1:
				smallDots_eaten = 0
				self.screen.blit(self.dot_small.image, (item.x, item.y))
		
		bigDots_eaten = 1
		for item in self.big_dotList:
			if item.visible==1:
				bigDots_eaten = 0
				self.screen.blit(self.dot_big.image, (item.x, item.y))

	
		if self.game_screen == 0: #start screen
			self.screen.blit(self.start.image, self.start.rect)
			pygame.display.flip()
			time.sleep(5)
			self.game_screen =1 
		if self.game_screen == 1:
				
			if smallDots_eaten == 1 and bigDots_eaten == 1:
				time.sleep(2) # delays for 2 seconds
				reactor.stop()
			
			if (self.blueGhost.alive == 0 and self.redGhost.alive == 0):
				self.deathCounter += 1
				if self.deathCounter > 2:
					time.sleep(2)
					reactor.stop()
			
			#if (self.blueGhost.alive != 0):
			self.screen.blit(self.blueGhost.image, self.blueGhost.rect)
			self.screen.blit(self.redGhost.image, self.redGhost.rect)
			self.screen.blit(self.pinkGhost.image, self.pinkGhost.rect)
			self.screen.blit(self.orangeGhost.image, self.orangeGhost.rect)
			self.screen.blit(self.player.image, self.player.rect)
			self.levelLabel = self.myfont.render("Level: 1", 1, (255,255,0))
			self.scoreLabel = self.myfont.render("Score: "+str(self.score), 1, (255,255,0))
			self.screen.blit(self.scoreLabel, (25, 25))
			self.screen.blit(self.levelLabel, (675, 25))
			self.lifeLabel = self.myfont.render("Lives: ", 1, (255,255,0))
			self.screen.blit(self.lifeLabel, (240, 25))
			if self.player.alive != 0:
				self.screen.blit(self.life.image, self.life.rect)
				
			pygame.display.flip()
	
			
if __name__ == '__main__':
	handler = ConnectionHandler()
	commandFactory = CommandFactory(handler)
	redCommandFactory = redCommandFactory(handler)
	pinkCommandFactory = pinkCommandFactory(handler)
	orangeCommandFactory = orangeCommandFactory(handler)
	reactor.listenTCP(8678, commandFactory) # command port listening for blue ghost
	reactor.listenTCP(8679, redCommandFactory) #command port listening for red ghost
	reactor.listenTCP(8680, pinkCommandFactory) #command port listening for pink ghost
	reactor.listenTCP(8681, orangeCommandFactory) #command port listening for orange ghost
	gs = GameSpace(handler)
	LC = LoopingCall(gs.task)
	LC.start(1/60)
	reactor.run()
