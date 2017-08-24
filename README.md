# INTRODUCTION

This series of scripts processes HyRAD data acquired in the Fuller Lab at the Cornell Lab of Ornithology. It  was cobbled together from existing resources by Nick Mason. Thanks go to Mike Harvey and Ethan Linck for posting their pipelines and providing insight at various points along the way.

The pipeline here is intended for systems that do not have a reference genome. I have generated an alternative pipeline that makes use of a reference genome (link here eventually). 

# LISCENCE

# CITATION

# DEPENDENCIES

# USAGE

## 1. Cleaning raw sequences

When I've submitted HyRAD libraries to the Cornell BRC, they come back demultiplexed, so we do not deal with demultiplexing here. They may have already done some filtering as well as part of their demultiplexing pipeline, but we will go ahead and perform filtering anyways.

This step will assess sequence quality and then perform quality control on raw sequences, including removal of poor-quality reads and adapter contamination. There are many programs that can help with this step of the process. Here, I use trimmomatic in a shell script to process through each pair of paired-end files.

I have created an R script (trimmomaticShell.R) that should help generate the shell script if provided with an input directory and an output directory. Users will have to change the path to the program and adapter files if it is not PE data or if it is run outside of the CBSU Cornell computing cluster.

Here is an example for how I've run Trimmomatic on files received from Cornell BRC.


```
java -jar /programs/trimmomatic/trimmomatic-0.36.jar PE -threads 8 -phred33 /workdir/nam232/Ealp_phylogeo/0_rawsequences/8479_3270_55273_B869D_Lark_001_EA088_TGATAGGC_ACCGACAA_R1.fastq.gz /workdir/nam232/Ealp_phylogeo/0_rawsequences/8479_3270_55273_B869D_Lark_001_EA088_TGATAGGC_ACCGACAA_R2.fastq.gz /workdir/nam232/Ealp_phylogeo/1_cleaned/EA088_1P.fq.gz /workdir/nam232/Ealp_phylogeo/1_cleaned/EA088_1U.fq.gz /workdir/nam232/Ealp_phylogeo/1_cleaned/EA088_2P.fq.gz /workdir/nam232/Ealp_phylogeo/1_cleaned/EA088_2U.fq.gz ILLUMINACLIP:/programs/trimmomatic/adapters/TruSeq3-PE-2.fa:2:30:10 SLIDINGWINDOW:4:15 LEADING:30 TRAILING:30 MINLEN:40
```