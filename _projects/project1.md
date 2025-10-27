---
layout: single
title: Accidental Drug-Related Deaths
date: 2025-05-04
toc: true
excerpt: "An exploration into accidental drug-related deaths in Connecticut (2012–2023), analyzing substance patterns, demographics, and model predictions."
---

[ML/AI Project][project]{: .btn .btn--info}

## Overview

### Background

I retrieved the dataset from a U.S. government data catalog (catalog.data.gov). The data covers accidental deaths related to drug overdoses in Connecticut between 2012–2023, collected through investigations by the Office of the Chief Medical Examiner. It contains 48 columns and 11,981 rows, with basic details such as Date, Age, Sex, City, and Injury type. It also lists various substances, where a “Y” indicates that a particular drug was detected at the time of death.

Although the data is geographically limited to Connecticut (which is a relatively small state), it provides meaningful insight into potential patterns in accidental drug overdose deaths. By analyzing this data, I aimed to uncover trends that could benefit stakeholders such as hospitals and police departments. Initially, my goal was to predict the geographical regions of the deaths so I could explore how a heatmap might guide hospital and police department placements for prevention efforts. However, after data profiling, I shifted focus toward predicting the **age** of individuals based on the circumstances and substances involved.

### Data Profiling and Descriptive Analysis

When I examined the value counts for ‘Drugs_Present’, fentanyl appeared as the most common drug involved. Interestingly, the second-most frequent combination was cocaine and fentanyl. I’m not familiar with drug use personally, but seeing that mix appear so often suggests there might be a specific reason behind the combination (though unfortunately, there were no columns for pricing or dosage amounts).

Most of the individuals were between ages 25–60. Although the data didn’t show many extreme outliers, just slightly thinned-out tails, I noticed several underage cases, which I decided to keep since there wasn’t enough information to justify removing them or form any strong correlations.

Across all age groups, the number of drugs present at the time of injury averaged around 3.3 (with a standard deviation of 1.52), ranging from 0 to 10. The histogram was nearly normal, with a slight right skew. This may suggest that the involvement of multiple drugs increases the likelihood of an accidental drug-related death.

During profiling, I had to perform a fair amount of hardcoding to condense redundant categories. For example, the dataset contained multiple race variations such as ‘ASIAN’, ‘ASIAN, OTHER’, ‘ASIAN INDIAN’, ‘OTHER ASIAN’, etc. I remapped these variations to simplify and strengthen the data. I did similar remapping for ethnicity and location, and I also filtered out rows where category counts were less than 10, since they didn’t provide enough data for reliable model training.

### Model Results and Conclusions

After building a pipeline to process both categorical and numerical data, I tested several models to predict age. To keep everything consistent, I evaluated all models using `accuracy_score()`.

**Random Forest Classifier**  
training results: 0.0762 (7.62%)  
testing results: 0.0266 (2.67%)  
**Conclusion:** Clear overfitting, and the model didn’t generalize well at all.

**Gradient Boosting Classifier**  
training results: 0.0631 (6.31%)  
testing results: 0.0269 (2.69%)  
**Conclusion:** Slightly less overfitting than the RF model, but still weak predictive power.

**Support Vector Machine**  
training results: 0.0521 (5.21%)  
testing results: 0.0287 (2.87%)  
**Conclusion:** Performed slightly better on the test set, but overall accuracy remained low.

**Bagging Decision Tree**  
training results: 0.0836 (8.36%)  
testing results: 0.0278 (2.78%)  
**Conclusion:** Overfitting again, and very limited generalization ability.

**MLP Classifier**  
training results: 0.0833 (8.33%)  
testing results: 0.0258 (2.58%)  
**Conclusion:** Worst performance among all the models; clear overfitting present.

### Improvements / Future Work

**Profiling**  
I spent a considerable amount of time cleaning up inconsistencies in how people entered data. I tried to avoid removing rows unnecessarily so that biases wouldn’t increase. Looking back, I would spend more time identifying and mitigating potential biases more systematically.

For instance, when I remapped the “Race” column, I grouped categories broadly by continent rather than keeping smaller subdivisions. This simplified modeling but also made it impossible to distinguish, say, Korean from Chinese. Keeping those subdivisions might improve nuance, but they could also introduce more bias or instability due to small sample sizes.

I also think mapping the ages of individuals on a geographic heatmap could show how certain age groups cluster by region. Using a model like KNN (K Nearest Neighbors) might help group new data points according to demographic proximity.

**Modeling**  
If I had more time, I’d focus on deeper hyperparameter tuning, especially in models with severe overfitting. I also want to understand more about how each parameter influences the model without falling into confirmation bias, just tuning until I get “nice-looking” results.

I’d also explore alternative scoring metrics like **balanced accuracy** or **F1-score** to see if they provide a better picture of model performance.

Beyond model performance, I’d like to connect the results to real-world implications: could a model like this ever become accurate enough to help public agencies, and if so, what safeguards would it need?

**More Data?**  
If I were able to apply a heatmap using the coordinates from ‘ResidenceCityGeo’, ‘InjuryCityGeo’, and ‘DeathCityGeo’, I could return to my original goal: predicting the geographic regions of deaths. It would be interesting to see whether overdoses are concentrated more in urban or rural areas.

More numerical variables would also strengthen the model. I had to manually create a “drug count” column since the dataset lacked numeric features. Data on dosage amounts or concentrations could have helped tremendously. For instance, comparing fatal doses relative to age or weight. Although such details may not be public due to privacy, even proxies or categorical dosage levels would have been useful. Adding a “holiday” column might also reveal temporal correlations, like spikes during specific holidays.

---

## Technology & Tools

### Languages

- Python

### Libraries

- pandas
- numpy
- matplotlib
- scikit-learn

### Methods / Classes / Functions Used

- **Pandas:** `.read_csv()`, `.drop()`, `.map()`, `.value_counts()`, `.fillna()`, `.astype()`, `.query()`, `.groupby()`, `.describe()`
- **NumPy:** `np.random.seed()`, `np.round()`
- **Matplotlib:** `plt.hist()`, `plt.scatter()`, `plt.xlabel()`, `plt.ylabel()`, `plt.title()`, `plt.show()`
- **Scikit-learn:**
  - `Pipeline`, `ColumnTransformer`, `FeatureUnion`, `StandardScaler`, `OneHotEncoder`, `IterativeImputer`
  - Models: `RandomForestClassifier`, `GradientBoostingClassifier`, `SVC`, `BaggingClassifier`, `MLPClassifier`
  - Metrics: `accuracy_score`, `classification_report`

### References

Data Source: [catalog.data.gov – Accidental Drug Related Deaths 2012–2023](https://catalog.data.gov/dataset/accidental-drug-related-deaths-2012-2018)  
Office of the Chief Medical Examiner, State of Connecticut.

---

[project]: #
