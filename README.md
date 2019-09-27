#UNIX Assignment

##Data Inspection
###Attributes of fang_et_al_genotypes
By inspecting this file I learned that:
line:2783  word: 2744038 byte:11051939 filename:fang_et_al_genotypes.txt
column of fang_et_al_genotypes.txt: 986

###Attributes of snp_position.txt
By inspecting this file I learned that:
line:984 word:13198 byte:82763 filename:snp_position.txt
column of snp_position.txt: 15
##Data Processing

###Maize Data

here is my snippet of code used for data processing
Here is my brief description of what this code does

###Teosinte Data

here is my snippet of code used for data processing
Here is my brief description of what this code does



awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt#transpose fang_et_al_genotypes.txt
