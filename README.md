# hse22_hw1

### Creating symbolic links

```bash
mgstepanyants@bioinflab-2:~$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
mgstepanyants@bioinflab-2:~$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
mgstepanyants@bioinflab-2:~$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
mgstepanyants@bioinflab-2:~$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```

### Extracting data from source files

```bash
mgstepanyants@bioinflab-2:~$ seqtk sample -s124 oil_R1.fastq 5000000 > sub1.fastq
mgstepanyants@bioinflab-2:~$ seqtk sample -s124 oil_R2.fastq 5000000 > sub2.fastq
mgstepanyants@bioinflab-2:~$ seqtk sample -s124 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq
mgstepanyants@bioinflab-2:~$ seqtk sample -s124 oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq
```
