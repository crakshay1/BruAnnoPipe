# BruAnnoPipe

**BruAnnoPipe** is an automated bioinformatics pipeline designed for the comprehensive annotation of genomic sequences. It integrates local command-line tools with web-based prediction and validation services to identify transposable elements, predict gene structures, and validate protein sequences.  `BruAnno.ipynb` is a notebook designed to be used as if you were in a laboratory.   

⚠️ Special thanks to **Georgy ZAOUK** who modified the pipeline to automatically generate the .gff3 files.

---

## 🔍 Features

* **Interactive GUI**: Easy-to-use selection for species identifiers and input files via `easygui`.
* **Transposable Element (TE) Analysis**:
    * Local alignment against `TrepDB` using local BLASTn.
    * Local alignment against `URGIDB` using local BLASTn.
    * Automated web-submission to **Censor** (Giri Institute) for soft-masking and TE detection.
* **Gene & Protein Prediction**:
    * **Augustus**: Local prediction executed on both raw and masked sequences.
    * **FGENESH**: Automated web-based prediction (optimized for plant genomes) executed on both raw and masked sequences.
* **Automated Validation**:
    * **BLASTn**: Validation of mRNA against the TSA database.
    * **BLASTp**: Protein validation against NR and SwissProt databases.
    * **BLASTx**: Final check of the full sequence against SwissProt to catch missed coding regions.
* **Prediction Visualization**:  .gff3 files are generated for Artemis visualization.
* **Anonymity & Access**: Integrates with the **Tor** network to manage web requests.

---

## 📖 Prerequisites

### System Requirements
* **Linux/Unix** environment (recommended), if you don't have Linux, WSL can be used.
* **Mozilla Firefox** and **Geckodriver** (for Selenium automation).
* **Tor Service** (installed and configurable via `sudo service tor`).

### External Tools
The following must be installed and available in your system `$PATH`:
* **EMBOSS** (makeblastdb, blastn, blastp, blastx).
* **Augustus**.
* **Artemis**.

### Python Dependencies
```bash
pip install -r requirements.txt
```

---

## 📁 Setup & Directory Structure

To function correctly, the script requires a specific environment setup and will generate organized results as follows:

### 1. Pre-run Requirements
Every folder in this git has to be downloaded, except for Results.

### 2. Output Organization
The script automatically creates a `Results/` directory. Within that folder, a sub-directory is created for each run using the format `[Species]_[Filename]`.

### 3. Folder Contents
Inside each result folder, you will find:
* **`ARTEMIS/`**: Contains the images obtained via Artemis, and the .gff3 files of the predictions.
* **`TE/`**: Contains the local BLAST outputs against TrepDB and URGIDB + the `result.pdf` masking report from Censor + Dotplots and .fasta files of the TEs found by Censor.
* **`pred_by_augustus/`**: Includes the full Augustus text output, as well as sub-folders for predicted proteins and mRNA in `.fasta` format.
* **`pred_by_fgenesh/`**: (If selected) Contains the parsed PDF results and corresponding `.fasta` predictions.
* **`blastp_results/`**: Organized by database (`nr/` and `swiss/`), containing the alignment reports for predicted proteins.
* **`blastn_results/`**: Contains the validation reports for predicted mRNA against the TSA database.
* **`blastx_result/`**: Contains a final validation check of the original sequence against protein databases.
