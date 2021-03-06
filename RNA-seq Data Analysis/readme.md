# RNA-seq Data Analysis Pipeline
## Connect to linux server 
Open a terminal and type <br /> `ssh username@ieng6-###.ucsd.edu`
## TOPHAT-CUFFLINK Pipeline
First let's create some target directories with the following commands
``` 
mkdir geneExpression
cd geneExpression
mkdir alignments 
mkdir fpkm       
mkdir diff       
```

Then we can use TOPHAT to align the reads to genes with the following template command <br />
`tophat -p 1 -G /path/to/genes.gtf -o out/dir  path/to/genome/index* path/to/reads_R1.fastq path/to/reads_R1.fastq` <br />
To align all the fastq files from the example data at the same time, we can create a shell script <br />
```
cd alignments
vi alignment.sh
reads=/home/linux/ieng6/be183f/public/bengTutorial/fastq    # address where the fastq files are stored
genes=/home/linux/ieng6/be183f/public/bengTutorial/index_gtf/genes4.gtf   # this contain information about the positions of genes on the genome
# Tophat need to know where is the reference genome, we'll create soft-links in of the reference genome in the current folder
for file in /home/linux/ieng6/be183f/public/bengTutorial/index_gtf/4*; do
       ln -s $file .
done

tophat -p 1 -G $genes -o C1_R1 4 ${reads}/GSM794483_C1_R1_1.ss.fq ${reads}/GSM794483_C1_R1_2.ss.fq &
tophat -p 1 -G $genes -o C1_R2 4 ${reads}/GSM794484_C1_R2_1.ss.fq ${reads}/GSM794484_C1_R2_2.ss.fq &
tophat -p 1 -G $genes -o C2_R1 4 ${reads}/GSM794486_C2_R1_1.ss.fq ${reads}/GSM794486_C2_R1_2.ss.fq &
tophat -p 1 -G $genes -o C2_R2 4 ${reads}/GSM794487_C2_R2_1.ss.fq ${reads}/GSM794487_C2_R2_2.ss.fq &
```
Next we quit and save the script by typing: `:wq` Then we run the script by typing: `bash alignment.sh` <br />
After the alignment step is finished, we use Cufflink to quantify the gene expression <br />
A template Cufflink command is like the following <br />
`cufflink -p 1 -G path/to/genes.gtf -o path/to/outdir path/to/accepted_hits.bam`
We can also write a shell script to execute the files all at once <br />
```
$ cd fpkm  # get into the fpkm folder
$ vi fpkm.sh
genes=/home/linux/ieng6/be183f/public/bengTutorial/index_gtf/genes4.gtf
alignments=../alignments

for condition in C1 C2; do
for replicate in R1 R2; do
   echo ${condition}_${replicate}
   cufflinks -p 1 -G $genes -o ${condition}_${replicate} ${alignments}/${condition}_${replicate}/accepted_hits.bam
done; done
```
We quit and save the script by typing: `:wq` Then we run the script by typing: `bash fpkm.sh` <br />
Here, genes.fpkm_tracking and isoforms.fpkm_tracking contains gene expression values (measured as FPKM) at the gene and transcript levels.

##STAR-Kallisto Pipeline
