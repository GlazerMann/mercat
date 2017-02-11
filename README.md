Mercat: Python code for Parallel k-mer counting
================================================

![GitHub Logo](mercat.jpg)

  
Installing MerCat: 
 - Available in BioConda: Enable BioConda repo and run `conda install mercat`  
 
Usage:
-----
 * -i I        path-to-input-file
 * -f F        path-to-folder-containing-input-files
 * -k K        kmer length
 * -n N        no of cores [default = all]
 * -c C        minimum kmer count [default = 10]
 * -pro        run mercat on protein input file specified as .faa 
 * -q          tell mercat that input file provided are raw nucleotide reads as [.fq, .fastq]
 * -p          run prodigal on nucleotide assembled contigs. Must be one of ['.fa', '.fna', '.ffn', '.fasta']
 * -t [T]      Trimmomatic options
 * -h, --help  show this help message

By default mercat assumes that inputs provided is one of ['.fa', '.fna', '.ffn', '.fasta']
> Example: To compute all 3-mers:
            mercat -i test.fa -k 3 -n 8 -c 10 -p
            
- Runs prodigal on test.fa, then runs mercat on the resulting protein file.            
- Results are stored in input-file-name.csv and input-file-name_summary.csv  
   (test.csv and test_summary.csv in the above example)  
- test.csv contains kmer count for kmers in individual sequences  
- test_summary.csv contains kmer count for all unique kmers across all sequences in the sample test.fa

  
Other usage examples:
---------------------

* `mercat -i test.fq -k 3 -n 8 -c 10 -q`  
   Runs mercat on raw nucleotide read (.fq or .fastq) 
   
*  `mercat -i test.fq -k 3 -n 8 -c 10 -q -t`  
   Runs trimmomatic on raw nucleotide reads (.fq or .fastq), then runs mercat on the trimmed nucleotides
    
*  `mercat -i test.fq -k 3 -n 8 -c 10 -q -t 20`  
   Same as above but can provide the quality option to trimmomatic
   
*  `mercat -i test.fq -k 3 -n 8 -c 10 -q -t 20 -p`
   Run trimmomatic on raw nucleotide reads, then run prodigal on the trimmed read to produce a protein file which is then processed by mercat
      
*  `mercat -i test.fna -k 3 -n 8 -c 10`  
   Run mercat on nucleotide input - one of ['.fa', '.fna', '.ffn', '.fasta']
    
*   `mercat -i test.fna -k 3 -n 8 -c 10 -p`  
    Run prodigal on nucleotide input, generate a .faa protein file and run mercat on it
    
*   `mercat -i test.fna -k 3 -n 8 -c 10 -pro`  
    Run mercat on a protein input (.faa)

* All the above examples can also be used with  `-f input-folder` instead of `-i input-file` option
  -  Example:  `mercat  -f /path/to/input-folder -k 3 -n 8 -c 10` --- Runs mercat on all inputs in the folder