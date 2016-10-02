Terminal  
===  
ssh bandit4@bandit.labs.overthewire.org  
bandit4@bandit.labs.overthewire.org's password: pIwrPrtPN36QITSp3EQaw936yaFoFgAB  
bandit4@melinda:~$ ls  
inhere  
bandit4@melinda:~$ cd inhere  
bandit4@melinda:~/inhere$ ls  
-file00  -file02  -file04  -file06  -file07~  -file09  
-file01  -file03  -file05  -file07  -file08  
bandit4@melinda:~/inhere$ file ./-*  
./-file00:  data  
./-file01:  data  
./-file02:  data  
./-file03:  data  
./-file04:  data  
./-file05:  data  
./-file06:  data  
./-file07:  ASCII text  
./-file07~: regular file, no read permission  
./-file08:  data  
./-file09:  data   
bandit4@melinda:~/inhere$ cat ./-file07  
koReBOKuIDDepwhWk7jZC0RTdopnAYKh  

