# Digital Marketing in the Fitness Industry

## Background

24/7 Fitness is a rapidly growing fitness company whose goal is to expand their national reach and acquire as many studio members as possible. They have employed ten different marketing agencies and are investing thousands of dollars in digital advertisements. The problem is the company has no visibility on agency performance, no knowledge of optimal marketing spend, and no understanding of market performance or seasonality trends. 

In search of strategic guidance, 24/7 Fitness hired Business Analytics Team Force (B.A.T. Force),  a consulting company that specializes in helping companies optimize their digital marketing performance.  B.A.T. Force quickly stepped in and has conducted an exploratory analysis to better understand 24/7 Fitness' problem areas as well as potential for growth. Then, they developed a robust machine learning model to support 24/7 Fitness in increasing the effectiveness of their digital marketing. 

## Resources

### Data Cleaning, Exploration, and Analysis:
Pandas is the Python library we used to clean the data and perform exploratory analysis.

### Database Storage:
We used SQLAlchemy to connect Python to pgAdmin in order to store the data.
 
### Machine Learning: 
SciKitLearn is the ML library we used to create a classifier.

### Dashboard: 
We used Tableau Public to visualize our findings.

## Key Questions
- What is the performance of each agency/brand?
- How does cost per lead (CPL) vary by season and by brand?
- How does digital marketing performance differ across regions?
- Can we predict leads off particular features?

## Steps of Analysis

B.A.T. Force split the project into two subgroups: Machine Learning (Izzy and Rashid) and Database & Visualization (Mariela and Michaela).

### Cleaning & Exploration
B.A.T. Force obtained two CSV files directly from 24/7 Fitness, anonymized for confidentiality purposes. The original CSV included 56 columns and over 200 rows of data. Mariela and Michaela used Pandas to clean the dataset, removing null values, duplicates, and excess columns. Then, they created an [ERD](https://github.com/marielakinn/Social_media/blob/main/SQL%20Queries%20and%20ERD/ERD%20Table.xlsx).   Next, they used SQLAlchemy to connect Python to pgAdmin in order to store the data. In SQL, they created four tables: one from the cleaned primary dataset, and three from three additional datasets (us_regions, visits, and seasons. They used left join to combine the datasets. The team of 4 worked together to determine which columns were most important to include in the model. Izzy and Rashid used the clean dataset to build out a draft machine learning model. With the data loaded, they worked to employ several different methods of binning. 

### Machine Learning
Izzy and Rashid tested multiple models, including the logistic regression model. After receiving feedback from TAs and tutors, they implemented different methods to increase accuracy of the model. In particular, Izzy believed some columns were weighted differently, and were therefore skewing the ability to predict on our target. So, he received feedback to scale all numerical columns to remove the possibility of magnitude affecting the model categorical columns. Later, they completed a feature importance test which informed us that the model does not seem to think many/any of the columns are important predictors on leads. If anything, impressions had a slight importance. They received feedback to try only looking at one brand, one state, and retest to see if leads is a good target variable. So, Mariela and Michaela worked in pgAdmin to query an updated CSV for the machine learning model that includes only B1 brand and the state of CA, with the columns: leads, impressions, agency, reach, link clicks, spend, state, and brand. Rashid and Izzy then used this refined dataset for preprocessing and binning, with hopes that the model would run better. For a more detailed overview of the Machine Learning process, please read [ml_progress.md](https://github.com/marielakinn/Social_media/blob/main/ml_progress.md).

### Visualization 
Michaela and Mariela worked together to import the team's final CSV into Tableau Public, and began visualizing the data. They created multiple dashboards: Background, Lead Generation, Trends in Leads and Spend and 2021 CPL Dashboard. The dashboards include interactive visualizations that vary in type: bar charts, line charts, scatter plots, and maps. Izzy and Rashid also completed machine learning specific visualizations in Tableau. After completing the visualizations, B.A.T. Force worked collaboratively to synthesize their findings into a Google Slide presentation. 


## Results

### Tableau Findings
- The systemwide CPL is $19.25
- Brand 2 is the highest performing brand, as demonstrated by its low CPL($18.76)
- Agency 8 and Agency 3 are the highest performing agencies, with the lowest CPLs ($15.91 and $17.64 respectively)
- Winter is the most optimal season for digital marketing, as CPL decreases to an average of $17.52

### ML Findings
- Random Forest Algorithm is the best model to predict leads
- ADD ADDITIONAL FINDINGS ONCE ML.md IS COMPLETE

## Limitations
1. Accuracy rate decreases significantly when we run model for all states
2. Only one-year of data (not able to do year-to-year seasonality comparisons)
3. No lead-to-conversion rate data



## Recommendations for Future Analysis 
1. Obtain better quality lead data, including: what is the membership to lead ratio; why didn't link clicks convert to leads?
2. Collect demographic data, including: who is being targeted by campaigns, where do leads live; where was marketing placed; what mile radius from gym did campaign cover?
3. Conduct ARIMA Model in order to assess lead level (i.e. campaign x resulted in # of leads), rather than simply tracking whether a campaign resulted in a lead (yes/no).

## Presentation: [Google Slides](https://docs.google.com/presentation/d/1znRkusDe7-G68lACfZTGBikjaQkrRGYngHLJKc4Vmec/edit#slide=id.p)

## Tableau Dashboard: [Digital Marketing Spend Dashboard](https://public.tableau.com/app/profile/mariela.kinn.terrazas/viz/DigitalMarketingSpend/Background?publish=yes)



