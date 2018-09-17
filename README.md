# d8-pandas

import pandas as pd

XYZ_web = {'Name':['Li','Bob','Jane','Mike'],'grade':[90,80,95,70]}
df = pd.DataFrame(XYZ_web)
print(df) =>    Name  grade
             0    Li     90
             1   Bob     80
             2  Jane     95
             3  Mike     70

XYZ_web = {'Day':[1,2,3,4,5,6],'Visitors':[1000,700,6000,1000,400,350],'Bounce_rate':[20,20,23,15,10,34]}
df=pd.DataFrame(XYZ_web)
print(df) =>   Day  Visitors  Bounce_rate
            0    1      1000           20
            1    2       700           20
            2    3      6000           23
            3    4      1000           15
            4    5       400           10
            5    6       350           34
#slicing
print(df.head(2)) =>   Day  Visitors  Bounce_rate
                    0    1      1000           20
                    1    2       700           20 
print(df.tail(2)) =>   Day  Visitors  Bounce_rate
                    4    5       400           10
                    5    6       350           34

#merging
df1 = pd.DataFrame({'HPI':[80,90,70,60],'Int_rate':[2,1,2,3],'IND_GDP':[50,45,45,67]},
                   index = [2001,2002,2003,2004])
df2 = pd.DataFrame({'HPI':[80,90,70,60],'Int_rate':[2,1,2,3],'IND_GDP':[50,45,45,67]},
                   index = [2005,2006,2007,2008])
merge = pd.merge(df1,df2)
print(merge) =>    HPI  Int_rate  IND_GDP
                0   80         2       50
                1   90         1       45
                2   70         2       45
                3   60         3       67
print(pd.merge(df1,df2,on = ('HPI','Int_rate'))) =>    HPI  Int_rate  IND_GDP_x  IND_GDP_y
                                                    0   80         2         50         50
                                                    1   90         1         45         45
                                                    2   70         2         45         45
                                                    3   60         3         67         67

#joining
df1 = pd.DataFrame({'Int_rate':[2,1,2,3],'IND_GDP':[50,45,45,67]},
                   index = [2001,2002,2003,2004])
df2 = pd.DataFrame({'Low_Tier_HPI':[50,45,67,34],'Unemployment':[1,3,5,6]},
                   index = [2001,2003,2004,2004])
joined=df1.join(df2)
print(joined) =>       Int_rate  IND_GDP  Low_Tier_HPI  Unemployment
                 2001         2       50          50.0           1.0
                 2002         1       45           NaN           NaN
                 2003         2       45          45.0           3.0
                 2004         3       67          67.0           5.0
                 2004         3       67          34.0           6.0

#set_index()
df = pd.DataFrame({'Day':[1,2,3,4],'Visitors':[200,100,230,300],'Bounce_rate':[20,45,60,10]})
df.set_index('Day',inplace=True)
print(df) =>      Visitors  Bounce_rate
             Day                       
             1         200           20
             2         100           45
             3         230           60
             4         300           10

#columns
df = pd.DataFrame({'Day':[1,2,3,4],'Visitors':[200,100,230,300],'Bounce_rate':[20,45,60,10]})
df = df.rename(columns={'Visitors':'Users'})
print(df) =>    Day  Users  Bounce_rate
             0    1    200           20
             1    2    100           45
             2    3    230           60
             3    4    300           10
             
#concatenation
df1 = pd.DataFrame({'HPI':[80,90,70,60],'Int_rate':[2,1,2,3],'IND_GDP':[50,45,45,67]},
                   index = [2001,2002,2003,2004])
df2 = pd.DataFrame({'HPI':[80,90,70,60],'Int_rate':[2,1,2,3],'IND_GDP':[50,45,45,67]},
                   index = [2005,2006,2007,2008])
concat = pd.concat([df1,df2])
print(concat) =>       HPI  Int_rate  IND_GDP
                 2001   80         2       50
                 2002   90         1       45
                 2003   70         2       45
                 2004   60         3       67
                 2005   80         2       50
                 2006   90         1       45
                 2007   70         2       45
                 2008   60         3       67
                 
#statistics
from statistics import variance,mean,mode,median

print(variance([1,1,1,1,3,4,4,4,5,2])) =>2.488888888888889
print(mean([1,1,1,1,3,4,4,4,5,2])) => 2.6
print(mode([1,1,1,1,3,4,4,4,5,2])) => 1
print(median([1,1,1,1,3,4,4,4,5,2])) => 2.5
