
# ChIP Sequencing 
## History of ChIP Sequencing
ChIP-Seq was originally invented by Dr. Keji Zhao in 2007. At the time, there were at least three separate groups new techniques for genome-wide protein binding assay, and there was a race among the three groups.  Dr. Zhao’s team first completed the development of this next generation sequencing based technique and submitted their work to journal.
## The Goal of ChIP-Seq
It has been known that various proteins bind to the genome. We are interested in where proteins bind to on the genome. Based on binding sites of different proteins in different cells, we can predict regulation of genes in certain cells. Furthermore, we can study common binding sequence of certain protein and derive its binding motif.
## Targets of ChIP-Seq
* Transcription factor: Transcription factors (TF) are proteins that bind to DNA and initialize transcription. There two types of TF binding sites, core promoter and proximal promoter. Core promoter contains the transcription start site and is the binding site of RNA polymerase. About 200-300 TFs bind to core promoter. Core promoters are present in all cells. On the other hand, proximal Promoter only regulate some genes and their sequencing vary in different cells. They are located upstream of core promoters, and about 1400 TFs bind to them. 
* Nucleosome: Nucleosome is the structure of DNA coiling around the core of 8 histones.
* Histone modification: Histone modifications are modifications on histone proteins including methylation and phosphorylation. 
* Insulator: By blocking of interaction sites, insulators prevent distal enhancers from acting on promoter of nearby gene.
## Workflow of ChIP-Seq
1. Use formaldehyde to cross-link cells and fix protein on where they bind on the genome.
2. Use restriction enzymes or sonification to sheer DNA into fragments.
3. Use target protein specific antibody to select DNA fragments where our target protein bind, and wash away the rest of the DNAs.
4. Reverse the crosslink and select out only DNA fragments.
5. Perform next generation sequencing on the selected DNA fragments and align resulting reads to the reference genome for further analyses.
## Introduction to raw data of ChIP-Seq
The raw data of ChIP-Seq are in reads stored in fastq format. In the fastq file, each four line represents one single read. The first of the four lines begins with a “@” character and is followed by a sequence identifier and optional description about the read. The second line is the actual ATCG sequence of the reads. The third line begins with a “+” character and is optionally followed by the same sequence from last line. The fourth line are encoded quality scores each base pair of the read. The fourth line always has the same length as the second line.
## Downstream analysis and peak calling
After aligning reads of DNA fragments to a reference genome, we can perform peak calling to identify binding sites of our target protein. The idea behind is that since we only select for and sequence DNA regions where our target proteins were fixed at, only regions on the reference genome where reads are enriched at can by binding site of our target protein. We can also visualize the alignment result of our reads on genome browsers like Ensemble Genome Browser, UCSC Genome Browser and IGV. The regions enriched with our reads will look like peaks on a genome browser, and this is why the method of identifying target protein binding in ChIP-Seq is called peak calling. After peaking calling, we can further utilize the reads to discover protein binding motifs or correlate with SNP data to find allele specific bindings.
## Understanding visualization of ChIP-Seq data on genome browsers
### Background noise
They tiny peaks on the genome browser are background noise which is unlikely to be binding site of our target protein. Two things may cause background noise:
1. Mapping algorithm may map reads with low quality to wrong place.
2. The antibodies used in the experiment may not be specific enough so that they select some proteins other than our target protein. Reads from those mis-selected proteins will become tiny peak on genome browser.
The general solution to background noise is to use a negative control antibody like an antibody for mouse to do the same experiment. This will give us the background of the experiment.
### Clear peaks could also be wrong
Even large peaks on genome browser may not be the actual binding site of our target protein.
1. The target protein may have more than one binding sites so one protein can have multiple peaks.
2. The sample we used for experiment may have abnormal number of copies of some genes. Those regions will look like they are enriched on reference genome. We can perform the same experiment on multiple biological replicates to solve this problem. 
## Further application of ChIP-Seq
ChIP-Seq has been modified to study RNA-protein interaction analysis. It has also been modified into DNase-seq and FAIRE-seq. The ENCODE Project stores a large amount of ChIP-Seq data with high quality.




