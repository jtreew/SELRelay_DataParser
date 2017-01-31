# SELRelay_DataParser
Data Parser for use with SEL Relay Settings Files

#Title: Main_Parser.py
#Version: 1.0
#Author: Joshua Watkins
#Release Date: 31 January 2017
#Description: Data Parser for use with SEL Relay Settings Files

#====================================================================
#                       ***PREFUNCTION SETUP***

#Import Key Python Libraries
import re

#Ask the user which file they would like to analyse
#No need to add the file extension as it is assumed to be a .txt file
fileName=input("What is the txt file? -- Example: SET_1 (No file extension) >>>")
fileName=fileName + ".txt"

#Identify the comma as the primary delimiter
keyword=","

#====================================================================
#                       ***PRIMARY FUNCTION***

def main():
    #Opens and reads the contents of a text file line by line
    file = open(fileName,"r")
    lines = file.readlines()
    #closes the document after reading in the lines
    file.close()

    #Define and initialise key variables used in the function
    findRID=0
    findTID=0
    findTR=0
    findCTR=0
    lineCount=0

    #Print the leading header for the results
    print("\nLine | Parameter | Setting")

    #Loop that will iterate through every line in the text file
    for line in lines:
        #removes needless carriage returns in the lines read
        line=line.strip()
        #iterates the line counter
        lineCount=lineCount+1

        #Utilises the REGEX library functionality to find exact matches of ...
        #...the parameter names below
        exactCTR=re.findall('\\bCTR\\b',line)
        exactRID=re.findall('\\bRID\\b',line)
        exactTID=re.findall('\\bTID\\b',line)
        exactTR=re.findall('\\bTR\\b',line)

        #conditional operators to perform actions upon finding ...
        #... exact matches in the string
        if exactCTR:
            #Iterates the counter related to this parameter
            findCTR=findCTR+1
            #Removes needless quotations
            line = line.replace('"', '').strip()
            #Returns string segments before and after delimiter found
            B_k, k_k, A_k = line.partition(keyword)
            #prints the values with specified padding or leading zeroes
            print("%03d" % lineCount," | ","%7s" %B_k," | ",A_k)
        if exactRID:
            #Iterates the counter related to this parameter
            findRID=findRID+1
            #Removes needless quotations
            line = line.replace('"', '').strip()
            #Returns string segments before and after delimiter found
            B_k, k_k, A_k = line.partition(keyword)
            #prints the values with specified padding or leading zeroes
            print("%03d" % lineCount," | ","%7s" %B_k," | ",A_k)
        if exactTID:
            #Iterates the counter related to this parameter
            findTID=findTID+1
            #Removes needless quotations
            line = line.replace('"', '').strip()
            #Returns string segments before and after delimiter found
            B_k, k_k, A_k = line.partition(keyword)
            #prints the values with specified padding or leading zeroes
            print("%03d" % lineCount," | ","%7s" %B_k," | ",A_k)
        if exactTR:
            #Iterates the counter related to this parameter
            findTR=findTR+1
            #Removes needless quotations
            line = line.replace('"', '').strip()
            #Returns string segments before and after delimiter found
            B_k, k_k, A_k = line.partition(keyword)
            #prints the values with specified padding or leading zeroes
            print("%03d" % lineCount," | ","%7s" %B_k," | ",A_k)


#====================================================================
#                       ***POSTFUNCTION***

#Calls the function
main()

#Creates a redundant dialog to signify the end of the process
input("\n\n***SCRIPT COMPLETE***")

#====================================================================
#                       ***FINAL COMMENTS***

'''
Generally this version is useful but only for fixed / static text files.
There is very little flexibility when you need to identify parameters
dynamically.

Needs work....
'''



