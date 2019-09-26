#UNIX Assignment

##Data Inspection

###Attributes of fang_et_al_genotypes

here is my snippet of code used for data inspection
By inspecting this file I learned that:

point 1
point 2
point 3
or

point 1
point 2
point 3
###Attributes of snp_position.txt

here is my snippet of code used for data inspection
By inspecting this file I learned that:

point 1
point 2
point 3
or

point 1
point 2
point 3
##Data Processing

###Maize Data

here is my snippet of code used for data processing
Here is my brief description of what this code does

###Teosinte Data

here is my snippet of code used for data processing
Here is my brief description of what this code does

#UNIX Assignment
##line:2783  word: 2744038 byte:11051939 filename:fang_et_al_genotypes.txt
#line:984 word:13198 byte:82763 filename:snp_position.txt
-rw-r--r--. 1 pyang19 domain users 11051939 Sep 13 13:33 fang_et_al_genotypes.txt
-rw-r--r--. 1 pyang19 domain users    82763 Sep 13 13:33 snp_position.txt
column of fang_et_al_genotypes.txt: 986
column of snp_position.txt: 15
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt#transpose fang_et_al_genotypes.txt
