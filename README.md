# Colaptes_PIRATE##

### Post CDHIST processing ###

#### Copy first column of PASTEC output into new .txt file (in this case named LINE.list.txt) ###

### Extract lines that match to a specific category (this case is written for LINEs). #### 

grep "LINE" PASTEC_first_column.csv > LINE.list.txt

#### Extract string that matches name of the sequences in those lines. ####

grep -Po '^"[a-zA-Z0-9]*' LINE.list1.txt > LINE.sequences.txt

#### Converting CDHIST output to one line per sequence #### 

awk '/^>/ {printf("\n%s\n",$0);next; } { printf("%s",$0);}  END {printf("\n");}' < Galaxy116-\[Cdhit-est_output\].fasta > one_line.fasta

### Adding > symbol to the start of each sequence name ### 
sed -i -e 's/^/>/' LINE.sequences.txt

### Extract sequences that match sequence names in LINE.sequences.txt ####
grep -A 1 -w -f LINE.sequences.txt one_line_LINE.fasta > LINE.fasta
