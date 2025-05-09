Weather-Energy Relationship Data Warehouse Project

Overview:

This project investigates the relationship between weather conditions and energy consumption patterns across multiple U.S. cities. By integrating weather data from the Open-Meteo API and energy data from the EIA API, we've created a comprehensive data warehouse that enables advanced statistical analysis of how temperature and other weather variables impact energy demand.

Our findings reveal a clear U-shaped relationship between temperature and energy demand, with regional variations and seasonal patterns that have significant economic implications. The project implements a complete data pipeline: from extraction and cleaning to integration, analysis, and visualization.

Project Structure:

├── functions/
│   ├── Weather_Extract_Clean.Rmd       # Weather data extraction and cleaning
│   ├── Energy_Extract_Clean.Rmd        # Energy data extraction and cleaning
│   ├── Merge_Energy_Weather.Rmd        # Data integration
│   ├── EDA_Final.Rmd                   # Exploratory data analysis
│   ├── Interactive_Visualisations.Rmd  # Interactive visualizations
│   └── index.Rmd                       # Main project navigation
├── data/
│   ├── raw/                            # Raw data from APIs
│   ├── processed/                      # Cleaned and transformed data
│   └── backup/                         # Backup of original data
├── results/
│   ├── figures/                        # Static visualizations
│   └── reports/                        # Reports
├── PPT/
│   └── presentation.Rmd                # Class presentation slides
├── config/
│   ├── setup.R                         # Shared parameters and functions
│   └── eia_api_key.txt                 # API key (gitignored)
├── README.md                           # Project documentation (this file)
├── requirements.txt                    # Package dependencies
├── data_dictionary.md                  # Variable definitions
├── session_info.txt                    # R environment details
└── .gitignore                          # Git ignore file
├── _targets.R                          # Defines the workflow and dependencies within the project
└── Main.R                              # script handling data upload, modifications, and error processing
├── Project_Report.R                    # Project Report
└── Technical_Appendix.R                # Technical Appendix
├── cross-doc-links.html                # Create links between project report and technical appendix

Key Findings

U-Shaped Relationship: Energy demand follows a robust U-shaped pattern with temperature, with minimum energy usage occurring at approximately 51.5°F (95% CI: 50.8-52.2°F).
Regional Variations: Weather sensitivity varies substantially by region, with some regions showing up to 2x higher temperature elasticity than others.
Seasonal Effects: Seasonal factors beyond temperature significantly impact energy demand, with summer demand 26.5% above spring baseline.
Economic Implications: Each 1°F deviation from optimal temperature increases energy demand by approximately 2.03% on average.
Predictive Power: Random Forest models achieve 93.1% improvement in predictive accuracy compared to linear regression, demonstrating the complex nature of weather-energy interactions.

Getting Started
Prerequisites

R (version 4.1.0 or higher)
RStudio (for .Rmd files)
Required packages (install using requirements.txt)

Installation

Clone this repository:
git clone https://github.com/yourusername/weather-energy-project.git
cd weather-energy-project

Install required packages:
install.packages(c("tidyverse", "httr", "jsonlite", "lubridate", 
                  "readxl", "plotly", "DT", "corrplot", "skimr", 
                  "ggpubr", "scales", "viridis", "patchwork",
                  "mgcv", "lmtest", "car", "quantreg", "segmented", 
                  "Hmisc", "gridExtra", "nlme", "sandwich", 
                  "boot", "performance", "effects", "MASS", 
                  "randomForest", "gbm", "caret", "kableExtra"))

Set up API access:

Create an EIA API key at https://www.eia.gov/opendata/
Create a file at config/eia_api_key.txt containing only your API key



Running the Project
Execute the R Markdown files in the following order:

Data Extraction and Cleaning:

Run Weather_Extract_Clean.Rmd to retrieve and process weather data
Run Energy_Extract_Clean.Rmd to retrieve and process energy data


Data Integration:

Run Merge_Energy_Weather.Rmd to combine the datasets


Analysis:

Run EDA_Final.Rmd for exploratory data analysis
Run Interactive_Visualisations.Rmd for interactive exploration


View the Results:

Open index.Rmd to navigate through all project components
Interactive visualizations will be available in output/interactive/



Data Sources
Weather Data

Source: Open-Meteo ERA5 Historical Weather API
URL: https://archive-api.open-meteo.com/v1/era5
Variables: Temperature, humidity, precipitation, wind speed, cloud cover
Coverage: 20 major U.S. cities
Time Period: January 1, 2024 - December 31, 2024

Energy Data

Source: U.S. Energy Information Administration (EIA) API v2
URL: https://api.eia.gov/v2/electricity/rto/daily-region-data/data/
Variables: Energy demand, generation, and interchange
Coverage: Multiple U.S. energy regions
Time Period: January 1, 2024 - December 31, 2024

Methodology

Data Extraction: Automated retrieval from APIs with error handling and rate limit management
Data Cleaning: Standardization, missing value handling, and feature engineering
Data Integration: Custom mapping between weather locations and energy regions
Exploratory Analysis: Visualization of relationships and patterns
Statistical Modeling: Multiple approaches (parametric, non-parametric, machine learning)
Validation: Cross-validation, bootstrapping, and robustness checks

Key Visualizations

U-Shaped Relationship: Temperature vs. energy demand with optimal point
Regional Sensitivity Map: Geographic visualization of temperature elasticity
Seasonal Patterns: Energy demand variation across seasons
Interactive Dashboard: Web-based exploration of weather-energy relationships

Contributors

Student 1: Ajinkya Phanse - Weather data extraction and analysis
Student 2: Darshit Shah - Energy data extraction and analysis

License
This project is licensed under the MIT License - see the LICENSE file for details.
Acknowledgments

Data provided by Open-Meteo and the U.S. Energy Information Administration
Project completed as part of the Data Warehousing course at [University Name]
Special thanks to Stevenson Attuesta for guidance and feedback

Contact
For questions or feedback about this project, please contact:

ajinkyaphanse2996@gmail.com
https://github.com/amp660

