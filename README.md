# Metabolomics Analysis for Cytochrome b Inhibitor Identification

This repository contains a reproducible analysis workflow for identifying and triaging cytochrome b inhibitors during Chagas' disease drug discovery using untargeted metabolomics.

## Overview

This analysis reproduces the validation experiments from the manuscript:

**"Untargeted metabolomics for triaging of cytochrome b inhibitors during Chagas' disease drug discovery"**

by A. Kenneth MacLeod et al., specifically reproducing **Figure 3** - the validation of the cytochrome b metabolomic signature.

### Scientific Background

During phenotypic screening for Chagas' disease drugs, approximately 20% of hits act through cytochrome b, a promiscuous target. This metabolomic profiling approach enables:

- **Rapid identification** of cytochrome b inhibitors through metabolite signatures
- **Early triaging** to prioritize compounds with novel mechanisms of action
- **Resource optimization** by deprioritizing promiscuous target hits

### Key Results

The analysis demonstrates:
- Clear separation of cytochrome b inhibitors from other compound classes using PCA
- Distinction from other oxidative phosphorylation inhibitors (oligomycin A, DNP)
- High technical reproducibility with QC samples
- Specific metabolomic signature for cytochrome b inhibition

## Repository Contents

```
.
├── data_analysis.ipynb              # Main analysis notebook (enhanced with documentation)
├── Peak areas.csv                   # LC-MS peak area data (46 metabolites × 51 samples)
├── sample_info.txt                  # Sample metadata and classifications
├── Peak_areas_quantile_norm.csv     # Output: Normalized data
├── PCA.svg                          # Output: PCA scores plot (Figure 3)
├── Loading.svg                      # Output: PCA loadings plot
└── README.md                        # This file
```

## Requirements

### Input Files

1. **Peak areas.csv**: LC-MS peak area measurements for metabolites across all samples
2. **sample_info.txt**: Tab-separated file with sample classifications:
   - `NAME`: Original LC-MS filename
   - `rename`: Simplified sample identifier
   - `Color`: Color code for visualization
   - `CLASS`: Sample classification (Cytb, Non-cytb, Other OxPhos, QC, SB)

### Dependencies


## Reproducing the Analysis

### Option 1: Using Docker (Recommended)

We provide a Docker-based Jupyter Lab environment with all dependencies pre-installed.

#### 1. Clone the repository

```bash
git clone <repository-url>
cd metabolomic_kennet
```

#### 2. Run the Docker container

**Example command** (adjust ports and volume paths according to your system):

```bash
docker run -p 8890:8888 -v /path/to/metabolomic_kennet:/app --rm mtinti/biojupyter_debian
```

**Parameters**:
- `-p 8890:8888`: Map container's Jupyter Lab port 8888 to host port 8890
- `-v /path/to/metabolomic_kennet:/app`: Mount your local directory to `/app` in container
  - **Windows**: `-v F:/metabolomic_kennet:/app`
  - **Mac/Linux**: `-v /Users/username/metabolomic_kennet:/app`
- `--rm`: Automatically remove container when stopped
- `mtinti/biojupyter_debian`: Docker image with bioinformatics tools

**Docker Image Details**:

The `biojupyter_debian` image contains Jupyter Lab and common bioinformatics packages. For more information about the Dockerfile and available tools, see:

👉 **https://github.com/mtinti/docker_data_analysis/**

#### 3. Access Jupyter Lab

After running the docker command, you'll see output like:

```
[C 2024-xx-xx xx:xx:xx.xxx ServerApp]

    To access the server, open this file in a browser:
        file:///...
    Or copy and paste one of these URLs:
        http://localhost:8888/lab?token=...
```

Open your browser and navigate to:
```
http://localhost:8890/lab?token=<your-token>
```

(Note: Use port 8890 if you mapped it as in the example, or whatever port you chose)

#### 4. Open and run the notebook

1. Navigate to the `/app` directory in Jupyter Lab
2. Open `data_analysis.ipynb`
3. Run all cells: **Run → Run All Cells**

## Analysis Workflow

The notebook performs the following steps:

### 0. Set Random Seeds
- Ensures reproducibility of all stochastic processes

### 1-2. Data Loading
- Import LC-MS peak area data (46 metabolites × 51 samples)
- Create unique metabolite identifiers

### 3-4. Data Preprocessing
- Remove problematic features
- Extract peak area matrix

### 5. Log Transformation
- Apply log10 transformation to stabilize variance

### 6. Quantile Normalization
- Remove technical variation between samples
- Make distributions identical across samples

### 7. Normalization Visualization
- Side-by-side comparison of data before/after normalization

### 8. Export Data
- Save normalized peak areas to CSV

### 9-10. Sample Metadata
- Load sample classifications
- Create annotation dictionaries

### 11. Feature Summary
- Display metabolite identifiers

### 12. Dimensionality Reduction Dashboard
- PCA, t-SNE, and UMAP visualizations

### 13. PCA Analysis (Figure 3)
- Reproduce manuscript Figure 3
- Demonstrate separation of compound classes

### 14. PCA Loadings
- Identify key discriminative metabolites

### 15. Summary
- Key findings and conclusions

## Expected Outputs

After running the analysis, you will generate:

1. **Peak_areas_quantile_norm.csv**: Quantile-normalized metabolite data
2. **PCA.svg**: Principal component analysis scores plot showing sample clustering
3. **Loading.svg**: PCA loading plot showing metabolite contributions
