# Running ABGD (the better way!)

This tutorial will present how to run Automated Barcode Gap Discovery (or ABGD) to obtain species hypotheses (i.e. species delimitation analyses).

We will do so using a distance matrix extracted form branch lengths of a high quality tree (i.e ML or Bayes) rather than letting ABGD compute distances for us (by default Jukes Cantor) from a multiple alignment in FASTA format.

There are several advantages in getting our distance matrix from a precomputed tree:

**1- We can use a more complex evolutionnary model (e.g. GTR) than used by default in ABGD - this may estimate distance between taxa more accurately**

**2- This allows us to use an imcomplete matrix where sequence might vary slightly in length. By doing so we keep maximum sequence information rather than cropping all sequences to the shortest one to produce a 'complete' matrix**

**3- Compensate for potential sequence barcode error from public data that we may not ber able to check. Modelling may help reduce impact of erroneous bases and their potential impact on species boundaries**

```
cd   path_to_working_directory
```
