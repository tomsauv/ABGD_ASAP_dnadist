# Running ABGD (the better way!)

This tutorial will present how to run **Automated Barcode Gap Discovery** (or **ABGD**) to obtain species hypotheses (i.e. species delimitation analyses)

Running ABGD can be confusing at first and interpetating its output eventually prone to errors. In my opinion there is also a better way to run it with some upstream work, which you will have to do anyway to publish your results

We will do so using a matrix of pairwise distances extracted from branch lengths of a high quality tree (i.e ML or Bayes) rather than letting ABGD compute Jukes Cantor distances for us from a multiple alignment in FASTA format (by default)

There are several advantages in getting our distance matrix from a pre-computed tree:

1- We can use a more complex evolutionary model (e.g. GTR) to estimate distances more accurately<br/>
Modelling may also help reduce the impact of potential sequence errors (e.g. from public data) on delimitation

2- We can use an incomplete matrix to keep maximum sequence information (i.e. when sequences may vary slightly in length)

Thus, after building your FASTA alignment from carefully curated data, the first step is to run your phylogenetic analysis with a serious tree builder (e.g. RAxML or Mr. Bayes). We will not cover this here, but we will use the resulting newick string (in a newick/tree file) as a starting point for the present tutorial. You may need to open the newick/tree file with a simple text editor to remove unecessary lines depending on the programs you used for tree buidling - the line should start by a parenthesis ```(``` and finish by ```);``` as below:

```
((((((((taxon1:0.22177,(((taxon6:0.596697,taxon8:0.232903):0.077822,........,taxon65:0.0065);
```

We will then import it in R to extract branch lengths and produce a distance matrix that ABGD can read (phylip format)<br/>
 
```
require(ape)
require(phangorn)
my_tree <- read.tree(x=read.tree("RAxML.tre")                       # Import tree
my_matrix <- cophenetic.phylo(my_tree)                              # Extract branch lengths
writeDist(my_matrix, "RAxML_dist_for_ABGD.txt", format ="phylip")   # Export distance matrix
```

If you open ```RAxML_dist_for_ABGD.txt``` with a simple text editor values will be space delimited ad as below:
In this example, there were 80 taxa in the tree, values represent pairwise distances and 0s are on the diagonal (e.g. taxon1 vs taxon1)

```
80 
taxon1 0 2.099816 1.736022 2.162966 ...
taxon2 2.099816 0 0.8296 1.412188 ...
taxon3 1.736022 0.8296 0 1.048394 ...
taxon3 2.162966 1.412188 1.048394 0 ...
...
...
taxon80 0.761922 2.418198 2.054404 2.481348 ... 0
```




