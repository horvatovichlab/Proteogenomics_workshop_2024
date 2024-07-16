# QUILTS

## 1) Install python.

Installing python with a package manager such as Anaconda is recommended.

Either Anaconda or Miniconda can be installed.

Miniconda comes with less packages but requires much less storage space:

a.    Anaconda: https://docs.anaconda.com/anaconda/install/

b.    Miniconda: https://docs.anaconda.com/miniconda/
 
## 2) Download the QUILTS code.

Download the QUILTS code from the github repository and extract it to a convenient location on your system: https://github.com/ruggleslab/pyQUILTS/archive/refs/heads/master.zip
 
## 3) Download example data.

Download the reference database and the example input data here: https://drive.google.com/drive/folders/10LsvpLnrsevbSSId1IqYhosIUyQ1uvbC?usp=sharing. 

The files/folders that are needed are as follows:

a.    **pyquilts-db/GRCh38** [human genome reference db]

b.    **pyquilts-db/ensemble_human_38.100** [human proteome reference db]

c.    **chr22/germline_mutations** [folder containing chr22 germline mutations]

d.    **chr22/somatic_mutations** [folder containing chr22 somatic mutations]

e.    **chr22/junctions** [folder containing chr22 junction genes]

Note: Placing the downloaded files in a folder called data at the same level as the QUILTS source code directory should allow for using the QUILTS execution script (step 4) without any edits.

For example, use this structure:

&nbsp;&nbsp;&nbsp;&nbsp;**/home/software/pyQUILTS**  [QUILTS source code, step 2]
 
&nbsp;&nbsp;&nbsp;&nbsp;**/home/software/data/pyquilts-db/GRCh38**
 
&nbsp;&nbsp;&nbsp;&nbsp;**/home/software/data/pyquilts-db/ensembl_human_38.100**
 
&nbsp;&nbsp;&nbsp;&nbsp;**/home/software/data/chr22**
 
## 4) Create a shell script (MacOS/Linux) or batch file (Windows).

Create a shell script (MacOS/Linux) or batch file (Windows) to execute QUILTS:

Edit the file **runtest.sh** (MacOS/Linux) or **runtest.bat** (Windows) that is included with the QUILTS source code, as needed.

Use a plain text editor (TextEdit in Plain Text format on MacOS or Notepad on Windows) to edit the file.

Change the input parameters to indicate the locations of the reference genome/proteome and the files listing any mutations, junctions and/or fusion genes on your local system.

QUILTS will pull all files within a folder for input, so each input file type will need to be in a separate folder.

Please refer to the README file included with the QUILTS source code for further details on input parameters.

## 5) Create a conda environment and run QUILTS.

a.    Open Terminal in Mac or the Anaconda Shell in Windows
 
b.    Run the following commands. This will create and activate the quilts conda environment. You should see (quilts) printed before the command prompt after running the 2nd line below.

```markdown
conda create --name quilts python=3.9
```

```markdown
conda activate quilts
```

c.    Change your current directory to the location of the QUILTS source code and the shell/batch file from steps 2 and 4. For example:

```markdown
cd /home/software/pyQUILTS
```

d. Execute QUILTS.  For example:

```markdown
./runtest.sh
```
(MacOS/Linux) or

```markdown
runtest.bat  
```

(Windows)

e. If you receive this error from QUILTS:

> *ERROR: read_chr_bed didn't work - now we don't have a proteome.bed.dna file. Try recompiling read_chr_bed.c*

then you may need to fix the execute permissions for the c application (**read_chr_bed**) that is utilized by Quilts.

Please run the below line at the command prompt, in the pyQUILTS (source code) directory:



```markdown
chmod a+x read_chr_bed
```

(MacOS) or


```markdown
chmod a+x read_chr_bed_lx  
```

(Linux)

## 6) Check QUILTS output. 

QUILTS output is described in the **README** file and **OUTPUT FASTA HEADER KEY.txt**

<br><br><br><br>

# PGx

## 1) Download the PGx code.

Download the PGx code from the github repository and extract it to a convenient location on your system: 
https://github.com/FenyoLab/PGx/archive/refs/heads/master.zip

## 2) Create and activate environment.

The same conda environment that was created for QUILTS can be used for PGx. (See QUILTS step 5a-c)

Open Terminal (Mac) or Anaconda Shell (Windows). 
 
a.    Activate the conda environment (step 5c for QUILTS above)

b.    Change your current directory to the directory where the PGx source code was saved.  For example:

```markdown
cd home/software/PGx  
```

## 3) Run PGx.

Run the example pipeline for PGx by

- (1) indexing the custom proteome stored in the “oncoproteome” folder

- (2) querying the custom proteome with the example peptide in “peptides.txt” and

- (3) mapping the peptide location(s) to a bed file with genomic coordinates:

```markdown
python pgx_index.py oncoproteome  
```

```markdown
python pgx_query.py oncoproteome peptides.txt > hits.txt  
```

```markdown
python pgx_bed.py oncoproteome hits.txt > hits.bed  
```

## 4) Check PGx output.

More details can be found in the **README** file included with the PGx repository.
