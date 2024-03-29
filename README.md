# 'Prepping' a distance matrix for ABGD/ASAP

There are several advantages in using a distance matrix from a pre-computed tree for species delimitation with ABGD/ASAP :<br/>

1- We can use a complex evolutionary model (e.g. GTR) to better estimate distances between sequences.<br/>
Such modelling may also help reduce the impact of potential sequence errors on delimitation (e.g. nucleotide errors from public data or in your own data...).

2- We can use an incomplete DNA alignment to keep maximum sequence information in which some sequences may vary drastically in length.

# Get your newick string

After building your FASTA alignment from carefully curated data, the first step is to run your phylogenetic analysis with a serious tree builder (e.g. RAxML). The resulting newick string (```.nwk``` or ```.tre``` file) may need to be opened in a simple text editor to remove unecessary lines depending on the programs you used for tree building - here, for the R snippets below to work, we want the line to start by a parenthesis ```(``` and finish by ```);``` as in the example below. This is 'barebone' newick format.

```
((((((((taxon1:0.22177,(((taxon6:0.596697,taxon8:0.232903):0.077822,........,taxon65:0.0065);
```
# Make it a PHYLIP dnadist

We now import our newick string in R to extract the tree branch lengths and produce a distance matrix that ABGD/ASAP can read (phylip format). We will need package ```ape``` and ```phangorn``` to do so the easy way. Thus you have to download these packages from CRAN and install them prior.<br/>
 
```
require(ape)
require(phangorn)
my_tree <- read.tree("RAxML.tre")                                           # Import the tree
my_matrix <- cophenetic.phylo(my_tree)                                      # Extract branch lengths
writeDist(my_matrix, "RAxML_dnadist_for_ABGD_ASAP.txt", format ="phylip")   # Export distance matrix
```

If you open ```RAxML_dnadist_for_ABGD_ASAP.txt``` with a simple text editor, values will be space-delimited on each row.<br/>
In the example below, there are 80 taxa and each taxon name is followed by values representing pairwise distances between taxa. Cells with 0s are on the diagonal (e.g. taxon1 vs. taxon1 is logically 0!).<br/>

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
The distance file is now ready to be used on the [ABGD](https://bioinfo.mnhn.fr/abi/public/abgd/abgdweb.html) or [ASAP](https://bioinfo.mnhn.fr/abi/public/asap/asapweb.html) webservers with appropriate parameters.<br/>

PS: It's always good practice to avoid special characters in the fasta titles of sequences (i.e. taxa names) to insure data portability across different tools. Use underscore or similar instead of special characters or blank spaces. If you encounter issues with running ABGD/ASAP, a first check may be to inspect your taxa names. 
