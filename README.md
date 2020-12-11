# Animal population game
# v0.6
# Atkin DaBell
# Copyright for sir.burton

import time, random

#Player stuff
day = 0


#Item stuff
items = {'bunnyPopulation':10,
         'foxPopulation':3,
         'plants':20,
         'thirst':40,
         'hunger':40,
         'sleep':0,
         'day':0
         }




#Creating a function to make sure any inputs are numbers.
#I take a lot of number inputs, so this will be helpful
def numberInput(text=""):
    cow = input(text)
    while not cow.isdigit():
        print("Please enter a number:")
        cow = input(text)
    return int(cow)


def menu():
    print(' 1) be a bunny')
    print(' 2) be a fox')
    print(' 0) do something else')
    pig = numberInput()
    print()
    if pig == 1:
        menuBunny()
    if pig == 2:
        menuFox()
    if pig == 0:
        print("you cant")
    else:
        items ['sleep'] += 1
        time.sleep(items ['sleep'])
        print()
        menu()


def randomEvents():
    global plants, hunger, thirst, bunnyPopulation, foxPopulation
    event = random.randint(0,350)
        #boom of foxes
    if event <= 30:
        print ("A boom of the fox population went up")
        items ['bunnyPopulation']+=4
        #boom of bunnies
    elif event <= 60:
        print("A boom of the bunny population went up")
        items ['bunnyPopulation']+=4
        #drought
    elif event <= 75:
        print("a drought acoured!")
        items ['thirst'] += 17
        #scarcity of plants
    elif event <=105:
        print("the population of plants have gone down")
        items ['plants']-=6
       

def menuBunny():
    global hunger, thirst, bunnyPopulation
    print('Hunger = ',items ['hunger'])
    print('Thirst = ',items ['thirst'])
    print('amount of plants =',items ['thirst'])
    print('Fox population = ', items ['foxPopulation'])
    print('Bunny population = ', items ['bunnyPopulation'])
    randomEvents()  #Initiate possible random events
    print(' 1) eat')
    print(' 2) drink')
    print(' 3) add population')
    option = numberInput()
    print()
    if option == 1:
        items ['hunger'] -= 12
        items ['plants'] -= 1
        items ['day'] += 1
    elif option == 2:
        items ['thirst'] -= 12
        items ['day'] += 1
    elif option == 3:
        items ['bunnyPopulation'] += 0.34
        items ['day'] += 1
    else:
        print("Unknown command")
    if random.randint(0,40) < items ["foxPopulation"]:
        bunnySeeFox()
    menuBunny()
    return option


def menuFox():
        global hunger, thirst, foxPopulation
        print('Hunger = ',items ['hunger'])
        print('Thirst = ',items ['thirst'])
        print('amount of plants =',items ['thirst'])
        print('Fox population = ', items ['foxPopulation'])
        print('Bunny population = ', items ['bunnyPopulation'])
        randomEvents()  #Initiate possible random events
        print(' 1) hunt')
        print(' 2) drink')
        print(' 3) add population')
        option = numberInput()
        print()
        if option == 1:
             foxSeeBunny()
        elif option == 2:
             items ['thirst'] -= 12
        elif option == 3:
             items ['foxPopulation'] += 0.34
        elif option == 0:
             print("no u")
        else:
            print("You wasted a day.")
        menuFox()
        return option


def bunnySeeFox():
    print("You see a fox.")
    print(" 1) Follow it")
    print(" 2) run away")
    choice = numberInput()
    if choice == 1:
        print('You follow the fox and you die')
    elif choice == 2:
         print("You run away")
    if random.randint(0,100) < 20:
        print("the fox caught up to you and ate you")
        exit()



def foxSeeBunny():
    print("You see a bunny.")
    print(" 1) Ignore")
    print(" 2) Hunt it")
    choice = numberInput()
    if choice == 1:
        print('You ignore the bunny')
    if choice == 2:
        print("you follow the bunny and you eat it")
        items ['hunger'] -= 15
    if random.randint(0,100) < 40:
        print("the bunny ran away")


for i in range(250):
    menu()
               

while day <= 250:
    print()
    print('CONGRATS! you survived till hibernation time!')
    time.sleep(1)
    print('you go into your bunny hole and hibernate')
    time.sleep(2)
    print('Thanks for playing!')
