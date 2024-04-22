---
layout: page
title: Brainstorming, sneakpeek
description: How we made a new metric?
---

``` python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

``` python
data = pd.read_csv("1Aspiring_with_emp_score.csv")
```

``` python
print(data.isnull().sum())
```

    ID                       0
    Salary                   0
    DOJ                      0
    DOL                      0
    Designation              0
    JobCity                  0
    Gender                   0
    DOB                      0
    10percentage             0
    10board                  0
    12graduation             0
    12percentage             0
    12board                  0
    CollegeTier              0
    Degree                   0
    Specialization           0
    collegeGPA               0
    CollegeState             0
    GraduationYear           0
    English                  0
    Logical                  0
    Quant                    0
    Domain                   0
    ComputerProgramming      0
    ElectronicsAndSemicon    0
    ComputerScience          0
    MechanicalEngg           0
    ElectricalEngg           0
    TelecomEngg              0
    CivilEngg                0
    conscientiousness        0
    agreeableness            0
    extraversion             0
    nueroticism              0
    openess_to_experience    0
    Period                   0
    gyear                    0
    12GradAge                0
    GradAge                  0
    AverageScore             0
    Acadperf                 0
    time_gap                 0
    Employability_Score      0
    dtype: int64

``` python
# Separate numerical and non-numerical columns
numerical_cols = data.select_dtypes(include=['float64', 'int64']).columns
non_numerical_cols = data.select_dtypes(exclude=['float64', 'int64']).columns
```

``` python
# Calculate correlation matrix for numerical columns only
corr = data[numerical_cols].corr()
```

``` python
# Plot the correlation matrix
plt.figure(figsize=(12, 10))
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.show()
```

![](/vertopal_9162bf60bd05496a964e297ece94f65a/636b588a0bdefb7abb870572931e4c15ce9f3658.png)

``` python
import matplotlib.pyplot as plt

# Create subplots with shared y-axis
fig, axs = plt.subplots(2, 3, figsize=(18, 12), sharey=True)

# Plot each personality trait against Employability_Score
axs[0, 0].scatter(data['conscientiousness'], data['Employability_Score'])
axs[0, 0].set_xlabel('Conscientiousness')
axs[0, 0].set_ylabel('Employability_Score')
axs[0, 0].set_title('Conscientiousness vs Employability_Score')

axs[0, 1].scatter(data['agreeableness'], data['Employability_Score'])
axs[0, 1].set_xlabel('Agreeableness')
axs[0, 1].set_title('Agreeableness vs Employability_Score')

axs[0, 2].scatter(data['extraversion'], data['Employability_Score'])
axs[0, 2].set_xlabel('Extraversion')
axs[0, 2].set_title('Extraversion vs Employability_Score')

axs[1, 0].scatter(data['nueroticism'], data['Employability_Score'])
axs[1, 0].set_xlabel('Nueroticism')
axs[1, 0].set_ylabel('Employability_Score')
axs[1, 0].set_title('Nueroticism vs Employability_Score')

axs[1, 1].scatter(data['openess_to_experience'], data['Employability_Score'])
axs[1, 1].set_xlabel('Openness to Experience')
axs[1, 1].set_title('Openness to Experience vs Employability_Score')

# Remove empty subplot
fig.delaxes(axs[1, 2])

plt.tight_layout()
plt.show()
```

![](/vertopal_9162bf60bd05496a964e297ece94f65a/b52ee8d01fe228cae6ee8203fc74c99733b10ce1.png)

``` python
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 8))

# Plot all personality traits against Employability_Score
plt.scatter(data['conscientiousness'], data['Employability_Score'], label='Conscientiousness')
plt.scatter(data['agreeableness'], data['Employability_Score'], label='Agreeableness')
plt.scatter(data['extraversion'], data['Employability_Score'], label='Extraversion')
plt.scatter(data['nueroticism'], data['Employability_Score'], label='Nueroticism')
plt.scatter(data['openess_to_experience'], data['Employability_Score'], label='Openness to Experience')

plt.xlabel('Personality Traits')
plt.ylabel('Employability_Score')
plt.title('Personality Traits vs Employability_Score')
plt.legend()
plt.grid(True)

plt.show()
```

![](/vertopal_9162bf60bd05496a964e297ece94f65a/b5c04c537127172e797e641bfa2720bcbed1b7e0.png)

``` python
# Select relevant columns
cols = ['conscientiousness', 'agreeableness', 'extraversion', 'nueroticism', 'openess_to_experience', 'Employability_Score']
corr = data[cols].corr()

# Plot the correlation matrix
plt.figure(figsize=(8, 6))
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
```

![](/vertopal_9162bf60bd05496a964e297ece94f65a/72571b043d38c90c1c6ec6419ae26068443d1716.png)

``` python
# Convert 'Designation' to a categorical variable
data['Designation'] = data['Designation'].astype('category')

# Bar plot for mean conscientiousness score by designation
data.groupby('Designation')['conscientiousness'].mean().plot(kind='bar', figsize=(10, 6))
plt.xlabel('Designation')
plt.ylabel('Mean Conscientiousness Score')
plt.title('Conscientiousness by Designation')
plt.show()

# Repeat for other personality traits
# You can also use box plots instead of bar plots
```

    /tmp/ipykernel_32701/3439493292.py:5: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      data.groupby('Designation')['conscientiousness'].mean().plot(kind='bar', figsize=(10, 6))

![](/vertopal_9162bf60bd05496a964e297ece94f65a/f8a8f52c7d598b269550145477d9c35a8b7d56cc.png)

``` python
import statsmodels.api as sm

# Linear regression model for salary
X = data[['conscientiousness', 'agreeableness', 'extraversion', 'nueroticism', 'openess_to_experience']]
y = data['Employability_Score']
X = sm.add_constant(X)  # Adding a constant for the intercept
model = sm.OLS(y, X).fit()
print(model.summary())
```

                                 OLS Regression Results                            
    ===============================================================================
    Dep. Variable:     Employability_Score   R-squared:                       0.059
    Model:                             OLS   Adj. R-squared:                  0.057
    Method:                  Least Squares   F-statistic:                     49.66
    Date:                 Tue, 26 Mar 2024   Prob (F-statistic):           4.77e-50
    Time:                         01:37:23   Log-Likelihood:                -14864.
    No. Observations:                 3998   AIC:                         2.974e+04
    Df Residuals:                     3992   BIC:                         2.978e+04
    Df Model:                            5                                         
    Covariance Type:             nonrobust                                         
    =========================================================================================
                                coef    std err          t      P>|t|      [0.025      0.975]
    -----------------------------------------------------------------------------------------
    const                    58.9373      0.168    350.985      0.000      58.608      59.267
    conscientiousness        -0.7669      0.187     -4.107      0.000      -1.133      -0.401
    agreeableness             1.8366      0.227      8.087      0.000       1.391       2.282
    extraversion             -0.4628      0.193     -2.394      0.017      -0.842      -0.084
    nueroticism              -1.9583      0.167    -11.701      0.000      -2.286      -1.630
    openess_to_experience     0.0104      0.202      0.052      0.959      -0.386       0.407
    ==============================================================================
    Omnibus:                       37.685   Durbin-Watson:                   2.030
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               38.632
    Skew:                           0.231   Prob(JB):                     4.08e-09
    Kurtosis:                       3.137   Cond. No.                         2.62
    ==============================================================================

    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.

``` python
```
