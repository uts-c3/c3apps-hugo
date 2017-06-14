+++
image = "img/portfolio/mol.jpeg"
showonlyimage = false
date = "2017-06-14T08:44:32+05:30"
title = "panbiom"
draft = false
weight = 1
+++

Panbiom is a tool to estimate the core operational taxonomic units (OTUs) of a user-defined set of samples and replicates.


<!--more-->

---

# Download and documentation

The source code is freely available on the official [panbiom github repository page](https://github.com/timkahlke/panbiom). Documentation and use cases can be found on the projects [wikipage](https://github.com/timkahlke/panbiom/wiki).

---


# Usage
panbiom.py [options] BIOM_FILE OUTPUT_FILE

# Options
-t, --treatments 
List of samples (treatments) that should be considered for analysis

-m, --abundance_minimum: Minimum abundance (between 0-1) an OTU must have to be considered present (default: 0.0)

-p, --abundance_parameter: Defines whether the abundance threshold should be based on the complete data set (c) or on the defined treatments (t) (default: t)

-r, --replicate_threshold: If groups/replicates are defined in the treatments file (second column) the given abundance threshold has to be met in at least given number of replicates.
# ampli-tool
Collection of helper scripts for amplicon sequence analysis, e.g. as outlined in the workflow in the docs directory.

Note: to get a full list of possible parameters and a short description of each tool just call the script without parameters.

---
