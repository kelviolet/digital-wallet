#! /usr/bin/python
import re

f=open('./paymo_input/batch_payment.txt')

dic={}
for line in f.readlines()[1:]:
    tmp=line.split()
    tmp[2]=tmp[2].rstrip(',')
    tmp[3]=tmp[3].rstrip(',')
    i1=int(tmp[2])
    i2=int(tmp[3])
    if i1 not in dic:
       dic[i1]=[]
       dic[i1].append(i2)
       if i2 not in dic:
          dic[i2]=[]
          dic[i2].append(i1)
       else:
          if i1 not in dic[i2]:
             dic[i2].append(i1)
    else:
       if i2 not in dic[i1]:
          dic[i1].append(i2)
       if i2 not in dic:
          dic[i2]=[]
          dic[i2].append(i1)
       else:
          if i1 not in dic[i2]:
             dic[i2].append(i1)   
       

             
df=open('./paymo_input/stream_payment.txt')

for line in df.readlines()[1:]:       
    dmp=line.split()
    dmp[2]=dmp[2].rstrip(',')
    dmp[3]=dmp[3].rstrip(',')
    j1=int(dmp[2])
    j2=int(dmp[3])

 # feature 1
    outf1=open('./paymo_output/output1.txt','a')
    if j1 in dic:
       if j2 in dic[j1]:
          outf1.write('trusted\n')
          outf1.close()
       else:
          outf1.write('unverified\n')
          outf1.close()
    else:
       outf1.write('unverified\n')   
    
# feature2
    outf2=open('./paymo_output/output2.txt','a')
    if j1 in dic:
       if j2 in dic[j1]:
          outf2.write('trusted\n')
       else:
          k=len(dic[j1])
          for x in dic[j1]:
              k-=1
              if j2 in dic[x]:
                 outf2.write('trusted\n')
                 break
              if k==0:
                 outf2.write('unverified\n')
                 break    
    else:
       outf2.write('unverified\n')
       outf2.close()

# feature3    
    outf3=open('./paymo_output/output3.txt','a')
    level=0
    leveln=4
    
 
    def indic(p1,p2,level):
        if level>leveln:
           return False
        else:
           if p1 in dic:
              if p2 in dic[p1]:
                 return True             
              else:
                 level+=1         
                 for x in dic[p1]:
                     return indic(x,p2,level)
           else:
              return False     
                
           
    if indic(j1,j2,level):
       outf3.write('trusted\n')
    else:
       outf3.write('unverified\n')

                          
