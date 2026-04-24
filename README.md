# covid19-and-related-factors
Project Title: An Ecological Study on the Mortality Impact of COVID-19 Pandemic According to Country Development Status and Pandemic Years
Authors: Murat Razi, Manuel Graña
Date: March 28, 2026
Affiliation: Computational Intelligence Group (UPV/EHU)

**The all code and materials can be downloaded via the zenodo link below.
**
https://zenodo.org/records/19404440

1. OVERVIEW
This project is a comprehensive MATLAB study analyzing 20 key macroscopic variables affecting COVID-19 mortality rates across 174 countries. To ensure the robustness of the findings, the study utilizes two distinct mortality metrics:
1. Reported Deaths: Official deaths per million people (averages.mat).
2. Excess Mortality: Estimated cumulative excess deaths per 100,000 people based on The Economist’s central estimate model (dataexcess.mat).
2. DIRECTORY STRUCTURE
The project is organized into 10 main folders, each representing a specific experimental setup:
* Analysis 1: Global Analysis. Covers the full pandemic timeframe. Both Model A (Main Effects) and Model B(Interactions) are executed here.
* Analysis 2 – 7: Economic Stratification Analyses (Developed, Developing, Least Developed Countries, etc.).
* Analysis 8 – 10: Pandemic Phase Analyses (Temporal analysis for Year 1, Year 2, and Year 3, respectively).
3. DATA WORKFLOW & EFFICIENCY (IMPORTANT)
The project structure is designed to minimize computational time by reusing processed data files (.mat) instead of re-reading raw CSV files for every analysis.
A. Global & Economic Analysis (Analysis 1 - 7)
1. Generate in Analysis 1: The foundation is established in Analysis 1. You must run datapreparation.mlx and datapreparationexcess.mlx here first. This generates the master averages.mat and dataexcess.mat files.
2. Copy to Analysis 2-7: To avoid redundant data processing, manually copy these two generated .mat files from Analysis 1 and paste them into the folders for Analysis 2 through Analysis 7.
3. Sub-Analysis Filtering: Even though the master data is loaded, it must be filtered for the specific economic group. Inside the main script (Analysis_X_A.mlx) for each folder, a specific datapreparationX.mlx script is called automatically. This script processes the loaded averages.mat or dataexcess.mat to extract only the relevant countries for that specific sub-analysis (e.g., Developed Countries only).
B. Temporal Phase Analysis (Analysis 8 - 10)
For your convenience, Analysis 8, 9, and 10 already contain pre-calculated averages.mat and dataexcess.matfiles specific to their respective timeframes.
* No Action Required: You generally do not need to run the data preparation scripts in these folders. You can proceed directly to running the analysis scripts (Analysis_X_A.mlx).
* Regeneration (Optional): If you need to re-process the data from scratch, you can still run the phase-specific datapreparation[X].mlx and datapreparationexcess.mlx scripts located within each folder.
4. SELECTING ANALYSIS MODE (SWITCHING DATASETS)
The analysis scripts (Analysis_X_A.mlx) default to analyzing Reported Deaths. To switch to Excess Mortality analysis, modify the load commands at the beginning of the script as follows:
* To Analyze Excess Mortality:
Matlab
load("dataexcess.mat");   % Remove the percent sign to activate
%load("averages.mat");    % Add a percent sign to comment out
* To Analyze Reported Deaths:
Matlab
%load("dataexcess.mat");  % Comment out
load("averages.mat");     % Activate
5. THE 20 INDEPENDENT VARIABLES
Following the removal of "GDP Nominal" to prevent multicollinearity, the model is built upon the following 20 predictors:
1. Demographic (7): Median Age, Population Density, and 5 Age Cohorts (0-4, 5-14, 15-24, 25-64, 65+).
2. Health (5): Obesity, Diabetes, Hypertension, Cardiovascular Death Rate, Lung Diseases.
3. Economic (2): GDP per capita, Unemployment Rate.
4. Socio-Political (6): Gini Coefficient, HDI, IHDI, GII, Democracy Index, Life Expectancy.
6. REQUIRED RAW DATA FILES
For the preparation scripts to function (if run from scratch), the following files must be present in the working directory:
* owid-covid-data.csv
* excess-deaths-cumulative-per-100k-economist.csv
* gini.csv, gdppercapita.csv, unemployment.xls
* obesity 2020.csv, obesity 2021.csv, obesity 2022.csv
* diabets.csv, hypertension-adults-30-79.csv, lung diases.csv, prevelance of Cardiovascular diseases.csv
* population-density.csv, population-by-age-group.csv, median-age.csv
* democracy-index-eiu.csv, hdi2019.xlsx, ihdi2019.xlsx, gii.xlsx, lifeexpectancy2019.xlsx
7. OUTPUTS & VISUALIZATION
Upon completion of the regression analysis, the system automatically executes:
1. GRAPHS.m: Tests model assumptions (VIF, White Test, Breusch-Pagan, Durbin-Watson) and plots diagnostic charts.
2. figure1_code_new.m: Generates the final publication-ready figure:
o Panel A: Model Performance (Observed vs. Predicted).
o Panel B: Predictor Strength (Ranked by Standardized Beta coefficients).
o Panel C: Bivariate association plots.


