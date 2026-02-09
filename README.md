### Ex-vivo-mucus-analysis

This repository provides an R-based method for the rapid generation of “Normalised penetrability (area under the curve - AUC)” and “Thickness (µm)” values for mucus quantified using the bead/penetrability ex vivo approach to quantifying mucus barrier properties in z-stack images of intestinal biopsies acquired by confocal microscopy.

### Prerequisites & Assumptions

Sample Geometry: This method assumes your sample is flat when imaged. If it is not, you should sub-sample tissue and beads data from flat areas within the original z-stack.

Bead Dynamics: The method assumes most beads settle at the surface of the mucus. Excess beads in the buffer will result in inaccurate data and should be cropped out prior to data extraction.

Image data extraction: This method is based on analysis of tissue and bead z-position values that have been extracted from confocal z-stack images. Such data can be extracted using image analysis software such as ImageJ, Imaris, etc.

User Knowledge: Prior knowledge of R is useful but not essential.

### Software Requirements

You will need to download and install the following:

R for Windows 
Rtools 
R Studio 

### Required R Packages

Open R Studio and run the following command in the console to install dependencies:

install.packages(c("ggplot2", "MESS", "dplyr", "ggpubr", "tidyr", "patchwork"))

### Data Preparation

Before running the script, you must prepare a combined data file:

Extract z-position data for tissue and beads (e.g., in Imaris).

Create an table file (e.g. Excel) with the following structure:

Row 1: Simple sample names (no spaces or special characters).

Row 2: Tissue z-position (NOTE - only one value per sample).

Row 3-n: Bead z-positions (can be any number of values).

Columns: Each column should represent one sample only.

Save as: A tab-delimited text file named combined_data.txt.

### Usage Procedure

Create a new project and working directory in R Studio (File > New Project).

Move your combined_data.txt and the Preprocessing and analysis v5_1.Rmd script into this directory.

Open the .Rmd file in R Studio.

In the "Run" dropdown menu, select "Run All".

### Outputs

The script generates the following files in your directory:

combined_results.txt: All AUC and Thickness values for each sample.

<sample_name>.png: Visualisation of the distribution and penetrability curves (useful for Quality Control).

<sample_name>_pen_data.txt: Normalized z and frequency values.

Note on Thickness: Mucus thickness is defined as the mode (maximum peak) of the bead distribution curve. With a default bin-width of 5µm, values will be divisible by 5. You can adjust the binwidth in the "Penetrability function" code chunk for more granular data.