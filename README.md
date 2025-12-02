# Comparing Professor Salary to their Rating

This project analyzes the relationship between professors' salaries and their ratings at Bridgewater State University (BSU). The analysis examines whether higher-rated professors earn higher salaries and explores departmental variations.

## Project Structure

- **BSU_prof_salary.csv**: Raw data in CSV format containing professors' salaries and ratings.
- **BSU_prof_salary.xlsx**: Raw data in Excel format containing professors' salaries and ratings.
- **data_analysis.ipynb**: Jupyter Notebook for analyzing the data and visualizing the relationship between salaries and ratings.
- **data_scrapping.ipynb**: Jupyter Notebook for scraping or collecting the data used in this project.
- **README.md**: Project documentation.

## Getting Started

1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```

2. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```
   
   If you encounter any issues, you may need to install specific packages and upgrade pip:
   ```bash
   pip3 install --upgrade pip
   pip install statsmodels
   pip install seaborn
   ```

3. Open the Jupyter Notebooks to explore the data:
   ```bash
   jupyter notebook
   ```

## Data Overview

The dataset contains **175 professors** with the following key statistics:

### Salary Statistics
- **Mean Salary**: $77,096.94
- **Median Salary**: $82,746.35
- **Range**: $3,444.87 - $120,793.52
- **Highest Paid**: Steven Greenberg ($120,793.52)
- **Lowest Paid**: Jeanne Ingle ($3,444.87)

### Rating Statistics
- **Mean Rating**: 3.69 / 5.0
- **Median Rating**: 3.8 / 5.0
- **Range**: 1.7 - 5.0
- **Highest Rated**: David O'Malley (5.0)
- **Lowest Rated**: Chien Yu (1.7)

## Key Findings

### Overall Relationship: Weak Negative Correlation

**The analysis reveals virtually no meaningful relationship between professor ratings and salaries.**

- **Pearson Correlation**: r = -0.074 (p > 0.05)
- **Spearman Correlation**: r = -0.162 (p = 0.032)
- **95% Confidence Interval**: [-0.214, 0.070]

The correlation is so weak that it explains less than 1% of the variance in salaries. Importantly:
- The **highest-rated professor** (David O'Malley, 5.0) does NOT have the highest salary
- The **lowest-rated professor** (Chien Yu, 1.7) earns $106,674.74, well above the median
- The **highest-paid professor** (Steven Greenberg) has a rating of 4.3
- The **lowest-paid professor** (Jeanne Ingle) has a rating of 4.1

### Department-Level Analysis

The relationship between salary and rating varies significantly by department:

**Positive Correlations** (higher ratings → higher salaries):
- Languages: r = 0.930 (strongest positive, n=6)
- Music: r = 0.819 (n=4)
- Fine Arts: r = 0.766 (n=4)
- English: r = 0.408 (n=22)

**Negative Correlations** (higher ratings → lower salaries):
- Social Work: r = -0.996 (n=3)
- Criminal Justice: r = -0.937 (n=4)
- Physical Education: r = -0.788 (p = 0.020, statistically significant)
- Geography: r = -0.829 (n=5)

**Note**: After FDR correction for multiple testing, no department-level correlations remain statistically significant at α = 0.05, suggesting these patterns may be due to chance or confounding factors.

### Regression Analysis

Controlling for department fixed effects:
- The coefficient for rating is **-$3,095** (p = 0.374, not significant)
- This suggests that within departments, a 1-point increase in rating is associated with a $3,095 *decrease* in salary, though this finding is not statistically significant
- **Department membership** is a much stronger predictor of salary than rating

Quantile regression shows consistent negative coefficients across salary distribution:
- 25th percentile: -$3,200
- 50th percentile: -$4,052
- 75th percentile: -$4,004
- 90th percentile: -$4,004

## Interpretation

**Why might there be no positive correlation between ratings and salaries?**

1. **Salary is largely determined by factors other than teaching quality**: seniority, tenure status, research output, administrative roles, and market rates by field
2. **Rating systems may not accurately reflect teaching quality**: they can be influenced by course difficulty, grading leniency, and student biases
3. **Universities may not use ratings in salary decisions**: promotion and tenure committees often prioritize research and service over student evaluations
4. **Reverse causality**: higher-paid professors may teach more advanced courses that receive lower ratings due to difficulty

The weak negative trend (though not statistically significant) suggests that if anything, highly-rated professors might be slightly underpaid relative to their peers, potentially because they invest more time in teaching at the expense of other compensated activities.

## Data Analysis

The analysis includes:

- Descriptive statistics and distributions of salaries and ratings
- Correlation analysis (Pearson and Spearman)
- Department-level comparisons with FDR correction
- Regression modeling with department fixed effects
- Quantile regression across the salary distribution
- Visualizations including scatter plots, box plots, and departmental comparisons

## Data Collection

The `data_scrapping.ipynb` notebook demonstrates how the data was collected from:
- Salary data: Massachusetts State Employee Payroll Database
- Rating data: RateMyProfessors.com

## Requirements

- Python 3.x
- Jupyter Notebook
- Libraries: pandas, numpy, matplotlib, seaborn, scipy, statsmodels (install via requirements.txt)

## Limitations

- Sample size varies significantly by department (1-22 professors)
- Student ratings may not reflect actual teaching effectiveness
- Salary data may not account for additional income sources
- Cross-sectional data cannot establish causality
- Self-selection bias in who gets rated on RateMyProfessors

## Acknowledgments

- Salary data sourced from [Massachusetts State Employee Payroll Database](https://cthrupayroll.mass.gov/)
- Rating data sourced from [RateMyProfessors.com](https://www.ratemyprofessors.com/school/134)