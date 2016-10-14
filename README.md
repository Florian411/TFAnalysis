# TFAnalysis
This project contains our code used to generate the conference round submissions to the _ENCODE DREAM in vivo Transcription Factor Binding Site Prediction Challenge_.

##Required software
In order to operate our code on a linux system, the following software must be installed:
- [bedtools](https://github.com/arq5x/bedtools2) (minimum version 2.25.0)
- R (minimum version 3.x.x)
- The _randomForest_ R-package
- Python (minimum version 2.7)
- [TEPIC](https://github.com/SchulzLab/TEPIC)
- [JAMM](https://github.com/mahmoudibrahim/JAMM/releases) version 1.0.7.2

Note that _TEPIC_ and _JAMM_ have additional dependencies. Links to the respective repositories are set up in this project.

##Required data
To run our scripts, the following data from Synapse must be available:
- The file *training_data.ChIPseq.tar*
- The file *training_data.DNASE_wo_bams.tar*
- The file *training_data.annotations.tar*
- All DNase bam files stored in the [DNase bams folder at synapse](https://www.synapse.org/#!Synapse:syn6176232)

In addition, the human reference genome in fasta format, version *hg19*, must be available. A corresponding [genome size file](Preprocessing/Genome_Size_File_For_JAMM.txt), required by *JAMM*,
is included in the *Preprocessing* folder. 
Position Frequency Matrices (PFMs), obtained from Jaspar, Hocomoco, and Uniprobe are already included in the _TEPIC_ repository.

##Step by step guide
In the following sections, the usage of our pipeline is described step by step.

###Data preprocessing

####Processing TF ChIP-seq label tsv data
The provided TF ChIP-seq label tsv files have to separated by TF and tissue. Further, the training data is balanced by randomly choosing
just as many samples from the unbound class as there are for the bound class. 
Use the script `Preprocessing/Split_and_Balance_ChIP-seq_TSV_files.py` to perform these tasks. 

In the Preprocessing folder, the command line is:
```
python Split_and_Balance_ChIP-seq_TSV_files.py <Path to TF ChIP-seq label tsv files> <Target directory>
```

####Identifiying DNase hypersensitive sites using JAMM
To run *JAMM* the DNase bam files have to be converted to bed files. As we do not use the replicate mode of JAMM, but call peaks in all available samples
independently, the bed files have to be distributed in individual folders. This task is carried out by the script `Preprocessing/Convert_Bam_To_Bed.py`.
This script uses the *bamToBed* tool of *bedtools*.

In the Preprocessing folder, the command line is:
```
python Convert_Bam_To_Bed.py <Path to DNase Bam files> <Target directory>
```

To start the actual peak calling, the script `Preprocessing/Call_DHS_Peaks_using_JAMM.py` can be used. Note that you have to put this script either in the *JAMM* folder
or the script `JAMM.sh` must be in your path. To run this script, use the command:

```
python Call_DHS_Peaks_using_JAMM.py <Target directory used in Convert_Bam_To_Bed.py> <Target directory for the peak calls> <Genome size file> <Number of corse to use (default 4)>
```
###Computing Transcription Factor affinities using TEPIC


###Predicting Transcription Factor binding in bins


###Preparing the data for submission


##References


##Contact
