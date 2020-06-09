# hi-c

## 1. intro

ref: http://www.bioinformatics.babraham.ac.uk/projects/hicup/read_the_docs/html/index.html#scripts-description

## 2. Procedure

QC --> Map --> filter(readlevel,read pair) --> normalization

Map: Hicup, there are a lot of tools for you to choose, hicup is one of them which are widely used.

The argument ‘–re1’ specifies the restriction enzyme used to digest the genome (a caret symbol ‘^’ is used to denote the restriction enzyme cut site, and a comma separates the DNA sequence from the restriction enzyme name). The argument ‘–genome’ is for specifying the name of the genome to be digested, it is NOT used to specify the path to the genome aligner indices.

–re1 A^GATCT,BglII:A^AGCTT,HindIII

```bash
# preparation bowtie index
#bowtie2-build 1.fa,2.fa,...,MT.fa Human_GRCh38

# hicup_digester find the enzyme clevage sites
# two enzymes: –re1 A^GATCT,BglII:A^AGCTT,HindIII
hicup_digester \
	--re1 $sites \
	--genome $ref \
	--outdir $digestDir \
	${ref}.fa

hicup \
	--bowtie2 $bowtie2 \
	--digest ${digestDir}/${ref}.fa \
	--format \
	--index $index \
	--keep \
	--outdir $outdir \
	--threads $threads \
	$input

# or you could run hicup config
# hicup --config $config



```