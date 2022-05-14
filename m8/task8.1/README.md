1.Write easy program, which will display current date and time.

import time

print('Now is', time.strftime("%Y-%m-%d %H:%M:%S"))


2.Write python program, which will accept comma-separated numbers, and then it should write tuple and list of them:Enter numbers: 1, 2, 7, 43, 9

a = input("Type in numbers seperated only by a comma :")

a1 = a.split(',')

b = [a]

c = tuple(a1)

print(b)

print(c)


3.Write python program, which will askfile name. File should be read, and only even lines should be shown.

import itertools

import sys

c = input('Enter the file name: ')

if c == '1.txt':

    with open(c,'r') as fs:
	
        sys.stdout.writelines(itertools.islice(fs, 1, None, 2))

else:

    print('Error')




4.Write python program, which should read htmldocument, parse it, and showit’s title.

from bs4 import BeautifulSoup

with open("index.html") as fp:

    soup = BeautifulSoup(fp, "html.parser")
	
    print(soup.head.title)


5.Write pythonprogram, which will parse user’s text, and replace some emotions with emoji’s (Look: pip install emoji)

import emojis

def main():

    sentence = input("Input a Sentence: ")
	
    print(sentence)
	
    sentence = convert(sentence)
	
    print(sentence)


def convert(sentence):

    smile = emojis.encode(':smile:')
	
    pensive = emojis.encode(':pensive:')
	
    sentence = sentence.replace(":)", smile)
	
    sentence = sentence.replace(":(", pensive)
	
    return sentence


main()



6.Write program, that will show basic PC information (OS, RAM amount, HDD’s, andetc.)

import platform,socket,re,uuid,json,psutil,logging

def getSystemInfo():

    try:
	
        info={}
		
        info['platform']=platform.system()
		
        info['platform-release']=platform.release()
		
        info['platform-version']=platform.version()
		
        info['architecture']=platform.machine()
		
        info['hostname']=socket.gethostname()
		
        info['ip-address']=socket.gethostbyname(socket.gethostname())
		
        info['mac-address']=':'.join(re.findall('..', '%012x' % uuid.getnode()))
		
        info['processor']=platform.processor()
		
        info['ram']=str(round(psutil.virtual_memory().total / (1024.0 **3)))+" GB"
		
        return json.dumps(info)
		
    except Exception as e:
	
        logging.exception(e)

print(getSystemInfo())