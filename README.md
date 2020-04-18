# Running ABGD (the better way!)

This tutorial will present how to run **Automated Barcode Gap Discovery** (or **ABGD**) to obtain species hypotheses (i.e. species delimitation analyses).

We will do so using a distance matrix extracted form branch lengths of a high quality tree (i.e ML or Bayes) rather than letting ABGD compute distances for us from a multiple alignment in FASTA format (Jukes Cantor by default).

There are several advantages in getting our distance matrix from a precomputed tree:

1- We can use a more complex evolutionnary model (e.g. GTR) to estimate pairwise distances more accurately

Modelling may also help reduce the impact of potential sequence error (public data can be difficult to verify but yours should be error free! triple-check it!).

2- We can use an incomplete matrix to keep maximum sequence information (i.e. when sequence vary slightly in length)

```
cd   path_to_working_directory
```
