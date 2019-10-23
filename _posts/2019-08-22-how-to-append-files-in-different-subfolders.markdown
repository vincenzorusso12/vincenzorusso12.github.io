---
title: "How to append files with the same name from different subfolders in R"
layout: post
date: 2019-10-23 12:48
image: /assets/images/markdown.jpg
headerImage: false
tag:
- R
- components
- extra
category: blog
author: vincenzorusso
description: append files with the same name from different subfolders in R
---

## The problem

During my thesis I've found myself dealing with some **text files** called Corpus.
For each patient I had one Corpus. Every patient has many visits, we could think each visit as a different **subfolder**.<br>
In each of those we have a file called Patient1870.txt, we want to create a new file which has the content of the 3 files in these subfolders.




<br>
* Parent Folder
    * Visit 1
    * Visit 2
    * Visit 3
    
<br>
<br>
## How to do it in R


```r
setwd("/home/vincenzo/Scrivania/TestAppendCorpusWorking") #Working folder
out<- read.csv("Patient_Status.csv",header = TRUE) #List of all patients

visite<-c("SC","BL","V01","V02","V03","V04","V05","V06","V07") #Number of visits or subdirectories
sourceFolder<-"/home/vincenzo/Scrivania/TestAppendCorpusWorking"#Parent directory of our subdirectories
destFolder<-"/home/vincenzo/Scrivania/TestAppendCorpusWorking/SC-V07/Corpus/"
    
for (i in 1:nrow(out)) {
  ith <- out[i,2]
  fileToWrite <- paste0(destFolder,ith,".txt") #For each element in our patient list create an empty file
    for (j in 1:length(visite)) { #For each file to wrirte visit the subdirectories and append the file with the same name
          fileToRead <- paste(sourceFolder,visite[j],"Corpus",paste0(ith,".txt"), sep="/")
      file.append(fileToWrite, fileToRead)
    }
}

```