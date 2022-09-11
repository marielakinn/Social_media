# Digital Marketing in the Fitness Industry

## Background

Team 10 is a consulting company that specializes in helping companies optimize their digital marketing performance. The Team's current client is Company X, a rapidly growing fitness company. Company X's goal is to expand their national reach, and gain was many gym members as possible. To achieve this goal, they employed ten different marketing agencies, and are investing thousands of collars in digital advertisements. The problem is the company has no visibility on agency performance, no knowledge of optimal marketing spend, and no understanding of market performance or seasonality trends. Team 10 conducted an exploratory analysis to better understand the Company's problems as well as potential. They also developed a machine learning model to support Company X in increasing the effectiveness of their digital marketing. 

## Resources
Python 3.7, Jupyter Notebook, pgAdmin, Tableau (NOTE: just list technologies like this, or include detailed version below:)

### Data Cleaning, Exploration, and Analysis:
Pandas is the Python library we used to clean the data and perform exploratory analysis.

### Database Storage:
We are using pgAdmin to store the data.
 
### Machine Learning: 
SciKitLearn is the ML library we are using to create a classifier.

### Dashboard: 
We will be using Tableau Public to visualize our findings.

## Key Questions
- What is the performance of each agency/brand?
- How does cost per lead (CPL) vary by season and by brand?
- How does digital marketing performance differ across regions?
- Can we predict leads off particular features?

## Steps of Analysis

Team 10 split the project into two subgroups: Machine Learning (Izzy and Rashid) and Database & Visualization (Mariela and Michaela).

### Cleaning & Explotation
Team 10 obtained two CSV files directly from Company X, anonymized for confidentiality purposes. The original CSV includes 56 columns and over 200 rows of data.Mariela and Michaela used Pandas to clean the dataset, removing null values, duplicates, and excess columns. Then, they created an [ERD](https://github.com/marielakinn/Social_media/blob/main/SQL%20Queries%20and%20ERD/ERD%20Table.xlsx).  Next, they used SQLAlchemy to connect Python to pgadmin in order to store the data. In SQL, they created fourth tables-- one from the cleaned primary dataset, and three from three additional datasets (us_regions, visits, and seasons. They used left join to combine the datasets. The team of 4 worked together to determine which columns were most important to include in the model. Izzy and Rashid used the clean dataset to build out a draft machine learning model. With the data loaded, they worked to employ several different methods of binning. 

### Machine Learning
Izzy and Rashid tested multiple models, including the logistic regression model. After receiving feedback from TAs and tutors, they implemented different methods to increase accuracy of the model. In particular, Izzy believed some columns were weighted differently, and were therefore skewing the ability to predict on our target. So, he received feedback to scale all numerical columns to remove the possibility of magnitude affecting the model categorical columns. Later, they completed a feature importance test which informed us that the model does not seem to think many/any of the columns are important predictors on leads. If anything, impressions had a slight importance. They received feedback to try only looking at one brand, one state, and retest to see if leads is a good target variable. So, Mariela and Michaela worked in pgAdmin to query an updated CSV for the machine learning model that includes only B1 brand and the state of CA, with the columns: leads, impressions, agency, reach, link clicks, spend, state, and brand. Rashid and Izzy will use this refined dataset for preprocessing and binning, with hopes that the model will run better.

### Visualization 
Michaela and Mariela worked together to import the team's final csv into Tableau Public, and begin visualizing the data. They created twelve visualizations: Leads by Month, Spend by Month, Impressions by Month, Lead vs. Spend, Spend Distribution by Brand, Map Studio Count, Heatmap Spend, Agency Spend by Brand, CPL by Agency, CPL by Brand, MAP Cost Per Lead, and MAP Cost Per Impression. These interactive visualizations vary in type: bar charts, line charts, scatter plots, and maps. Izzy also completed machine learning specific visualizations in Tableau (NAME SPECIFIC ONES) After completing the visualizations, they worked together to format and design the graphs so that they match the aesthetics of our Google Slides. The Team worked collaboratively to further develop Google Slide content. 


## Results

- Tableau findings
- ML findings

## Limitations
1. Machine Learning Model does not understand what we are trying to do with so many states. Accuracy rate decreases significantly when we run model for all states
2. 1-year data (not able to do year-to-year seasonality comparisons)
3. Data organization
4. No revenue data– confidentiality limitations


## Recommendations for Future Analysis 
1. Include dataset with additional years in order to more accurately assess seasonality trends
2. If we had more time, more resources more data. Pursue second level of modeling. If we had x amount of money, posted ad in x state, to x demographics, what is likeliness of lead?
3. Get more data on outcomes of leads/ gather more data on leads
4. Get more data on campaigns -- Where was marketing placed? 

## Presentation:[GoogleSlides](https://docs.google.com/presentation/d/1znRkusDe7-G68lACfZTGBikjaQkrRGYngHLJKc4Vmec/edit#slide=id.p)



