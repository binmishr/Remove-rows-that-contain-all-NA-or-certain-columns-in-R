# Remove-rows-that-contain-all-NA-or-certain-columns-in-R

In this article, we are going to discuss how to remove NA values from a data frame.

How to clean the datasets in R? » janitor Data Cleansing »
Remove rows that contain all NA or certain columns in R?
1. Remove rows from column contains NA

If you want to remove the row contains NA values in a particular column, the following methods can try.
Method 1: Using drop_na()

Create a data frame

df=data.frame(Col1=c("A","B","C","D",
                          "P1","P2","P3")
                   ,Col2=c(7,8,NA,9,10,8,9)
                   ,Col3=c(5,7,6,8,NA,7,8)
                   ,Col4=c(7,NA,7,7,NA,7,7))
df
    Col1 Col2 Col3 Col4
 1    A    7    5    7
 2    B    8    7   NA
 3    C   NA    6    7
 4    D    9    8    7
 5   P1   10   NA   NA
 6   P2    8    7    7
 7   P3    9    8    7
library(tidyr)
df %>% drop_na(Col2)
   Col1 Col2 Col3 Col4
1    A    7    5    7
2    B    8    7   NA
3    D    9    8    7
4   P1   10   NA   NA
5   P2    8    7    7
6   P3    9    8    7

Method 2: Using is.na()

Create a data frame

df=data.frame(Col1=c("A","B","C","D",
                     "P1","P2","P3")
              ,Col2=c(7,8,NA,9,10,8,9)
              ,Col3=c(5,7,6,8,NA,7,8)
              ,Col4=c(7,NA,7,7,NA,7,7)) 
df[!is.na(df$Col3),]
   Col1 Col2 Col3 Col4
1    A    7    5    7
2    B    8    7   NA
3    C   NA    6    7
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

Method 3:Using complete.cases()

df=data.frame(Col1=c("A","B","C","D",
                     "P1","P2","P3")
              ,Col2=c(7,8,NA,9,10,8,9)
              ,Col3=c(5,7,6,8,NA,7,8)
              ,Col4=c(7,NA,7,7,NA,7,7))
df[complete.cases(df$Col4),]
   Col1 Col2 Col3 Col4
1    A    7    5    7
3    C   NA    6    7
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

Method 4:Using which()

df=data.frame(Col1=c("A","B","C","D",
                     "P1","P2","P3")
              ,Col2=c(7,8,NA,9,10,8,9)
              ,Col3=c(5,7,6,8,NA,7,8)
              ,Col4=c(7,NA,7,7,NA,7,7))
df[-which(is.na(df$Col3)),]
   Col1 Col2 Col3 Col4
1    A    7    5    7
2    B    8    7   NA
3    C   NA    6    7
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

2. Remove Rows with contains some missing NA values
Method 1:Using na.omit() Function

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
df
   Col1 Col2 Col3 Col4
 1    NA   NA   NA  NA
 2    B    8    7   NA
 3    C   NA    6    7
 4    D    9    8    7
 5   P1   10   NA   NA
 6   P2    8    7    7
 7   P3    9    8    7
na.omit(df)
   Col1 Col2 Col3 Col4
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

Method 2:Using complete.cases() Function

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
df[complete.cases(df), ]
   Col1 Col2 Col3 Col4
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

Method 3:Using rowSums() & is.na() Functions

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
df[rowSums(is.na(df)) == 0, ]
  Col1 Col2 Col3 Col4
4    D    9    8    7
6   P2    8    7    7
7   P3    9    8    7

Method 4:Using Using drop_na() Function

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
library(tidyr)
df %>% drop_na() 
   Col1 Col2 Col3 Col4
1    D    9    8    7
2   P2    8    7    7
3   P3    9    8    7

3. Row which contains all column values that are missing

Suppose if you want to remove all column values contains NA then following codes will be handy.
Method 1:Using  is.na(), rowSums() & ncol() Functions

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
df[rowSums(is.na(df)) != ncol(df), ]
Col1 Col2 Col3 Col4
2    B    8    7   NA
3    C   NA    6    7
4    D    9    8    7
5   P1   10   NA   NA
6   P2    8    7    7
7   P3    9    8    7

Method 2:Using  Using filter() Function

df=data.frame(Col1=c(NA,"B","C","D",
                     "P1","P2","P3")
              ,Col2=c(NA,8,NA,9,10,8,9)
              ,Col3=c(NA,7,6,8,NA,7,8)
              ,Col4=c(NA,NA,7,7,NA,7,7))
library("dplyr")
filter(df, rowSums(is.na(df)) != ncol(df))
   Col1 Col2 Col3 Col4
1    B    8    7   NA
2    C   NA    6    7
3    D    9    8    7
4   P1   10   NA   NA
5   P2    8    7    7
6   P3    9    8    7
