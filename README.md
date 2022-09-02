# Social_media Project
# SEGMENT 2: 
This README provides an overview of the work completed in segment one and two (and much of segment three). 

## Meet Team 10: 

- Izzy Diaz
- Rashid Abdella
- Mariela Kinn
- Michaela Austin

## Team Roles, Standards, and Summary of Work: 

Team 10 split the project into two subgroups: Machine Learning (Izzy and Rashid) and Database Creation (Mariela and Michaela). Due to the nature of partner work, we did not split branches out by individual. Instead, we created branches based on specific tasks (i.e. cleaningBranch, practiceML). 

During segment 1, Mariela and Michaela used Pandas to clean the dataset, removing null values, duplicates, and excess columns. Then, they connected Python to PostgresSQL in order to store the data. In SQL, they created fourth tables-- one from the cleaned primary dataset, and three from three additional datasets (us_regions, visits, and seasons. They used left join to combine the datasets. The team of 4 worked together to determine which columns were most important to include in the model. Izzy and Rashid used the clean dataset to build out a draft machine learning model. With the data loaded, they worked to employ several different methods of binning. 

During segment 2, Michaela and Mariela worked together to import the team's final csv into Tableau Public, and begin visualizing the data. They created twelve visualizations: Leads by Month, Spend by Month, Impressions by Month, Lead vs. Spend, Spend Distribution by Brand, Map Studio Count, Heatmap Spend, Agency Spend by Brand, CPL by Agency, CPL by Brand, MAP Cost Per Lead, and MAP Cost Per Impression. These interactive visualizations vary in type: bar charts, line charts, scatter plots, and maps. After completing the visualizations, they worked together to format and design the graphs so that they match the aesthetics of our Google Slides. Mariela and Michaela also further developed Google Slide content during this segment. 

Izzy and Rashid were steeped in the machine learning model testing this week. They tested multiple models, including the logistic regression model. After receiving feedback from TAs and tutors, they implemented different methods to increase accuracy of the model. In particular, Izzy believed some columns were weighted differently, and were therefore skewing the ability to predict on our target. So, he received feedback to scale all numerical columns to remove the possibility of magnitude affecting the model categorical columns. Later, they completed a feature importance test which informed us that the model does not seem to think many/any of the columns are important predictors on leads. If anything, impressions had a slight importance. They received feedback to try only looking at one brand, one state, and retest to see if leads is a good target variable. So, Mariela and Michaela worked in pgAdmin to query an updated CSV for the machine learning model that includes only B1 brand and the state of CA, with the columns: leads, impressions, agency, reach, link clicks, spend, state, and brand. Rashid and Izzy will use this refined dataset for preprocessing and binning, with hopes that the model will run better.


All team members work to troubleshoot challenges through the following methods: office hours, tutoring sessions, reviewing past modules, and internet research (i.e. slack overflow).

### Communication Protocols: 

Our team has maintained a collaborative approach to the project by checking in with each other daily. In addition to meeting during set class time, all team members participate in extended working sessions on the weekends. Ongoing communication helps team members stay apprised of eachother’s work, and also helps avoid git conflicts. Specific methods of communication include: Slack messages, huddles, and Zoom meetings.

## Our Topic, Initial Thoughts: 
Topic: Digital marketing spend in 3 different fitness studios/concepts

Reason we selected topic: Team 10 is interested in why X company's desire to be more strategic with their spend on digital marketing advertisement. The company currently own 3 brands and have little-to-zero visibility on agency performance. This project will explore which features are most predictive of a brand's success.

Data Source: CSV files obtained directly from X company, anonymized for confidentiality purposes. The original CSV includes 56 columns and over 200 rows of data.


## Primary Question:
This project concerns itself with the following question: Within the state of X or the country of X, can we predict the amount of leads based off the following features (spend, ad type, impressions)?

## Our Datasets:
### First-Download:
A concern held by our team was the use of "shallow", flat data files such as our first CSV. In this example, leveraged a sample firm's historical data across four social media platform accounts, with no more than 500 rows in total (spanning one-year of campaigns). We quickly realized that in lacking more rows, our features would lack the ability to train/test and then predict with accuracy during the ML portion of our project. 

### Dataset 1 - Primary/SM Firm Data:
As a result, we expanded our selection to a dataset that holds over 200,000 anonymized rows from our work.

### Dataset 2 - Secondary/Sample Survey:

### Issues in selecting the target and input features: 
Initially, by leveraging our primary dataset, we knew the target would either fall on the "impressions" or "leads" columns. Of the two, we understood the leads data to be the most beneficial target column, and more indecitive of a factor towards foot-traffic in our sample businesses. 

However, in debating the many machine learning modules, we were torn on which columns provided the most tangible meaning to predict or affect our target. A common question held was: How do we weight one column over another, such as the number of impressions vs the total spend on an ad?

## Technologies Used: 
### Data Cleaning, Exploration, and Analysis:
Pandas is the Python library we used to clean the data and perform exploratory analysis.

### Database Storage:
We are using pgAdmin to store the data.
 
### Machine Learning: 
SciKitLearn is the ML library we are using to create a classifier.


### Dashboard: 
We will be using Tableau Public to visualize our findings.

## Selecting our Model: 
### Stand-In Model, Neural Network:
#### Loading our Data:
In this first step, we loaded our uncleaned version of the CSV. Our approach was to drop as many columns with Nan values or confidential information that would not serve as important features in our predictive model. 
But from a broader perspective, we simply needed to reduce the amount of noise in our data, and confirm if a neural network is a lost-cause in terms of its predictive accuracy on the "leads" column. 
![load data](https://user-images.githubusercontent.com/102266450/185756802-4194f18d-8bde-417b-b0d8-b0fe04c3a626.gif)
#### Dropping Columns:
Next, we ran a simple pandas dataframe check to see the the amount of data and types, per column. As a group, we understood that at this stage, we are less concerned with cleaning within each column, and were able to identify a drop from 52 to 17 total columns for the purpose of a stand-in model: 
![drop columns](https://user-images.githubusercontent.com/102266450/185756942-f277d817-10ee-4327-b05f-2d1c7f1096b7.gif)
#### Reduction of Brands: 
We did however experiment with dropping the "B3" row values within the "brand" column. With over 200,000 rows of data, we thought it best to only compare B1 vs B2, so that our model is not overwhelmed by the unclean data sheet. 
Our approach was to create a simple for loop that checked for the number of unique values, returned its name, and then leveraging the "loc" function our dataframe to remove any rows equal to "B3" designations: 
![reduction to b1+2](https://user-images.githubusercontent.com/102266450/185757049-841728b9-5fdd-4bbe-8b83-c7fec4dbad69.gif)
Lastly, here is the process of dropping the B3 rows and the noisy columns: 
![dropped B3+noisy columns](https://user-images.githubusercontent.com/102266450/185757090-08b241da-24f6-4d9c-b77f-868f78a328dd.gif)

#### Training Approach:
#### Measuring Accuracy: 

#### Sample Process: 
### Option 2: 
#### Training Approach:
#### Measuring Accuracy: 

#### Sample Process: 

## Database Creation: 
### ERD: [ERD](https://github.com/marielakinn/Social_media/blob/main/SQL%20Queries%20and%20ERD/ERD%20Table.xlsx)


## Limitations to the Dataset and Model: 

## Draft Presentation(UPDATED 9/2/2022): [GoogleSlides](https://docs.google.com/presentation/d/1znRkusDe7-G68lACfZTGBikjaQkrRGYngHLJKc4Vmec/edit#slide=id.p)



