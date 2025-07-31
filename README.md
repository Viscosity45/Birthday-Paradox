# Birthday-Paradox
A Python-based simulation and probability calculator for the Birthday Paradox — exploring how likely it is that two people in a group share the same birthday. Includes visualizations, code for multiple group sizes, and comparison with theoretical probability.

import datetime, random

def get_random_birthdate(Numofdate):
    birthdays = [ ]
    startofyear = datetime.date(2002,1,1)
    for _ in range(Numofdate):
        randomNumberofdays = datetime.timedelta(random.randint(0,364))
        birthday = startofyear + randomNumberofdays
        birthdays.append(birthday)
    return birthdays

def getmatch(birthdays):
    if len(birthdays) == len(set(birthdays)):  #As set remove the same values
        return None  #If both are equal that means all birthdays are unique..
    
    for a, birthdayA in enumerate(birthdays):
        for b , birthdayB in enumerate(birthdays[a+1: ]):
            if birthdayA == birthdayB:
                return birthdayA

MONTHS = ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec')
          
# Display the intro:
print('''Birthday Paradox, by birthdayparadox.py
 The Birthday Paradox shows us that in a group of N people, the odds
 that two of them have matching birthdays is surprisingly large.
 This program does a Monte Carlo simulation (that is, repeated random
 simulations) to explore this concept.

 (It's not actually a paradox, it's just a surprising result.)
 ''')


while True:
    print('How many birthdays do you want to generate: ')
    response = input('>>>>>>')
    if response.isdecimal() and (0< int(response) <=100 ):
        numBdays = int(response)
        break
        
print()


# Generate and display the birthdays:
print('Here are {} birthdays:'.format(numBdays))
            
birthdays = get_random_birthdate(numBdays)
for i, birthday in enumerate(birthdays):
    if i != 0:
        print(',',end=" ")
    monthName = MONTHS[birthday.month - 1]
    dateText = '{}{}'.format(monthName, birthday.day)
    print(dateText, end="")
    
print()
print()

# To check if there are two same birthdays

match = getmatch(birthdays)
print('In this simulation>>>',end='')
if match != None:
    monthName = MONTHS[match.month - 1]
    datetext = ' {}{}'.format(monthName, match.day)
    print('Multiple people have a birthday on',datetext)
else:
    print('There are no matching birthdays.')
print()

# Run through 100,000 Simulations

print('Generating', numBdays, 'random birthdays 100,000 times....')
input('Press Enter to begin...')
similar  = 0
print('Let\'s run another 100,000 simulations.')
for i in range(100000):
    if i % 10000 == 0:
        print(i, 'simulations run...')
    birthdays = get_random_birthdate(numBdays)
    if getmatch(birthdays) != None:
        similar += 1
print('100,000 simulations run.')

# Display simulation results:
probability =round(((similar/100000)*100),2)
print('Out of 100,000 simulations of', numBdays, 'people, there was a')
print('matching birthday in that group', similar, 'times. This means')
print('that', numBdays, 'people have a', probability, '% chance of')
print('having a matching birthday in their group.')
print('That\'s probably more than you would think!')
