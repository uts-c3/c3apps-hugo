+++
image = "img/portfolio/mol.jpeg"
showonlyimage = false
date = "2017-06-14T08:44:32+05:30"
title = "BASTA"
draft = false
weight = 1
+++
BASTA is a customisable basic sequence taxonomy annotation tool that assigns taxonomies to sequences or groups of sequences based on 7 level NCBI taxonomies and a user defined sequence comparison file. Additionally, BASTA can be used to filter fasta files based on taxonomic classification and visualise results in KRONA plots.

<!--more-->


# BASTA
BAsic Sequence Taxonomy Annotation

As the name implies, BASTA assigns taxonomies to sequences or groups of sequences based on the Last Common Ancestor (LCA) of a number of best hits. BASTA can be customised to run on any kind of tabular output (default = blast -outfmt 6) as long as the input file provides values for e-value, percent identity and alignment length. Taxonomies are inferred from NCBI taxonomies based on a 7 level taxonomy. 


# Download and documentation

The latest [release candidate](https://github.com/timkahlke/BASTA/releases) as well as the [wiki](https://github.com/timkahlke/BASTA/wiki) with detailed installation and usage instructions can be found on the official [BASTA github repository page](https://github.com/timkahlke/BASTA).

# Requirements

BASTA uses levelDB (https://github.com/google/leveldb) and the python wrapper Plyvel as a local database to hold NCBI mappings and taxonomies. Additionally, BASTA requires the non-standrad python packages

* gzip
* hashlib

To generate Krona plots from BASTA taxonomies please also install Krona (https://github.com/marbl/Krona/wiki/KronaTools).

For a detailed installation guide please visit https://github.com/timkahlke/BASTA/wiki

# Quick start

## Inital Setup 

```
# set up NCBI taxonomy database
./bin/basta taxonomy

# download and set up genbank and uniprot mappings 
# NOTE: this might not be needed for you. See Wiki for details
./bin/basta download gb
./bin/basta download prot
```

## Running BASTA

```
# Infer one LCA for each query sequence of blast against uniprot
./bin/basta sequence BLAST_OUTPUT_FILE BASTA_OUTPUT_FILE prot

# Infer one LCA for the complete blast output file
./bin/basta single BLAST_OUTPUT_FILE prot

# Infer one LCA for each blast output file in a given directory
./bin/basta multiple BLAST_OUTPUT_DIRECTORY BASTA_OUTPUT_FILE prot
```

# Last Common Ancestor algorithm
BASTA supports two algorithms: all and majority

## All
If this method is used BASTA reads a given number of best hits for each query sequence and returns the LCA of all sequences (unknown taxonomic levels in database hits are ignored).

Additionally, if the *lazy* option is used, the user defined minimum number *n* of hits that is needed to estimate taxonomies will be discarded for sequences with a total hit number <n. Set values for e-value, identity, alignment length etc still apply.


## Majority
In this case BASTA determines the LCA based on the LCA of the majority of given best hits. Example: if maximum best hit number is set to 5 and 3 best hits are Bacteria and 2 best hits are Archaea, BASTA returns Bacteria as LCA.



# Additional scripts

## basta2krona.py

This creates a krona plot (html file) that can be opened in your browser from a basta annotation output file.

```
./scripts/basta2krona BASTA_OUTPUT_FILE KRONA_HTML_FILE
```


## filter_fasta.py

This script can be used to filter a given fasta file based on BASTA annotations.

```
./scripts/filter_fasta.py [options] FASTA_FILE FILTERED_OUTPUT_FILE NAME_OF_TAXON BASTA_FILE
```

