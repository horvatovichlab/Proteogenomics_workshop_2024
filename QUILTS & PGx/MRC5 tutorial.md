# Use QUILTS on the MRC5 dataset

## 1) Prepare the reference genome.

a.    Follow the instructions of the **readme** file located in the **prepare_genome** directory.

b.    You will first need to download the **Homo_sapiens.GRCh38.dna.chromosome.*.fa.gz** files following the instructions in the **readme** file. Alternatively, download the necessary files from here: https://drive.google.com/drive/folders/1xctlIkmS4B4oQ6E1AvPpC-WNPrhR3f3C 

c.    Place the downloaded files in the prepare_genome directory.

d.    Run the prepare_genome.py script, for example:

```markdown
python prepare_genome.py .
```

e.    Move the new files (***.cmp1**) to the **genome** subdirectory of the directory in which you would like to store all MRC5 data, for example: 

**data/mrc5/genome**

## 2) Prepare the reference proteome.

a.    Follow the instructions of the **readme** file located in the **prepare_proteome/prepare_ensembl** directory.

b.    You will first need to download the info files from Biomart and the reference proteome FASTA file (**mart_export.txt** and **Homo_sapiens.GRCh38.pep.all.fa**). Follow the instructions in the **readme** file. Unzip the fasta file if necessary. Alternatively, download these two files from here: https://drive.google.com/drive/folders/1FKy--oSHA1wachs9YmJP2vwxbqfCuOBl 

c.    Place the downloaded files in the **prepare_proteome/prepare_ensembl** directory.

d.    Run the **prepare_ensembl.py** script, for example:

```markdown
python prepare_ensembl.py mart_export.txt Homo_sapiens.GRCh38.pep.all.fa
```

e.    Rename the generated fasta file to proteome.fasta if it is not renamed already.

f.    Move the new files (**proteome.fasta**, **transcriptome.bed**, **proteome.bed**, **proteome-genes.txt**, **proteome-descriptions.txt**) to the proteome subdirectory of your MRC5 data directory, for example: 

**data/mrc5/proteome**

## 3) Download the MRC5 input files.

a.    Download the following files from this drive folder https://drive.google.com/drive/folders/16MvNuco8oSimGw5p9T8HOteA8CcuWY5G 

-	**MRC5_gatk_filtered.vcf.gz** and **MRC5_gatk_filtered.vcf.gz.tbi** (the new location should be for example: **data/mrc5/vcf**). Unzip the file before running QUILTS.

-	**MRC5.filtered.SJ.out.tabs.zip** (the new location should be for example: **data/mrc5/junction**). Unzip the file before running QUILTS.

## 4) Run QUILTS.

We do not have separate VCF files for somatic and germline mutations here, so you should treat the VCF file as if it were to contain somatic mutations only.

Example of the code:

```markdown
python quilts.py --output_dir ./results --genome ./data/mrc5/genome --proteome ./data/mrc5/proteome --somatic ./data/mrc5/vcf --junction ./data/mrc5/junction --junction_file_type star --threshB 1 --threshD 1 --threshN 1
```

## 5) Check QUILTS output.

The results are located in a **results_(date).(time)** directory.

QUILTS has generated the variant and reference proteome (**reference_proteome.fasta** and **variant_proteome.fasta**), which then can be used for database search in proteomics.

