#Дерево с узлами и ссылками (не дерево поиска)
class Tree:
    def __init__(self,new):
        self.info=new
        self.right=None
        self.left=None
    def push_right(self,new):
        if self.right==None:
            self.right=Tree(new)
        else:
            t=Tree(new)
            t.right=self.right
            self.right=t
    def push_left(self,new):
        if self.left==None:
            self.left=Tree(new)
        else:
            t=Tree(new)
            t.left=self.left
            self.left=t
    def getleft(self):
        return self.left
    def getright(self):
        return self.right
    def setinfo(self,new):
        self.info=new
    def getinfo(self):
        return self.info
    def infix(self):
        if self.left:
            self.left.infix()
        print(self.info)
        if self.right:
            self.right.infix()
    def postfix(self):
        if self.left:
            self.left.postfix()
        if self.right:
            self.right.postfix()
        print(self.info)
    def prefix(self):
        print(self.info)
        if self.left:
            self.left.prefix()
        if self.right:
            self.right.prefix()
    
#дерево синтаксического разбора  AST
from stack_and_sort import stack
from infix_to_prefix import primer
def sintax(expr):
    token=expr.split()
    st=stack()
    current=Tree('')
    st.push(current)
    for i in token:
        if i=='(':
            current.push_left('')
            st.push(current)
            current=current.getleft()
        elif i not in '+-*/)':
            current.setinfo(int(i))
            current=st.pop()
        elif i in '+-*/':
            current.setinfo(i)
            current.push_right('')
            st.push(current)
            current=current.getright()
        elif i==')':
            current=st.pop()
    return current

pred="( 2 * ( 2 + 5 ) )"
tr=sintax(pred)  #результат после вычисления переходит в экземпляр класса tr

#1 метод просчета с помощью файла и стэка
import sys
f=open('text1.txt','w')
saveout=sys.stdout
sys.stdout=f
tr.postfix()
sys.stdout=saveout
f.close()

f=open('text1.txt.','r')
s=f.read()
s=s.split('\n')
s=s[:-1]
f.close()
rez=primer(s)

import operator
#2 метод через рекурсию
def rez(parseTree):
       opers = {'+':operator.add, '-':operator.sub, '*':operator.mul, '/':operator.truediv}
       leftC = parseTree.getleft()
       rightC = parseTree.getright()
       if leftC and rightC:
           fn = opers[parseTree.getinfo()]
           return fn(rez(leftC),rez(rightC))
       else:
           return parseTree.getinfo()        

