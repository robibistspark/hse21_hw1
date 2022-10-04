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

### Platanus trim
```bash
platanus_trim sub*
platanus_internal_trim matep*
```

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

### См. Юпитер ноутбук Analysis.ipynb в папке src.

## Бонусная часть
### Я использовал чтения pair-end длиной 500'000 и mate pairs длиной 150000. Команды далее аналогичные, так что все их не привожу.
```bash
seqtk sample -s124 oil_R1.fastq 500000 > sub3.fastq
seqtk sample -s124 oil_R2.fastq 500000 > sub4.fastq
seqtk sample -s124 oilMP_S4_L001_R1_001.fastq 150000 > matep3.fastq
seqtk sample -s124 oilMP_S4_L001_R2_001.fastq 150000 > matep4.fastq
 ```
 
 ### MultiQC
![image](https://user-images.githubusercontent.com/71763293/193901637-33f74d12-0459-4654-85ff-c7362641d4e9.png)
![image](https://user-images.githubusercontent.com/71763293/193901720-a4a3294e-3165-477c-b093-a9af1eb2b84d.png)
![image](https://user-images.githubusercontent.com/71763293/193901774-1d3d2d40-c66d-474b-aa9c-d9dbe76ba1b4.png)

### MultiQC для подрезанных чтений
![image](https://user-images.githubusercontent.com/71763293/193901973-e1c439d2-dce4-437d-89af-2c96322e670a.png)
![image](https://user-images.githubusercontent.com/71763293/193902016-371d08bd-bfaa-4f81-a6ee-57e834ba8d2e.png)
![image](https://user-images.githubusercontent.com/71763293/193902073-196cab83-01e2-47cf-a9bf-5ea242852d78.png)
