#UNIX Assignment

##Data Inspection
###Attributes of fang_et_al_genotypes
By inspecting this file I learned that:
1.line:2783  word: 2744038 byte:11051939 filename:fang_et_al_genotypes.txt
2.column of fang_et_al_genotypes.txt: 986

###Attributes of snp_position.txt
By inspecting this file I learned that:
1.line:984 word:13198 byte:82763 filename:snp_position.txt
2.column of snp_position.txt: 15

##Data Processing                                                                          
$ egrep "ZMMLR|ZMMIL|ZMMMR|Sample_ID" fang_et_al_genotypes.txt > maize_fang_et_al_genotypes.txt #grep ZMMLR or ZMMIL or ZMMMR
$ egrep "ZMPBA|ZMPIL|ZMPJA|Sample_ID" fang_et_al_genotypes.txt > teosinte_fang_et_al_genotypes.txt #grep ZMPBA, ZMPIL, and ZMPJA
$ awk -f transpose.awk teosinte_fang_et_al_genotypes.txt > teosinte_transposed_genotypes.txt $ awk -f transpose.awk maize_fang_et_al_genotypes.txt > maize_transposed_genotypes.txt
$ mkdir Data-Processing
###Maize Data

###Teosinte Data
$ sed -i '1,3d' maize_transposed_genotypes.txt teosinte_transposed_genotypes.txt #delete Sample_ID, JG_OTU, and Group lines
$ sed '1d' snp_position.txt > snp_position_nonhead.txt #delete the head of snp
$ sort -k1,1V snp_position_nonhead.txt > snp_position_nonhead_sorted.txt #sort and save snp
$ sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.txt #sort maize
$ sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.txt #sort teosinte
$ join -1 1 -2 1 -t $'\t' snp_position_nonhead_sorted.txt maize_transposed_genotypes_sorted.txt > maize_transposed_genotypes_joined.bed #join snp with maize
$ join -1 1 -2 1 -t $'\t' snp_position_nonhead_sorted.txt teosinte_transposed_genotypes_sorted.txt > teosinte_transposed_genotypes_joined.bed #join snp with teosinte 
------teosinte------ 
$ sort -k3,3 teosinte_transposed_genotypes_joined.bed > teosinte_transposed_genotypes_joined_chr.bed #sort chrom colum
$ grep -v "^#" teosinte_transposed_genotypes_joined_chr.bed | cut -f3 | uniq -c #count chromosome
---output--- 155 1 53 10 127 2 107 3 91 4 122 5 76 6 97 7 62 8 60 9 6 multiple 27 unknown
$ sed -n '1,155p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr1.bed #chrom1 
$ sed -n '156,208p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr10.bed 
$ sed -n '209,335p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr2.bed
$ sed -n '336,442p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr3.bed 
$ sed -n '443,533p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr4.bed 
$ sed -n '534,655p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr5.bed 
$ sed -n '656,731p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr6.bed 
$ sed -n '732,828p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr7.bed 
$ sed -n '829,890p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr8.bed 
$ sed -n '891,950p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr9.bed 
$ sed -n '951,956p' teosinte_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_mutiple.bed 
$ sed -n '957,983p' teosinte_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_unknown.bed
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr9.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr9_ordered_increased.bed #ordered based on increasing position values and with missing data encoded by this symbol: ? 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr8.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr8_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr7.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr7_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr6.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr6_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr5.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr5_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr4.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr4_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr3.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr3_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr2.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr2_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr1.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr1_ordered_increased.bed 
$ sort -k4,4V teosinte_transposed_genotypes_joined_chr10.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr10_ordered_increased.bed

#decreasing position values and with missing data encoded by this symbol: -
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr8.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr8_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr1.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr1_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr2.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr2_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr3.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr3_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr4.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr4_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr5.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr5_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr6.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr6_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr7.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr7_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr9.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr9_ordered_decreased.bed
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr10.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr10_ordered_decreased.bed
------maize----- 
$ sort -k3,3 maize_transposed_genotypes_joined.bed > maize_transposed_genotypes_joined_chr.bed #sort chrom column
$ sed -n '1,155p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr1.bed #chrom1 
$ sed -n '156,208p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr10.bed 
$ sed -n '209,335p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr2.bed 
$ sed -n '336,442p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr3.bed 
$ sed -n '443,533p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr4.bed 
$ sed -n '534,655p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr5.bed 
$ sed -n '656,731p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr6.bed 
$ sed -n '732,828p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr7.bed 
$ sed -n '829,890p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr8.bed 
$ sed -n '891,950p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr9.bed 
$ sed -n '951,956p' maize_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_mutiple.bed 
$ sed -n '957,983p' maize_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_unknown.bed

$ sort -k4,4V maize_transposed_genotypes_joined_chr9.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr9_ordered_increased.bed #ordered based on increasing position values and with missing data encoded by this symbol: ? $ sort -k4,4V maize_transposed_genotypes_joined_chr8.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr8_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr7.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr7_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr6.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr6_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr5.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr5_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr4.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr4_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr3.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr3_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr2.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr2_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr1.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr1_ordered_increased.bed 
$ sort -k4,4V maize_transposed_genotypes_joined_chr10.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr10_ordered_increased.bed

#decreasing position values and with missing data encoded by this symbol: -

$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr8.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr8_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr1.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr1_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr2.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr2_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr3.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr3_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr4.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr4_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr5.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr5_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr6.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr6_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr7.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr7_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr9.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr9_ordered_decreased.bed
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr10.bed | sort -k4,4nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr10_ordered_decreased.bed



