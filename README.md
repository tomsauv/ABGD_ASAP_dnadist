# Running ABGD (the better way!)

This tutorial will present how to run **Automated Barcode Gap Discovery** (or **ABGD**) to obtain species hypotheses (i.e. species delimitation analyses)

Running ABGD and interpeting its output can be confusing at first and interpetation of its output eventually prone to errors. In my opinion there is also a better way to run it with some upstream work, which you may have ot do anyway to publish your results)

We will do so using a matrix of pairwise distances extracted from branch lengths of a high quality tree (i.e ML or Bayes) rather than letting ABGD compute Jukes Cantor distances for us from a multiple alignment in FASTA format (by default)

There are several advantages in getting our distance matrix from a pre-computed tree:

1- We can use a more complex evolutionary model (e.g. GTR) to estimate distances more accurately<br/>
Modelling may also help reduce the impact of potential sequence errors (in e.g. public data)

2- We can use an incomplete matrix to keep maximum sequence information (i.e. when sequences may vary slightly in length)

Thus, after building your FASTA alignment of curated data, the first step is to run your phylogenetic analysis with a serious tree builder (e.g. RAxML or Mr. Bayes). We will not cover this here, but we will use the resulting newick string (in a newick/tree file) as a starting point for the present tutorial. You may need to open the newick/tree file to remove unecessary lines depending on the programs you use for tree buidling, the line should start by a parenthesis '(' and finish by ');'









```
cd   path_to_working_directory
```
