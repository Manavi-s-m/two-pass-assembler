class symtab():
     lab=[]
     add=[]
     n=0
st=symtab()
class ot():
     nem=["jsub","lda","comp","tix","sta","ldx","add","jlt","rsub"]
     opcode=["48","00","28","2C","0C","04","18","38","4C"]
optab=ot()
def searchs(s,stab):
     i=0
     while(i<stab.n):
          if(s==stab.lab[i]):
               return i
          i=i+1
     return -1
def printtab(stab):
     i=0
     while(i<stab.n):
          print("%s %s") %(stab.lab[i],stab.add[i])
          i=i+1
def searcho(s,otab):
     i=0
     while(i<9):
          if(s==otab.nem[i]):
               return i
          i=i+1
     return -1

def insert(s,val,st):
      st.n=st.n+1
      (st.lab).append(s)
      (st.add).append(val)
print("enter code")
a=[""]
i=0
name=" "
a[0]=raw_input()
spl=a[0].split(" ")
if spl[1]=='start':
     loc=(int(spl[2],16))
     name=spl[0]
     sa=loc
     a.append(raw_input())
     i=i+1
else:
     loc=0
while(a[i]!="end"):
          spl=a[i].split(" ")
          if(spl[0]!="-"):
               flags=searchs(spl[0],st)
               if(flags>=0):
                  print("Duplicate Lable")
               else:
                  insert(spl[0],hex(loc),st)
          flago=searcho(spl[1],optab)
          if(flago>=0):
             loc=(loc)+3
          elif(spl[1]=="word"):
             loc=(loc)+3
          elif(spl[1]=="resw"):
               loc=(loc)+3*int(spl[2])
          elif(spl[1]=="resb"):
               loc=loc+int(spl[2])
          elif(spl[1]=="byte"):
             loc=loc+len(spl[2])
          else:
             print("Invalid opcode")
          #print hex(loc)
          i=i+1
          a.append(raw_input())
a[i]="end"
leng=loc-sa
print ("Program length=%d") %leng
print("\nFIRST PASS - symtab")
printtab(st)

#PASS TWO
print("\nSECOND PASS")
load=[]
temp="H^"+name+"^"+hex(sa)+"^"+str(leng)
load.append(temp)
i=1
j=1
while(a[i]!="end"):
     spl=a[i].split(" ")
     if(spl[1]=="byte" or spl[1]=="word"):
          temp="T^"+spl[2]
          load.append(temp)
          i=i+1
          j=j+1
          continue
     elif(spl[1]=="resb" or spl[1]=="resw"):
          i=i+1
          continue
     flago=searcho(spl[1],optab)
     if(flago>=0):
          op=optab.opcode[flago]
     spp=spl[2].split(",")
     if(spp[0]!=spl[2]):
          if(spp[1]=="x"):
               x=1
          else:
               x=0
     else:
          x=0
     flags=searchs(spp[0],st)
     if(flags>=0):
          ad=(st.add[flags])
     else:
          ad=hex(0000)
     i=i+1
     
     temp="T^"+op+"^"+str(x)+"^"+(ad)
     load.append(temp)
     j=j+1
temp="E^"+hex(sa)
load.append(temp)
k=0
while (k<=j):
     print (load[k])
     k=k+1
     
class ld:
     adr=[]
     value=[]
l=ld()
#LOADER
print("\nLOADER")
print("Program name is %s") % name
sh=load[1].split("^")
i=2
sad=sa
while(sh[0]!="E"):
     if(load[i-1].count("^")==1):
          sh=load[i].split("^")
          i=i+1
          continue
     l.adr.append(hex(sad))
     sad=sad+1
     l.value.append(hex(int(sh[1],16)))
     l.adr.append(hex(sad))
     sad=sad+1
     temp=(sh[3])[2:4]
     if(sh[2]=="1"):
          temp1=temp[0:1]
          temp1=int(temp1)
          temp1=temp1+8
          temp1=hex(temp1)
          temp2=temp[1:2]
          temp=temp1+temp2
     else:
          temp=hex(int(temp,16))
     l.value.append(temp)
     l.adr.append(hex(sad))
     if(len(sh[3])<6):
          l.value.append("0x00")
     else:
          temp=(sh[3])[4:6]
          l.value.append(hex(int(temp,16)))
     sh=load[i].split("^")
     i=i+1
     
j=0
i=len(l.value)
while (j<i):
     print("%s %s") %(l.adr[j],l.value[j])
     j=j+1
print("Control go to %s" % hex(sa))
