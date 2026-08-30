# **DSPP_May26_Summative**

---

## ***Data Science Project - Edinburgh House Prices***

The following shows the Data Science Project I did for the DPSS L4 Course. The initial scraped datasets along with post-processed dataset after pipeline transformations are included in this repository

---

### Executive Summary 

This project aims to explore whether different postal codes in Edinburgh has any effect on property prices in the city. Through data scraping of online resources, a dataset of residential property prices was obtained for the project.
Initial analysis - through summary statistics of the dataset used suggested - that prices did differ by area however, summary statistics on it’s own was not enough evidence for this. However, later on, through the use of a Kruskal Wallis non-parametric hypothesis test combined a post hoc Dunn test suggests that house prices do differ significantly in some postcode areas in the City of Edinburgh.

---

### Data Infrastructure & Tools 

Multiple tools were used during the duration of the project. As there was no public dataset already available that I could access for free to get information on property prices this meant I needed to utilise python to data scrape the information I needed for the project from the property website Rightmove of residential property prices in Edinburgh. 
I discovered a template Python script online written by Clarke (2024) which I used for the data scraping on Rightmove as is it performed the exact function that was required and was already tailored for the Rightmove website I was using. This data scrape leads on to the other tools I used of Excel and SQL Server Management Studio.   Excel was used to view the extracted dataset due to its familiarity and user friendly nature – including it’s simple features -  of reviewing data. 
Due to the nature of pipelining and data storage that SSMS provides with its ability to create and execute stored procedures and also manage security it made sense to use SSMS for the storage and transformations of the initial raw extracted dataset. More information on this will be provided in the next section – Data Engineering.
While Python was used for the initial extract, the functionality from imported packages like Pandas, Matplotlib, ‘scikit_posthocs’, and ‘scipy.stats’ allowed it to be used for both Data Visualisation and Analysis portions of this project as well. Pandas is widely used for data manipulation and Matplotlib is also widely used for the Data Visualisation through it’s ability to generate graphs and charts which is why it made sense to use for this project. The sci packages used also allowed for the statistical analysis that was required for this project.

---

### Data Engineering

---

### Data Analysis and Visualisations

Initial exploratory data analysis was performed on the exported dataset – to gain an initial high-level view of the transformed data itself. The initial exploratory analysis was done on Python using both the pandas package and matplotlib package to get both summary statistics of the dataset along with graphical visualisations of the distribution of data by different postcode areas respectively.

```python
summary = df.groupby("postcode_area")["normalised_price"].agg(["count", "mean", "median", "std", "min", "max"]) 

print(summary)
```

![histogram](assets/summary_stats.png)

As can be seen above, it appears that both the mean and median of the normalised prices by postcode area differs to some extent between different postcode areas. While the summary statistics can’t be considered as definitive evidence on its own - it is however, a good initial indicator that prices may differ by postcode area. It should also be noted that a count was done on each postcode area to see how many data points we had for prices. It was then decided that any postcode areas that had less than 30 records of data was to be removed from the analysis. This was done to remove any anomalies and noise present in the data since the limited amount of records available for that postcode area might distort the analysis or give us an incorrect value for the summary statistics. While it was decided that 30 would be the threshold for whether or not a postcode area would be included in the analysis it should be noted that this was a completely arbitrary decision as 30 seemed instinctually a reasonable threshold value to use.
After reading a guide on Hypothesis Testing on the University of Sheffield’s website, it was noted that many different hypothesis tests exist. As more than 3 different groups existed in this dataset, this meant that using either an ANOVA or Kruskal Wallis hypothesis test would be the most appropriate for the analysis. To help decide which one was to be used I needed to view how the data was distributed by different postcodes. The figures below – generated from the matplotlib package - shows the distributions price in different postcode areas.

![histogram](assets/postcode_histograms.png)

After looking at the visualisations of distributions for property prices in different postcodes it was seen generally that the data wasn’t normally distributed with most of the histograms skewed to the right. This meant that a non-parametric test would be more suitable to use as the hypothesis test (Allam, 2025). As the Kruskal Wallis test is a non-parametric test (Ostertagova, 2014) that doesn’t rely on normal distributions of data and is based on ranking rather than mean values of groups; the Kruskal Wallis test was used for the dataset.
With the hypothesis test settled on, the following null and alternative hypotheses were used:
H0 = There is no significant difference in the different postcode group medians
H1 = At least one postcode area group has a different median to the others.
Most commonly a significance level of 0.05 (Su, 2025) is used as the threshold to determine whether H0 is rejected or not. This will also be the case for this test and using the scipy.stats package the Kruskal Wallis test determined the following test statistics and p-value shown in script below:

```python
statistic, p_value = kruskal(*groups)

print("Kruskal-Wallis Test")
print("-------------------")
print("Statistic:", statistic)
print("P-value:", p_value)
```
