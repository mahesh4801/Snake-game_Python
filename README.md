# Snake-game_Python
import random
width=10
height=10
def print_board (snake,food):
    for y in range(height):
        for x in range(width):
            if [x,y]==food:
                print("F",end=" ")
            elif [x,y] in snake:
                print("S",end=" ")
            else:
                print(".",end= " ")
        print()
    print()
    
def move_snake(snake,direction):
    head=snake[-1]
    if direction=="up":
        new_head=[head[0],head[1]-1]#move up 
    elif direction=="down":
        new_head=[head[0],head[1]+1]#move down
    elif direction=="left":
        new_head=[head[0]-1,head[1]]#move left
    elif direction=="right":
        new_head=[head[0]+1,head[1]]#move right
    else:
        print("Invalid direction,use up/down/left/right.")
        return snake,False
#wall colide conditions
    if new_head[0]<0 or new_head[0]>=width or new_head[1]<0 or new_head[1]>=height:
        return snake,"wall"
#snake colide conditions
    if new_head in snake:
        return snake,"self"
    snake.append(new_head)
    return snake,new_head
#snake to eat food
def place_food(snake):
    while True:
        x=random.randint(0,width-1)
        y=random.randint(0,height-1)
        if[x,y] not in snake:
            return[x,y]
def snake_game():
    snake=[[5,5]]
    food=place_food(snake)
    score=0
    while True:
        print_board(snake,food)
        print("Score:",score)
        direction=input("enter direction (up/down/left/right):")
        snake,result=move_snake(snake,direction)
        if result=="wall":
            print("you hit the wall,Game Over!!!")
            break
        elif result=="self":
            print("you hit yor self,Game Over!!!")
            break
        elif result==food:
            score+=1
            food=place_food(snake)
        else:
            snake.pop(0)
    print("Final score:",score)
snake_game()
