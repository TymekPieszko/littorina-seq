## Download instructions for *Littorina* sequence collection

Contact: t.pieszko@ucl.ac.uk

(1) Create a Python or a Conda environment:

```bash
# Python env
python

# Conda env
conda create -n litto-seq pandas requests
conda activate litto-seq
```

(2) Download the the `get_fastq_urls.py` script:

```bash
wget https://raw.githubusercontent.com/TymekPieszko/littorina-seq/main/get_fastq_urls.py
```

(3) Download FASTQ URLs for all, or a subset, of BioSample IDs. You can subset the dataset by most categorical columns (not these ones: 'Timestamp', 'Corresponder, 'Latitude', 'Longitude', 'Targeted_coverage') and request multiple categories (comma-delimited).

```bash
# Fetch URLs
# Note the flags (but not the are in lowercase
python get_fastq_urls.py \
--project_id NRS \
--species saxatilis,arcana \
--sequence_type WGS_single_individual
```

The script writes two files: `fastq_urls.tsv` and `fastq_urls.report.tsv`. The latter contains XXX.

(4) To download the actual FASTQ files, can use the `get_fastq_files.py` script. The basic idea is that every file is downloaded using `wget` - which could be done in bash loop - but the script parallelises over wget operations on the URLs (saves time!). Using X cores, it took me X h to download the whole NSN dataset (params).  

```bash
# Bash loop example
mkdir fastq
cd ./fastq

while IFS=$'\t' read -r sample_id species biosample_id url; do

    filename=$(basename "$url")

    wget -O "${sample_id}.${species}.${biosample_id}.${filename}" "$url"

done < ../fastq_urls.tsv

# Python script example - X h for whole NSN dataset
# The script will ask you XXX, allowing to spot problematic files

```
(Other) If you wish to do something custom with the XXX, you can do this easily and directly from the online Google Sheet in either R or Python:

```R
cat("Hi")
```

```Python
```