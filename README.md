# hse22_hw1

### Creating symbolic links

```bash
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```

### Extracting data from source files

```bash
seqtk sample -s124 oil_R1.fastq 5000000 > sub1.fastq
seqtk sample -s124 oil_R2.fastq 5000000 > sub2.fastq
seqtk sample -s124 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq
seqtk sample -s124 oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq
```

### FastQC (to the special folder)
```bash
ls sub* matep* | xargs -tI{} fastqc -o fastqc {}
```

### MultiQC (to the special folder)
```bash
multiqc -o multiqc fastqc
```

### MultiQC report
![image](https://user-images.githubusercontent.com/71763293/193472430-704bd9ac-a932-4819-b388-8dd5cd0fb620.png)
![image](https://user-images.githubusercontent.com/71763293/193472515-662bfe96-7643-4870-85f6-dc14ae100ecc.png)
![image](https://user-images.githubusercontent.com/71763293/193472527-39b09e54-fd99-43a4-9a3a-3be99f6077d7.png)

### Trimmed FastQC
```bash
mkdir fastqc_trimmed
ls sub* matep*| xargs -tI{} fastqc -o fastqc_trimmed {}
```

### Trimmed MultiQC
```bash
mkdir multiqc_trimmed
multiqc -o multiqc_trimmed fastqc_trimmed
```

### Trimmed MultiQC report
![image](https://user-images.githubusercontent.com/71763293/193473296-bc451ef7-c9a8-47c4-9fce-45c26f0509cc.png)
![image](https://user-images.githubusercontent.com/71763293/193473306-8775a984-578f-4ef3-a642-3244112e6c6d.png)
![image](https://user-images.githubusercontent.com/71763293/193473314-708ccdd2-9d86-424b-97fd-7e52333bf9e0.png)

### Platanus assemble
```bash
time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
```

### Platanus scaffolds
```bash
time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> scaffold.log
```

### Platanus gap closing
```bash
time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> gapclose.log
```
