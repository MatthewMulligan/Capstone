# Capstone
#Final Project
#Names: Matthew Mulligan, Adam Schulze

#from stemming.porter2 import stem


class TextModel:

    def __init__(self, name):
        """ the constructor for the TextModel class
            all dictionaries are started at empty
            the name is just for our own purposes, to keep things 
            organized
        """
        self.name = name
        self.words = {}   # starts empty
        self.wordlengths = {}
        self.stems = {}
        self.sentencelengths = {}
        # you will want another dictionary for your text feature


    def __repr__(self):
        """ this method creates the string version of TextModel objects
        """
        s  = "\nModel name: " + str(self.name) + "\n"
        s += "    n. of words: " + str(len(self.words))  + "\n"
        s += "    n. of word lengths: " + str(len(self.wordlengths))  + "\n"
        s += "    n. of sentence lengths: " + str(len(self.sentencelengths))  + "\n"
        s += "    n. of stems: " + str(len(self.stems))  + "\n"
        # you will likely want another line for your custom text-feature!
        return s

    def readTextFromFile(self, filename):
        """Takes in string filename and returns text file as single long string"""
        f = open(filename)
        text = f.read()
        f.close()
        return text

    def makeSentenceLengths(self, s):
        """Takes text as input string and creates self.sentencelengths dictionary"""
        y = s.replace('!','.')
        z = y.replace('?','.')
        LoS = z.split('.')
        LoL = {}
        #Fix This
        n = 1
        for i in LoS:
            for j in i:
                if j == ' ':
                    n+=1
            LoL+=n
            n=0
        return LoL{:-1}

    def cleanString(self, s):
        """Takes in a string s and return a string with no punctuation and no upper-case letters"""
        for i in range(len(s)):
            c = s[i]
            if c in '.?!,:;':
                s = s.replace(c, ' ')
            if 'A' <= c <= 'Z':
                new_ord = ord(c) + 32
                q = chr(new_ord)
                s = s.replace(c, q)
        s = s.replace('  ', ' ')
        if s[-1] == ' ':
            s = s[:-1]
        return s

    def makeWords(self, s):
        """Uses text input string to create self.words dictionary"""
        self.words = {}
        s = self.cleanString(s)
        pw = '$'
        LoW = s.split()
        for nw in LoW:
            if pw == '$':
                pw = nw
            elif pw not in self.words:
                self.words[pw] = 1
                pw = nw
            else:
                self.words[pw] += 1
                pw = nw
        self.Words[pw] += 1
        return self.words

    def makeWordLengths(self, s):
        """Takes in text input string and creates dictionary of word lengths"""
        self.wordlengths = {}
        s = self.cleanString(s)
        pw = '$'
        LoW = s.split()
        for nw in LoW:
            if pw == '$':
                pw = nw
            elif len(pw) not in self.wordlengths:
                self.wordlengths[len(pw)] = 1
                pw = nw
            else:
                self.wordlengths[len(pw)] += 1
                pw = nw
        self.wordlengths[len(pw)] += 1
        return self.wordlengths

    def makeStems(self, s):
        """Takes in text input and creates a dictionary of stems."""


    def printAllDictionaries(self):
        """Prints out all five dictionaries to examine"""
        print self.words  
        print self.wordlengths 
        #print self.stems 
        print self.sentencelengths 

