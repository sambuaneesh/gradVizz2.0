---
layout: page
title: Employability Score, Story of how we made a new metric?
description: How we made a new metric?
---

The dataset did not contain any direct information about employment status or factors related to employability. The data consisted of personal information, educational qualifications, and test scores of individuals. To address this gap, we derived a new column or metric that could serve as a proxy for an "employability factor."

## Factors Considered

We considered the following factors for deriving the employability score:

1. **Weighted average of academic performance metrics:**
   - 10th percentage
   - 12th percentage
   - College GPA

```python
# Calculate academic score (weighted avg of 10th, 12th, and college percentages)
academic_score = (df["10percentage"]*0.2 + df["12percentage"]*0.3 + df["collegeGPA"]*0.5) / 3
```

2. **A score based on the individual's skills or domain knowledge:**
   - English
   - Logical
   - Quant
   - Computer Programming
   - Electronics and Semiconductor
   - Computer Science
   - Mechanical Engineering
   - Electrical Engineering
   - Telecommunication Engineering
   - Civil Engineering

```python
# Calculate skills score (avg of all skill columns)
skills_score = (df["English"] + df["Logical"] + df["Quant"] + df["ComputerProgramming"] + df["ElectronicsAndSemicon"] + df["ComputerScience"] + df["MechanicalEngg"] + df["ElectricalEngg"] + df["TelecomEngg"] + df["CivilEngg"]) / 10
```

3. **Time difference between an individual's graduation year and their date of joining (DOJ)**

```python
# Calculate time gap between graduation and joining (in years)
df["time_gap"] = (pd.to_datetime(df["DOJ"]) - pd.to_datetime(df["GraduationYear"], format="%Y")).dt.days / 365.25

# Normalize time gap (shorter is better)
normalized_time_gap = 1 - (df["time_gap"] - df["time_gap"].min()) / (df["time_gap"].max() - df["time_gap"].min())
```

## Methodology

We adjusted the weights for each of the three individual factors (academic score, skills score, and time gap) through trial and error to create a new column named "Employability_Score." The process of choosing these metrics and assigning weights was not random.

To determine the optimal set of metrics and weights, we performed the Ordinary Least Squares (OLS) regression test each time we considered a set of attributes to create the employability factor. Our goal was to maximize the R-squared value, which represents the standard deviation it provides for the personality traits.

Once we finalized the set of metrics and weights, we added the newly derived "Employability_Score" column to our dataset.

```python
# Calculate employability score (weighted avg of academic, skills, time gap, and salary)
employability_score = academic_score*0.25 + skills_score*0.25 + normalized_time_gap*0.3 + salary*0.2

# Add employability score to dataframe
df["Employability_Score"] = employability_score
```

## Conclusion

By deriving the "Employability_Score" column and performing scatterplot analysis, we were able to create a proxy for an employability factor and explore its relationship with various personality traits. This approach allowed us to leverage the available data and gain valuable insights into factors contributing to employability.