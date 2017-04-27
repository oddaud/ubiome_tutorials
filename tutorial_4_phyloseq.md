# Introduction to analysis in R: phyloseq
***
Authored by Audra Devoto

***

## Overarching Goal  
* This tutorial will teach you how use the qiime outputs in the R package ```phyloseq```.

## Learning Objectives
*	Convert qiime output into a phyloseq object
* Analyze and visualize the output uring phyloseq commands. 

***

### 0.  Getting started
You will need to have both R and R studio installed. 

* [Here](http://shapbio.me/courses/biolB215f15/install_orient.html) is a great tutorial explaining the download process.
* I also recommend beginning with the [First Steps with R](http://shapbio.me/courses/biolB215f15/first_steps.html) tutorial.
* [Here](http://www.statmethods.net/) is a great website with plenty of R resources. 

### 1. Installing phyloseq

* Open R studio. 
* From the terminal:
```
source("http://bioconductor.org/biocLite.R")
biocLite("phyloseq")
```
* If promted, enter 'a' to update all packages. 

### 2. Analyses

* Create a new R file.
* Load necessary libraries (install if not already installed, see [Installing Packages in R Studio](https://www.youtube.com/watch?v=u1r5XTqrCTQ)
```
library(phyloseq)
library(ape)
library(GUniFrac)
library(phangorn)
library(ggplot2)
```

## Creating the phyloseq object
The phyloseq object contains information about a data set, such as the OTUs, a phylogenetic tree, abundance counts, samples, and metadata.
For more information, see the [phyloseq publication](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0061217)

* First, we must import specific output files from qiime. 
* Import the .tre file:
```
uzdir <- "/path/to/merged/otus/"
mytree <- read.tree("/path/to/merged/otus/rep_set.tre")
```
* Next, import the biom file
```
biomfile = import_biom("/path/to/merged/otus/otu_table_json.biom")
```
* Map file
```
map_file <- import_qiime_sample_data("/path/to/merged/otus/map.tsv")
```
* Now we can create the phyloseq object. View the object to see a summary of its attributes
```
physeq = merge_phyloseq(mytree, biomfile, bmsd)
....
phyloseq-class experiment-level object
otu_table()   OTU Table:         [ 18055 taxa and 14 samples ]
sample_data() Sample Data:       [ 14 samples by 8 sample variables ]
tax_table()   Taxonomy Table:    [ 18055 taxa by 7 taxonomic ranks ]
phy_tree()    Phylogenetic Tree: [ 18055 tips and 18053 internal nodes ]
```
* View the rank names
```
rank_names(clst.expt)
```
Rank1 = domain, Rank2 = phylum, etc...

* Filter out the chloroplasts and mitochondria

```
expt <- subset_taxa(expt, Rank3!="c__Chloroplast") #gone
expt <- subset_taxa(expt, Rank5!="f__mitochondria") #gone
```



