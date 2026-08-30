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
