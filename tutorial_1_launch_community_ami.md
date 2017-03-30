# Introduction
***
Authored by Audra Devoto

***

## Overarching Goal  
* This tutorial will teach you how to launch an AWS community server with **qiime**

## Learning Objectives
*	Understand what AWS is and how to use it
* Launch the community qiime AMI
*	Learn how to use the command line

***

# Launching a community AMI

** What is a community AMI? **
* A community AMI is a remote machine that comes pre-installed with necessary software.
* Individuals or groups can set up and maintain these AMIs, and then make them available for use.
* We will be using the Qiime AMI, which is maintained by the Qiime developers. 

** What is Qiime? (pronounced chime) **
* Qiime stands for Quantitative Insights Into Microbial Ecology. http://qiime.org/
* From the website: "QIIME is an open-source bioinformatics pipeline for performing microbiome analysis from raw DNA sequencing data. QIIME is designed to take users from raw sequencing data generated on the Illumina or other platforms through publication quality graphics and statistics. This includes demultiplexing and quality filtering, OTU picking, taxonomic assignment, and phylogenetic reconstruction, and diversity analyses and visualizations. QIIME has been applied to studies based on billions of sequences from tens of thousands of samples."

### Navigate to the Qiime AMI
* Check you are in the N. Virginia Range
[Edit security rules](https://github.com/oddaud/img/ec2-range.png)
* Navigate to the [EC2 management console](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:)

