# Differential gene expression analysis using unsupervised clustering and a random forest model
## University of California, San Francisco (UCSF)

This was an initial differential gene expression analysis that was performed as a proof-of-concept classifier for patients with and without sepsis&mdash;a life-threatening infection typically requiring admission to the intensive care unit (ICU). The gene expression data is not included in this repo as the data and a final analysis using bagged support support vector machines is currently under review for publication.

The following is an `.Rmd` file that contains a short exposition that reviews the rationale for the project, the methods used, the results obtained, and a brief discussion of these results. The code to reproduce these analyses is detailed thereafter. All required packages are listed in the `{r setup}`.  

The `.Rmd` file cannot knit without the missing data. Therefore, two `.html` files are also included in the repo with the output of the code blocks for reference and review of the output. The larger `.html` file with both the exposition and the complete project code cannot be rendered in GitHub because of its size, so must be downloaded to open. Therefore, the `Abdelghany_ML_project_write-up.html` file is included with the project write-up only for convenience, which can be opened and viewed.

## An outline of the included exposition and code:  
The below is an outline of the exposition and the `.Rmd` code that generated the analysis. The table of contents corresponds to the sections in the .Rmd file and the accompanying knit `.html` file. To jump to a section in the `.Rmd` or `.html` file, use `Ctrl-F` or `Cmd-F` and search for the titles listed below.

### Table of contents:
[Exposition outline](#integrating-host-response-and-unbiased-microbe-detection-for-precision-sepsis-diagnosis-in-critically-ill-adults)  
[Code for the analysis](#code-for-the-analysis)  
&nbsp;&nbsp;&nbsp;&nbsp;[Data preparation](#data-preparation)  
&nbsp;&nbsp;&nbsp;&nbsp;[Random forest model](#random-forest-model)  
&nbsp;&nbsp;&nbsp;&nbsp;[Start the `DESeq` workflow](#start-the-deseq-workflow)  
&nbsp;&nbsp;&nbsp;&nbsp;[DESeq analysis with outliers removed](#deseq-analysis-with-outliers-removed)  
&nbsp;&nbsp;&nbsp;&nbsp;[Group 1 (Bacteremic sepsis) vs. group 4 (no sepsis) analysis](#group-1-bacteremic-sepsis-vs-group-4-no-sepsis-analysis)  
&nbsp;&nbsp;&nbsp;&nbsp;[Generate heatmap figures](#generate-heatmap-figures)  
&nbsp;&nbsp;&nbsp;&nbsp;[Webgestalt data preparation](#webgestalt-data-preparation)  
&nbsp;&nbsp;&nbsp;&nbsp;[Table 1 code](#table-1-code)
	
### Integrating host response and unbiased microbe detection for precision sepsis diagnosis in critically ill adults
1. Introduction
2. Methods
	- Study design, clinical cohort and ethics statement
	- Metagenomic sequencing
	- Host differential expression and pathway analysis 
	- Sepsis classifier using random forest
3. Results
	- Patient enrollment and sample collection
	- Host signature of blood culture positive sepsis
	- Host transcriptional classifier for bloodstream infection-related sepsis
4. Discussion
5. References

### Code for the analysis
#### Data preparation
1. Read in the RNA seq counts and metadata and modify for analysis
2. Find genes that are in at least 30% of the samples
3. Prepare the data for entry into the `DESeq()` function

#### Random forest model
1. Prepare the data
2. Split the data into training and validation
3. Perform cross-validation of random forest model
4. Predict on the test dataset

#### Start the `DESeq` workflow
1. Create the DESeq object
	- Rewrite plotPCA function to plot PCAs 3 and 4
2. Quality assessment metrics
	- Generate the heatmap to assess for outliers
	- Perform PCA to assess for outliers
3. Perform manual PCA
	- Find the outliers in the PCA analysis
	- Remove the identified outliers

#### DESeq analysis with outliers removed
1. Model diagnostics

#### Group 1 (Bacteremic sepsis) vs. group 4 (no sepsis) analysis
1. More model diagnostics
	- MA-plot (intensity ratio by average intensity)
	- p value histogram
2. Summary of results

#### Generate heatmap figures
1. Filter for genes with a p value < 0.05
2. Get normalized count values only in the significantly DE genes
3. Perform vst transformation
4. Generate the heatmaps
	- All differentially expressed genes 
	- Top 1000 differentially expressed genes
	- Top 500 differentially expressed genes
5. Top 25 differentially expressed genes, boxplot

#### [Webgestalt](http://www.webgestalt.org/) data preparation
WebGestalt (WEB-based Gene SeT AnaLysis Toolkit) is a functional enrichment analysis web tool that was used to obtain the pathways that were differential expressed between the analyzed groups. The data was prepared for use with the web tool using R and then the analyses were performed using WebGestalt. WebGestalt was set to:  
- Organism of interest: Homo sapiens  
- Method of interest: Gene set enrichment analysis (GSEA)
- Functional database: pathway  

with advanced parameters set as default.

#### Table 1 code
Table 1 is used in all scientific literature to showcase the proportion of baseline characteristics (e.g., age, sex, etc.) between comparator groups. This helps assess the uniformity of each comparator group&mdash;a crude method for identifying possible confounders.
