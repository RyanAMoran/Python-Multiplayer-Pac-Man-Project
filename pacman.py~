import sys, os, math, time, pygame
from pygame.locals import *

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
		
class Player(pygame.sprite.Sprite):
		
	def __init__(self, gs=None):
		self.gs = gs
		FILE = "images/pacman.png"
		FILE2 = "images/packman_full.png"
		self.image = pygame.image.load(FILE) #filled in pacman image
		self.image_full = pygame.image.load(FILE2)
		self.image = pygame.transform.scale(self.image, (int(30),int(30)))
		self.image_full = pygame.transform.scale(self.image_full, (int(30),int(30)))
		self.orig_image = self.image # hold on to original pacman image facing right
		
		self.rect = self.image.get_rect()
		self.rect.x = 396
		self.rect.y = 393
		self.orientation = "right"
		self.last_key = "right"
		self.count = 0

	def validMove(self, x, y):
		#lower right half of board start
		if x>636:
			return 0
		elif y>633:
			return 0
		elif x>536 and y>213 and y<453:
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
		elif ((x<=231) and (y>=214 and y<=452)):
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
		elif ( x <= 131):
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
		else:
			return 1
		
				
	def move(self, keycode):
		if (keycode == K_RIGHT):
			self.last_key = "right"
			if self.validMove(self.rect.x+4, self.rect.y):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(4, 0)
				if self.orientation != "right":
					self.image = self.orig_image
					self.orientation = "right"
				elif self.count==1:
					self.image = self.image_full
					self.orientation = "full"
			
		if (keycode == K_LEFT):
			self.last_key = "left"
			if self.validMove(self.rect.x-4, self.rect.y):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(-4,0)
				if self.orientation != "left":
					self.image = pygame.transform.rotate(self.orig_image, 180)
					self.orientation = "left"
				elif self.count==1:
					self.image = self.image_full
					self.orientation = "full"
			
		if (keycode == K_DOWN):
			self.last_key = "down"
			if self.validMove(self.rect.x, self.rect.y+4):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(0,4)
				if self.orientation!="down":
					self.image = pygame.transform.rotate(self.orig_image, 270)
					self.orientation = "down"
				elif self.count == 1:
					self.image = self.image_full
					self.orientation = "full"
			
		if (keycode == K_UP):
			self.last_key = "left"
			if self.validMove(self.rect.x, self.rect.y-4):
				if self.count<1:
					self.count = self.count+1
				else:
					self.count = 0
				self.rect = self.rect.move(0,-4)
				if self.orientation!="up":
					self.image = pygame.transform.rotate(self.orig_image, 90)
					self.orientation="up"
				elif self.count == 1:
					self.image = self.image_full
					self.orientation = "full"
		return
		
	def tick(self):
		#print self.rect.x, self.rect.y

		return
		
class GameSpace:
	def main(self):
		pygame.init()
		self.myfont = pygame.font.SysFont("monospace", 15)
		

		pygame.mixer.pre_init(44100, -16, 2, 2048) #initializing sound
		pygame.mixer.music.load('./sounds/adjSiren.wav')
		self.waka = pygame.mixer.Sound('./sounds/waka.wav')
		
		winTitle = pygame.display.set_caption("Paradigms Final Project: Multiplayer Pacman")
		
		self.size = self.width, self.height = 800, 800
		
		self.black = 0, 0, 0
		
		self.screen = pygame.display.set_mode(self.size)
		
		pygame.key.set_repeat(1, 50) #adjust this to make pacman move faster
		
		self.clock = pygame.time.Clock()
		
		self.player = Player(self)
		self.background = Background(self)
		self.dot_small = Dot_Small(self)
		self.dot_big = Dot_Big(self)
		self.dotList=[]
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
		newdot = dot(self.dot_small.rect.x+3, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+219, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+280, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+305+32*6, self.dot_small.rect.y+38)
		self.dotList.append(newdot)
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

		newdot = dot(self.dot_small.rect.x+3, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)	
		newdot = dot(self.dot_small.rect.x+217, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+278, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)
		newdot = dot(self.dot_small.rect.x+300+32*6, self.dot_small.rect.y+33*16)
		self.dotList.append(newdot)
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


		while 1:
			#check to see if pacman eats a dot
			for item in self.dotList:
				if self.player.rect.x+5>item.x-15 and self.player.rect.x+5<item.x+15 and self.player.rect.y+5<item.y+15 and self.player.rect.y+5>item.y-15 and item.visible==1:
					item.visible=0
					self.waka.play()
					self.score = self.score+10

			if pygame.mixer.music.get_busy()==False:
				pygame.mixer.music.play()
			self.clock.tick(60)
			for event in pygame.event.get():
				if (event.type == KEYDOWN):
					self.player.move(event.key)
			
				if (event.type == pygame.QUIT):
					sys.exit()
				self.player.tick()
				
				self.screen.fill(self.black)	
				self.screen.blit(self.background.image, self.background.rect)

				##blitz all visible dots
				for item in self.dotList:
					if item.visible==1:
						self.screen.blit(self.dot_small.image, (item.x, item.y))
				

				
				self.screen.blit(self.player.image, self.player.rect)
				self.scoreLabel = self.myfont.render("Score: "+str(self.score), 1, (255,255,0))
				self.screen.blit(self.scoreLabel, (25, 25))
				
				pygame.display.flip()
			
if __name__ == '__main__':
	gs = GameSpace()
	gs.main()
