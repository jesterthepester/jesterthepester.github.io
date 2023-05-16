# Automate the Boring Stuff

## Link for Material <br>

[Automate The Boring Stuff Book](https://automatetheboringstuff.com/#toc)

## Table of Contents <br>

[1. First For Loop](#1-first-for-loop)<br>
[2. Function](#2-function)<br>
[3. First Game](#3-first-game)<br>
[4. File Management](#4-file-management)<br>
    [4. 1. Open and Read](#41-open-and-read)<br>
    [4. 2. Delete a File](#42-delete-a-file)<br>
[5. Practical Use 1 - Folder and File List](#5-practical-use-1---folder-and-file-list)<br>
[6. Print a Box](#6-print-a-box)<br>
[7. Logging](#7-logging)<br>
[8. Get a price from a URL](#8-get-a-price-from-a-url)<br>
[9. Excel Manipulation](#9-excel-manipulation)<br>
    [9. 1. Worksheet Names and Locations](#91-worksheet-names-and-locations)<br>
    [9. 2. Creating and Manpulating Worksheets](#92-creating-and-manpulating-worksheets)<br>
[10. SMTP - Simple Mail Transfer Protocol](#10-smtp---simple-mail-transfer-protocol)<br>
    [10. 1. Sending Email](#101-sending-email)<br>
    [10. 2. Checing Inbox (IMAP)](#102-checing-inbox-imap)<br>
[11. Mouse Control](#11-mouse-control)<br>
[12. Keyboard Control](#12-keyboard-control)<br>
[13. Screen Capture](#13-screen-capture)<br>

## Scripts

### 1. First For Loop
<br>

```Python
print('My name is')
for i in range(5,-1,-1):
    print('Jimmy Five Times '+str(i))
```

### 2. Function
<br>

``` Python
def spam():
    global eggs
    eggs = 'Hello'
    print(eggs)
eggs = 42
print(eggs)
spam()
```

### 3. First Game
<br>

``` Python
import random
print("Hello, what is your name?")
name=input()
print('Well, '+name+', I am thinking of a number between 1 and 20')
secretNumber=random.randint(1,20)
for guessesTaken in range(1,7):
    print('Take a guess.')
    guess=int(input())
    if guess < secretNumber:
        print('Your guess is too low.')
    elif guess > secretNumber:
        print('Your guess is too high.')
    else:
        break # This condition is for the correct guess!
if guess == secretNumber:
    print('Good job, '+name+'! You guessed my number in '+str(guessesTaken)+' guesses.')
else:
    print('Nope, the number I was thinking of was '+str(secretNumber))
```

### 4. File Management
<br>

#### 4.1. Open and Read

```Python
helloFile = open('c:\\users\\mlogan\\hello.txt')
helloFile.read()
```

#### 4.2. Delete a File

```Python
import os
for filename in os.listdir():
    if filename.endswith('.rxt'): # meant to be txt
        #os.unlink(filename)
        print(filename)
```

### 5. Practical Use 1 - Folder and File List
<br>

```Python
import os
for folderName, subfolders, filenames in os.walk('c:\\_delicious'):
	print('The folder is ' + folderName)
	print('The subfolders in ' + folderName + ' are: ' + str(subfolders))
	print('The filenames in ' + folderName + ' are: ' + str(filenames))
    for subfolder in subfolders:
        if 'fish' in subfolder:
            os.rmdir(subfolder)
    for file in filenames:
        if file.endswith('.py'):
            shutil.copy(os.join(folderName, file), os.join(folderName, file + '.backup'))
```

### 6. Print a Box
<br>

```Python
def boxPrint(symbol, width, height):
    if len(symbol) != 1:
        raise Exception('Symbol needs to be a string of length 1.')
    if (width < 2) or (height < 2):
        raise Exception('Witdth and height must be 2 or greater')
    print(symbol * width)
    for i in range(height - 2):
        print(symbol + (' ' * (width - 2)) + symbol)
    print(symbol * width)
boxPrint('*',8,8)
```

### 7. Logging
<br>

```Python
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s - %(levelname)s - %(message)s')
# basic logging function above ^

#logging.basicConfig(filename='xyzlog.txt', level=logging.DEBUG, format='%(asctime)s - %(levelname)s - %(message)s')
##log above records the debug messages to the CWD in the "filename" mentioned

logging.disable(logging.CRITICAL)
# dissables logging at or below critical
# 5 levels of logging (debug to critical)
logging.debug('Start of program.')
def factorial(n):
    logging.debug('Start of factorial (%s)'%(n))
    total = 1
    for i in range(1, n + 1):
        total *= i
        logging.debug('i is %s, total is %s' % (i, total))
    logging.debug('Return value is %s' % (total))
    return total
print(factorial(5))
logging.debug('End of program.')
```

### 8. Get a price from a URL
<br>

```Python
import requests
import bs4
# html.parser ignores warning
def getAmazonPrice(productUrl):
    res = requests.get(productUrl)
    res.raise_for_status()
    soup = bs4.BeautifulSoup(res.text, 'html.parser')
    elems = soup.select('price')
    return elems[0].text.strip()
price = getAmazonPrice('https://www.amazon.com.au/Automate-Boring-Stuff-Python-Programming/dp/1593279922/ref=sr_1_1?crid=KY2HRARA3J32&dchild=1&keywords=automate+the+boring+stuff+with+python&qid=1624183053&sprefix=automate+the+%2Caps%2C339&sr=8-1')
print('The price is ' + price)
```

### 9. Excel Manipulation
<br>

#### 9.1. Worksheet Names and Locations

```Python
import openpyxl, os
os.chdir('c:\\.......')
workbook = openpyxl.load_workbook('example.xlsx')
type(workbook)
sheet = workbook.get_sheet_by_name('Sheet1')
workbook.get_sheet_names() # returns list of sheets
cell = sheet['A1']
cell.value
str(sheet['A1'].value) # for date values
sheet.cell(row = 1, column = 2)
for i in range(1,8):
    print(i, sheet.cell(row = i, column = 2).value)
```

#### 9.2. Creating and Manpulating Worksheets

```Python
import openpyxl, os
wb = openpyxl.Workbook()
wb.get_sheet_names()
sheet=get_sheet_by_name('Sheet')
sheet['A1'].value == None # true as new worksheet
os.chdir('c:\\....')
wb.save('example.xlsx')
sheet2 = wb.create_sheet()
wb.get_sheet_names()
sheet2.title = 'My New Sheet Name'
wb.save('example2.xlsx')
wb.create_sheet(index=0,title='My Other Sheet')
wb.save('example3.xlsx')
```

### 10. SMTP - Simple Mail Transfer Protocol
<br>

#### 10.1. Sending Email

```Python
# sending an email
import smtplib
conn = smtplib.SMTP('smtp.gmail.com', 587)
conn.ehlo() # checks connection
conn.starttls() # encryption
conn.login('michaellogan40@gmail.com','PASSWORD') # log onto gmail
conn.sendmail('michaellogan40@gmail.com','rmloganj@gmail.com','Subject: So long...\n\nDear Me,\nSo long, and thanks for all the fish.\n\n-Michael')
```

#### 10.2. Checing Inbox (IMAP)
<br>

```Python
# IMAP is for checking email
import imapclient, pyzmail
conn = imapclient.IMAPClient('imap.gmail.com', ssl=True)
conn.login('michaellogan40@gmail.com','PASSWORD')
conn.select_folder('INBOX', readonly=True) # readonly doesnt allow deleting of emails
UIDs = conn.search(['SINCE 20-Aug-2019'])
# returns list of number [x, y, z] format
# search key: 'ALL', 'BEFORE date', 'ON date', 'SINCE date', 'SUBJECT "string"', 'BODY "string"', 'TEXT "string"' etc.
rawMessage = conn.fetch([UID number],['BODY[]','FLAGS'])
# pulls email detais (replace 'UID number' with actual number from UIDs list
message = pyzmail.PyzMessage.factory(rawMessage[UID number][b'BODY[]'])
# useses pyzmail to call pyzmessage object
message.get_subject()
message.get_addresses('from') # gets name and email in tuple
message.get_addresses('to') # etc. ('bcc', 'cc')
message.text_part # if None, it was html
message.html_part # if == None - it was text
message.text_part.get_payload().decode('UTF-8')
# decodes as UTF-8 (99% of the time)
message.tex_part.charset == None # checks UTF-8 ?
conn.list_folders() # lists folders
conn.select_folder('INBOX', readonly = False)
conn.delete_messages([UID number]) # deletes a message with a UID number
```

### 11. Mouse Control
<br>

```Python
import pyautogui, os
pyautogui.size() # calls screen size
width, height = pyautogui.size() # sets width and heigh as etc.
pyautogui.position() # current mouse position
pyautogui.moveTo(10, 10, duration=1.5) # moves the mouse directly to the coordinate in the time 1.5s
pyautogui.moveRel(200,0,1.5) # moves the mouse 200 pixels to the right
pyautogui.click(339,38) # clicks instantly on the coordinate
pyautogui.doubleClick()
pyautogui.middleClick() # double / middle
# dragTo() and dragRel() drags to / rel to
pyautogui.displayMousePosition() # shows live location of my mouse
## - auto-spiral program - ##
import pyautogui
pyautogui.click()
distance = 200
while distance > 0:
    print(distance, 0)
    pyautogui.dragRel(distance, 0, duration = 0.1)
    distance = distance - 25
    print(0,distance)
    pyautogui.dragRel(0, distance, duration = 0.1)
    print(-distance,0)
    pyautogui.dragRel(-distance, 0, duration = 0.1)
    distance = distance - 25
    print(0, -distance)
    pyautogui.dragRel(0, -distance, duration = 0.1)
# failsafe - if mouse is in 0,0 it will break
```

### 12. Keyboard Control
<br>

```Python
import pyautogui
pyautogui.click(100,100); # colon for running two commands in idle
pyautogui.typewrite('Hello world!', interval = 0.2)
# interval for slowly typing with interval of 0.2s per character
pyautogui.typewrite(['a','b','left','left','X','Y'], interval = 1)
# types out a then b then left key twice then x and finally y
pyautogui.KEYBOARD_KEYS() # lists all keys
pyautogui.press('f1') # for one off press of a key
pyautogui.hotkey('ctrl','o') # series of keys (ctrl+o)
```

### 13. Screen Capture
<br>

```Python
import pyautogui
pyautogui.screenshot() # returns pillow image
pyautogui.screenshot('c:\....screenshot.png')
# saves screenshot in specific location
pyautogui.locateOnScreen('c:\\ ... calc7key.png') # returns location of image
# returns ('x','y','width','heigh')
center = pyautogui.locateCenterOnScreen('c:\\ ... calc7key.png') # center location of image given
pyautogui.moveTo((932,336),duration = 1) # pictures need to be pixel perfect
```

