# blast

```txt
# Background 

I received trinity outputs for WZ, WW and WY individuals from Ben.
Working in the directory,
```bash
/scratch/premacht/trace_unique_genes
```

# blast fasta files to reference genome

 In the parent directory (trace_unique_genes) Run following to create reference genome

``` bash
mkdir reference_genome

# Download reference genome, unzip it and move to the reference genome folder
wget http://ftp.xenbase.org/pub/Genomics/JGI/Xenla9.2/XENLA_9.2_genome.fa.gz
gunzip XENLA_9.2_genome.fa.gz
mv XENLA_9.2_genome.fa* ./reference_genome
```

Create the nucleotide database based on `ref.fa` 

Run following in the directory reference_genome/


```bash
module load gcc/7.3.0 blast+/2.9.0

makeblastdb -in XENLA_9.2_genome.fa -title reference -dbtype nucl -out XENLA_9.2_genome.fa

```


for i in *.fasta; do blastn -db nt -query ${i} -outfmt 6 > ${i%%_trinity_output.Trinity.fasta}_fmt6_out -remote; done










Then in the directory with Trinity files






#!/bin/sh
#SBATCH --job-name=bwa_505
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --time=24:00:00
#SBATCH --mem=64gb
#SBATCH --output=bwa505.%J.out
#SBATCH --error=bwa505.%J.err
#SBATCH --account=def-ben

#SBATCH --mail-user=premacht@mcmaster.ca
#SBATCH --mail-type=BEGIN
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL
#SBATCH --mail-type=REQUEUE
#SBATCH --mail-type=ALL


module load gcc/7.3.0 blast+/2.9.0

for i in *.fasta; do blastn -db nt -query ${i} -outfmt 6 > ${i%%_trinity_output.Trinity.fasta}_fmt6_out -remote; done




Installed ncbi-blast-2.11.0+.dmg from https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ in my Mac

After installation, blast can be found in /usr/local/ncbi/blast/bin




type 
chmod +x blastn 

to enable blastn


to use local databases 
Followed instructions from
https://www.blaststation.com/intl/members/en/howtoblastmac.html

```
