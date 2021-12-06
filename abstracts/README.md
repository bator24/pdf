# Abstracts

```
> wdir <- "D:/mark"
> setwd(wdir)
> F <- dir(path="./abstracts")
> length(F)
[1] 416
> head(F)
[1] "abstract_2_Mode_Networks_1.txt"   "abstract_2_Mode_Networks_2.txt"  
[3] "abstract_2_Mode_Networks_3.txt"   "abstract_2_Mode_Networks_4.txt"  
[5] "abstract_Academic_Networks_1.txt" "abstract_Academic_Networks_2.txt"
> tail(F)
[1] "abstract_Visualization_5.txt" "abstract_Visualization_6.txt" "abstract_Viszards_1.txt"     
[4] "abstract_Web_Mining_1.txt"    "abstract_Web_Mining_2.txt"    "abstract_Web_Mining_3.txt"   
> F[1]
[1] "abstract_2_Mode_Networks_1.txt"
> gsub("abstract_","",gsub(".txt","",F[1]))
[1] "2_Mode_Networks_1"
> N <- gsub("abstract_","",gsub(".txt","",F))
> head(N)
[1] "2_Mode_Networks_1"   "2_Mode_Networks_2"   "2_Mode_Networks_3"   "2_Mode_Networks_4"  
[5] "Academic_Networks_1" "Academic_Networks_2"
> absF <- paste("./abstracts/",F[1],sep="")
> absF
[1] "./abstracts/abstract_2_Mode_Networks_1.txt"
> S <- readLines(absF)
> length(S)
[1] 8
> S
[1] "Presenter: Ronald Breiger"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
[2] "Title: Exploiting the Duality of Cases and Variables in QCA (Qualitative Comparative Analysis)"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        
[3] "Format: Lecture (20 mins)"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             
[4] "Session: 2-Mode Networks"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
[5] "Date and time: 03-14-2009 8:30am"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
[6] "Keywords: Methods, Two-mode Data, QCA (qualitative comparative analysis)"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
[7] ""                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
[8] "An innovative, highly developed, and widely influential strategy for conducting comparative social research is the Qualitative Comparative Analysis (QCA) approach of Charles Ragin. I think about QCA from the perspective of two-mode network analysis. I build upon a foundation of QCA, the duality of cases and variables. Within QCA, cases are productively understood as configurations of variables; at the same time, variables may be seen as configurations of cases. From the perspective of social network analysis of two-mode data, the key challenges are (1) how to deal with \"dependent variables,\" (2) how a large number of potential QCA \"solutions\" might be ordered with respect to their association with an outcome variable, (3) how to represent in a joint space the fundamental units of QCA, which are combinations of cases and combinations of variables, and (4) extensions to Ragin's fuzzy-set mode of QCA. The principal machinery brought to bear in this investigation is barycentric correspondence analysis, which is well-suited for set-theoretic work and its extensions. Applications are provided to the study of ethnic political mobilization and to other topics."
> regexpr(":", S)
[1] 10  6  7  8 14  9 -1 -1
attr(,"match.length")
[1]  1  1  1  1  1  1 -1 -1
attr(,"index.type")
[1] "chars"
attr(,"useBytes")
[1] TRUE
> C <- c("Pres","Titl","Form","Sess","Date","Key1","Key2","Key3","Key4","Key5","Key6","Abst")
> n <- length(F); m <- length(C)
> D <- as.data.frame(matrix(NA,nrow=n,ncol=m))
> row.names(D) <- N; names(D) <- C
> head(D)
                    Pres Titl Form Sess Date Key1 Key2 Key3 Key4 Key5 Key6 Abst
2_Mode_Networks_1     NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
2_Mode_Networks_2     NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
2_Mode_Networks_3     NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
2_Mode_Networks_4     NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
Academic_Networks_1   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
Academic_Networks_2   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA
> 

> i <- 1; k <- 1
> key <- substr(S[i],1,4)
> key
[1] "Pres"
> j <- regexpr(":", S)
> j
[1] 10  6  7  8 14  9 -1 -1
attr(,"match.length")
[1]  1  1  1  1  1  1 -1 -1
attr(,"index.type")
[1] "chars"
attr(,"useBytes")
[1] TRUE
> val <- substr(S[i],j[i]+2,nchar(S[i]))
> val
[1] "Ronald Breiger"
> D[k,key] <- val
> D[k,]
                            Pres Titl Form Sess Date Key1 Key2 Key3 Key4 Key5 Key6 Abst
2_Mode_Networks_1 Ronald Breiger   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA   NA

> k <- 1
> j <- regexpr(":", S)
> for(i in 1:5){
+    key <- substr(S[i],1,4); val <- substr(S[i],j[i]+2,nchar(S[i]))
+    cat(i,key,val,"\n")
+    D[k,key] <- val
+ }
> D[k,]

> key <- substr(S[6],1,4); val <- substr(S[6],j[i]+2,nchar(S[6]))
> keys <- trimws(unlist(strsplit(val,",")))
> for(j in 1:length(keys)) D[k,5+j] <- keys[j]
> D[k,"Abst"] <- S[8]


```

```
> F <- dir(path="./abstracts")
> N <- make.unique(gsub("abstract_","",gsub(".txt","",F)))
> C <- c("Pres","Titl","Form","Sess","Date","Key1","Key2","Key3","Key4","Key5","Key6","Abst")
> n <- length(F); m <- length(C)
> D <- as.data.frame(matrix(NA,nrow=n,ncol=m))
> names(D) <- C; row.names(D) <- N; 

> for(k in 1:length(F)){
+    absF <- paste("./abstracts/",F[k],sep="")
+    S <- gsub('"',"''",gsub("\t"," ",readLines(absF,encoding="UTF-8")))
+    # cat("***file",k,F[k],"\n"); flush.console()
+    if(S[7]!="") {cat("*** bad file",k,F[k],"\n"); flush.console(); next}
+    j <- regexpr(":", S)
+    for(i in 1:6){
+       if(length(j[i])>0){ji <- j[i][1]
+          key <- substr(S[i],1,4); val <- substr(S[i],ji+2,nchar(S[i]))
+          if(key=="Keyw"){
+             if(nchar(trimws(val))>0){
+                keys <- trimws(unlist(strsplit(tolower(val),",")))
+                keys <- keys[nchar(keys)>0]
+                for(j in 1:length(keys)) D[k,5+j] <- keys[j]
+             }          
+          } else D[k,key] <- val
+       } else {cat("***",k,i,F[k],"\n"); flush.console()}
+    }
+    D[k,"Abst"] <- paste(S[8:length(S)],collapse=" ")
+ }
> 

> dim(D)
> write.table(D,file="abstracts.csv",sep="\t",fileEncoding="UTF-8")

> A <- read.table(file="abstracts.csv",header=TRUE,sep="\t",row.names=1,fileEncoding="UTF-8")
> dim(A)

> save(D,file="abstracts.RData")


```
