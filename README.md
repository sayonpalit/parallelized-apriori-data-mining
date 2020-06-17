# parallelized-apriori-data-mining
OpenMP based multicore implementation of APriori Algorithm

## Getting Started
  * Install OpenMP(MacOS)
  ```console
      brew install omp
      xcode-select --install
  ```
## Running the Project
  ```console
      gcc -fopenmp aprioriomp.cpp
  ```
## PseudoCode
* Pass 1
    *  Generate the candidate itemsets in C1
    *  Save the frequent itemsets in L1  
* Pass k
  *  Generate the candidate itemsets in Ck from the frequent itemsets in Lk-1
      * Join Lk-1 p with Lk-1 q, as follows:
          * insert into Ck
          * select p.item1, p.item2, . . . , p.itemk-1, q.itemk-1 from Lk-1 p, Lk-1 q
             where p.item1 = q.item1, . . . p.itemk-2 = q.itemk-2, p.itemk-1 < q.itemk-1
      * Generate all (k-1) - subsets from the candidate itemsets in Ck
      * Prune all candidate itemsets from Ck where some (k-1) - subset of the candidate itemset is not in the frequent itemset Lk-1
  *  Distribute among p threads
   * Scan the transaction database to determine the support for each candidate itemset in Ck
  *  Save the frequent itemsets in Lk
  
<img src = "https://i.imgur.com/mmjLxJz.jpg">


