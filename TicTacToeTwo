'''
Created on Feb 29, 2020

@author: DekotaToot
'''
from tkinter import *
board=['a1','a2','a3','b1','b2','b3','c1','c2','c3']
rowOne=[board[0],board[1],board[2]]
rowTwo=[board[3],board[4],board[5]]
rowThree=[board[6],board[7],board[8]]
colOne=[board[0],board[3],board[6]]
colTwo=[board[1],board[4],board[7]]
colThree=[board[2],board[5],board[8]]
diaOne=[board[0],board[4],board[8]]
diaTwo=[board[2],board[4],board[6]]
gameState=[rowOne,rowTwo,rowThree,colOne,colTwo,colThree,diaOne,diaTwo]
def didIWin(l):
    for i in l:
        if i[0]==i[1]==i[2]:
            return True
    return False
def catGame(l):
    x=True
    if type(l)==str:
        if len(l)==2:
            return False
        else:
            return True
    if type(l)==list:
        for i in l:
            x= x and catGame(i) 
    return x
def replaceAll(old,new,l,b):
    for i in l:
        for j in i:
            if j==old:
                i.insert(i.index(old),new)
                i.remove(old)
    b.insert(b.index(old),new)
    b.remove(old)
def isRowFull(l):
    for i in l:
        if len(i)==2:
            return False
    return True
def winMove(c,l):
    for i in l:
        if c in i:
            if isRowFull(i)==False:
                counter=0
                for j in i:
                    if j==c: counter+=1
                if counter==2:
                    for h in i:
                        if h!=c: return h
    return
def moveScore(c,oc,b,l):
    score=[]
    for i in b:
        x=0
        if i==c or i==oc:
            score.append(0)
        else:
            for j in l:
                if i in j and c in j and not oc in j:
                    x+=1
            score.append(x)
    return score
def firstMoveScore(c,oc,b,l):
    score=[]
    for i in b:
        x=0
        if i==c or i==oc:
            score.append(0)
        else:
            for j in l:
                if i in j and not oc in j:
                    x+=1
            for k in l:
                if i in k and oc in k:
                    x+=.1
            score.append(x)
    return score
def tieBreaker(x):
    y=[]
    counter=1
    for i in x:
        y.append(i+.01*counter)
        counter+=1
    return y
def midMove(c,oc,b,l):
    if max(moveScore(c,oc,b,l))>=2:
        return b[tieBreaker(moveScore(c,oc,b,l)).index(max(tieBreaker(moveScore(c,oc,b,l))))]
    elif max(moveScore(oc,c,b,l))>=2:
        return b[tieBreaker(moveScore(oc,c,b,l)).index(max(tieBreaker(moveScore(oc,c,b,l))))]
    elif max(moveScore(c,oc,b,l))>=1:
        return b[tieBreaker(moveScore(c,oc,b,l)).index(max(tieBreaker(moveScore(c,oc,b,l))))]
    return
def startMove(c,oc,b,l):
    return b[tieBreaker(firstMoveScore(c,oc,b,l)).index(max(tieBreaker(firstMoveScore(c,oc,b,l))))]
play='x'
comp='o'
def goSecondBehavior(refx):
    compAct()
    refx['state']=DISABLED
def compAct():
    if winMove(comp,gameState)!=None:
        listOfButtons[originBoard.index(winMove(comp,gameState))]['state']=DISABLED
        listOfButtons[originBoard.index(winMove(comp,gameState))]['text']=comp.upper()
        replaceAll(winMove(comp,gameState),comp,gameState,board)
    elif winMove(play,gameState)!=None:
        listOfButtons[originBoard.index(winMove(play,gameState))]['state']=DISABLED
        listOfButtons[originBoard.index(winMove(play,gameState))]['text']=comp.upper()
        replaceAll(winMove(play,gameState),comp,gameState,board)
    elif midMove(comp, play, board, gameState)!=None:
        listOfButtons[originBoard.index(midMove(comp, play, board, gameState))]['state']=DISABLED
        listOfButtons[originBoard.index(midMove(comp, play, board, gameState))]['text']=comp.upper()
        replaceAll(midMove(comp, play, board, gameState),comp,gameState,board)
    elif startMove(comp, play, board, gameState)!=None:
        listOfButtons[originBoard.index(startMove(comp, play, board, gameState))]['state']=DISABLED
        listOfButtons[originBoard.index(startMove(comp, play, board, gameState))]['text']=comp.upper()
        replaceAll(startMove(comp, play, board, gameState),comp,gameState,board)
    if catGame(gameState)==True:
        winTitle['text']='It is a Draw'
    if didIWin(gameState)==True: 
        winTitle['text']='You Lose'
        for i in listOfButtons:
            i['state']=DISABLED
def playClick(c,s,refx):
    goSecond['state']=DISABLED
    replaceAll(s,c,gameState,board)
    refx['state']=DISABLED
    refx['text']=c.upper() 
    if catGame(gameState)==True:
        winTitle['text']='It is a Draw'
    if didIWin(gameState)==True: 
        winTitle['text']='You Win'
        for i in listOfButtons:
            i['state']=DISABLED
    if didIWin(gameState)==False and catGame(gameState)==False:
        compAct()
window=Tk()
winTitle=Label(master=window, text='TicTakToe')
winTitle.pack(side=TOP)
aFrame=Frame(window)
bFrame=Frame(window)
cFrame=Frame(window)
aFrame.pack(side=TOP)
bFrame.pack(side=TOP)
cFrame.pack(side=TOP)
a1=Button(master=aFrame,text='  ', command=lambda: playClick(play, 'a1', a1))
a2=Button(master=aFrame,text='  ', command=lambda: playClick(play, 'a2', a2))
a3=Button(master=aFrame,text='  ', command=lambda: playClick(play, 'a3', a3))
b1=Button(master=bFrame,text='  ', command=lambda: playClick(play, 'b1', b1))
b2=Button(master=bFrame,text='  ', command=lambda: playClick(play, 'b2', b2))
b3=Button(master=bFrame,text='  ', command=lambda: playClick(play, 'b3', b3))
c1=Button(master=cFrame,text='  ', command=lambda: playClick(play, 'c1', c1))
c2=Button(master=cFrame,text='  ', command=lambda: playClick(play, 'c2', c2))
c3=Button(master=cFrame,text='  ', command=lambda: playClick(play, 'c3', c3))
goSecond=Button(master=window,text='click to go second', command=lambda: goSecondBehavior(goSecond))
listOfButtons=[a1,a2,a3,b1,b2,b3,c1,c2,c3]
originBoard=['a1','a2','a3','b1','b2','b3','c1','c2','c3']
a1.pack(side=LEFT)
a2.pack(side=LEFT)
a3.pack(side=LEFT)
b1.pack(side=LEFT)
b2.pack(side=LEFT)
b3.pack(side=LEFT)
c1.pack(side=LEFT)
c2.pack(side=LEFT)
c3.pack(side=LEFT)
goSecond.pack(side=BOTTOM)
window.mainloop()
