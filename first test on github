import pygame
import math
import random
pygame.init()
clock = pygame.time.Clock()

#   some colers
BLACK  = (   0,   0,   0)
WHITE  = ( 255, 255, 255)
GREEN  = (   0, 255,   0)
RED    = ( 255,   0,   0)
BLUE   = (   0,   0, 255)


#   setting the window size
size = (700, 500)
screen = pygame.display.set_mode(size)




#   Setting the window title
pygame.display.set_caption("six seven")
shapes=[]
done = False
stomake=0
space=False
px=359
py=250
pdr=0
pxvel=0
pyvel=0





#   DEFINITIONS
def makeshape(xpos,ypos,sides,size,dr,speed,speeddir):
        shapes.append([xpos,ypos,sides,size,dr,speed,speeddir])
        
def move(xory,dr,amount):
    if xory == "x":
        return amount*math.cos(dr*math.pi/180)
    elif xory == "y":
        return amount*math.sin(dr*math.pi/180)
    else:
        return None
    
def drawshapecenter(xpos,ypos,sides,size,dr):
    mx=xpos
    my=ypos
    mdr=dr
    listopoints=[]
    length=size/math.tan(((sides-2)*90/sides)*math.pi/180)
    mx+= move("x",mdr,size)
    my+= move("y",mdr,size)
    mdr+=90
    mx+= move("x",mdr,length)
    my+= move("y",mdr,length)
    for i in range(sides):
        listopoints.append([mx,my])
        mdr+=180-((sides-2)*180/sides)
        if mdr >= 360:
            mdr-=360
        mx+= move("x",mdr,length*2)
        my+= move("y",mdr,length*2)
    pygame.draw.polygon(screen,WHITE,listopoints,2)
def point(degres):
    if degres>=360:
    
        return (degres-360)
    elif degres<0:
        
        return (degres+360)
    else:
        
        return degres
    

    
def drawplayer(xpos,ypos,size,dr):
    mx=xpos
    my=ypos
    mdr=dr
    listopoints=[]
    mx+= move("x",mdr,4)
    my+= move("y",mdr,4)
    mx+= move("x",mdr,14/size)
    my+= move("y",mdr,14/size)
    listopoints.append([mx,my])
    mdr= point(mdr-161.5)
    mx+= move("x",mdr,38/size)
    my+= move("y",mdr,38/size)
    listopoints.append([mx,my])
    mdr= point(mdr-144)
    mx+= move("x",mdr,15/size)
    my+= move("y",mdr,15/size)
    listopoints.append([mx,my])
    mdr= point(mdr+72)
    mx+= move("x",mdr,15/size)
    my+= move("y",mdr,15/size)
    listopoints.append([mx,my])
    mdr=point(mdr-144)
    mx+= move("x",mdr,38/size)
    my+= move("y",mdr,38/size)
    listopoints.append([mx,my])
    pygame.draw.lines(screen, WHITE, True, listopoints)
    
    
    
    




    
while not done:
    # --- Main event loop
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True

        elif event.type == pygame.KEYDOWN:
            if event.key== pygame.K_SPACE:
                makeshape(100,250,10,50,0,5,0)
                space=True
       
           
        
        elif event.type == pygame.KEYUP:
            if event.key== pygame.K_SPACE:
                space=False

        if event.type == pygame.MOUSEBUTTONDOWN:
            mousepressed=True
        
            
            
        
    mousex, mousey = pygame.mouse.get_pos()
    # Game Logic
    
    # PLAYER CODE
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP]:
        pxvel+=move("x",pdr,0.1)
        pyvel+=move("y",pdr,0.1)

    if keys[pygame.K_RIGHT]:
        pdr=point(pdr+5)
        
    if keys[pygame.K_LEFT]:
        pdr=point(pdr-5)
    px+=pxvel
    py+=pyvel
    pxvel*=0.99
    pyvel*=0.99
    
    if px<20:
        px+=740  
    if px>720:
        px-=740       
    if py<-20:
        py+=540     
    if py>520:
        py-=540



            
    
    #if space:
    
        #makeshape(100,250,10,50,0,5,0)
    
    
    if pygame.time.get_ticks()>1000*stomake: 
        stomake+=1

    # shapes runthrough
    thingstodelete=[]
    for i in range(len(shapes)):

        shapes[i][0]+= math.cos(shapes[i][6]/180*math.pi)*shapes[i][5]

        shapes[i][1]+= math.sin(shapes[i][6]/180*math.pi)*shapes[i][5]
        
        shapes[i][4]+= 2
        if shapes[i][4]>=360:
            shapes[i][4]-=360
        if math.sqrt((shapes[i][0]-mousex)**2+(shapes[i][1]-mousey)**2)<shapes[i][3] and mousepressed:
            if shapes[i][2]>4:
                for j in range(3):
                    makeshape(shapes[i][0],shapes[i][1],shapes[i][2]-1,shapes[i][3]-5,random.randint(0,360),random.randint(5, 5),random.randint(0, 360))
            thingstodelete.append(i)
            
    
    
    shapes=[i for i in range(len(shapes)) if i not in thingstodelete]
    print(len(thingstodelete))



    # --- Drawing code 
    screen.fill(BLACK)

    
    for i in shapes:
        drawshapecenter(i[0],i[1],i[2],i[3],i[4])

    
    
    drawplayer(px,py,3,pdr)



    # ---update the screen
    pygame.display.flip()
    mousepressed=False
    # --- Limit to 60 frames per secondu 89io k
    clock.tick(60)
pygame.quit()
