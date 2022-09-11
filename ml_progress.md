# Machine Learning
## ML Phase One:
### Deliverable 1: Stand-In Model
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

#### Continued Cleaning Approach:
##### Binning: 
After reducing the 'brand' column, we did a quick df.info() to check on the remaining columns: state, brand, spend, platform, date start, impressions, leads, link clicks, reach and agency. 
Of these columns, we checked the unique values in each, scanning for numbers greater than 10, on the non-numeric columns of interest such as: agency, date start, and state: 
![unique vals](https://user-images.githubusercontent.com/102266450/187090865-8c34a305-e8c4-4267-b195-113910cbf1d0.gif)

Then, we checked with "value_counts()" function on each of these three columns. The process for the "state" column is shown below: 
![state value counts](https://user-images.githubusercontent.com/102266450/187090872-e22e6def-c8f3-412b-a5c3-ac8b51aae1fc.gif)

To bin effectively, we debated an external tool such as "OptBinning" which sets equal bins; but ultimately favored following a similar process to the model and expanded to a "Tier" system.

In general, our density plot (see below) showed the tail trailing off to the right, and we decided to use a groupby on our state column with the impressions column. In this process, we returned the value counts attached by state, and then did a simple merge created the following: 
![merge state counts](https://user-images.githubusercontent.com/102266450/187090886-bc0f31cd-78af-4957-908c-4dd29806e220.gif)

After this, we created the "state tiers" column, showing binning from 0-1000, 1000-5000, 5000-10000, and lastly anything towards the upper limit of 40000: 
![tiers](https://user-images.githubusercontent.com/102266450/187090894-d09ffc7a-8f18-40d6-a09e-ed0137af429b.gif)

You can see that we removed a signficant amount of datapoints by dropping the Nan values, as well as properly attached the following states to a Tier designation, 1-4: 
![tiers check](https://user-images.githubusercontent.com/102266450/187090908-02a5b87c-6fc9-46de-84ec-c47d39057bab.gif)

Thereafter, we replicated a very similar process for the agency column. 

##### Results and Second-Thoughts: 
Upon cleaning this initial csv, we contemplated using SVM, Random Forest, Logistic Regression, and Neural Network models. 
We understood that with a target variable of 'leads', as a binary yes or no lead would require a binary classification model of some sort. 
Of the options above, SVM ran far too long with so many columns and tiers. And when we next focused on either Logistic Regression or the Neural Network, we only saw outputs of 55% or less in predictive accuracy. 

We started to dig deeper and eventually adopted the following notebooks: 
1. Within ML Data and Preprocessing Folder---We held 4 distinct notebooks, one for each brand (1-3), and a fourth notebook that focuses on brand 2, for the state of CA exclusively. 
2. Within the same folder, we then outputed: b1_df.csv, b2_df.csv, b3_df.csv and ca_b2_df.csv to then send off to our "Model Tests" folder for optimzation. Please note, for the 80.2% accuracy mark achieved and mentioned below, we leveraged the CA preprocessing book and the ca_b2_df.csv. 

###### View of our Preprocessing Book - CA + Brand 2: 
Please note, we once again created our agency tier, but dropped the state tier as it was redundant. 
Here is a view of the csv prior to new changes: 
![df4 view](https://user-images.githubusercontent.com/102266450/188338301-4e57369f-8f6f-4588-9122-8e6c586ed18a.gif)

Beyond this, we took the binning process a step forward and leverage a 'optbinning' library to estimate which column would have the most success, regardless of noise in the data and model type: 
![woe bin](https://user-images.githubusercontent.com/102266450/188338306-e13327f4-99f5-44fa-903f-9c39cf18bb8d.gif)

Above, we focused on the 'spend' column to map how our binning processed did; in this case we show negative correlation with the line drawn (we anticipate that the spend column will have some positive affect on the model in terms of predictions). The "woe" indicates the weight of evidence on each bin. We are essentially seeing if we can bin properly to test for events to occur!

Next, we used the "scorecard" library, similar to the concepts in Optbinning package to check the "iv" or information value score for each of our columns, as it tires to bin and predict on leads. We found postive correlations in most of our columns, and were pleasantly surprised to find the most "indicative" column would be impressions or link clicks. 
This logically makes sense, as we expect clicks to contribute as a metric towards a lead: 
![woe bin all](https://user-images.githubusercontent.com/102266450/188338313-1b22e73e-cd13-4e7c-be0c-29e0d9a4226c.gif)

Quick note: The IV is also known as the stastical distance from the bin, the "Divergence". 
We observed that many of these columns showed promise, including the ones shown above! 

## Deliverable 2-3: ML Optimization: 
Following the preprocessing notebooks and CSVs mentioned above, we currently stand at 80.2% model accuracy, when using a Neural Network approach, for the state of CA. 
We decided to use CA as it contained nearly 25,000 rows of data after the cleaning process and due to its consistent 55% mark regardless of modeling in the earlier stages. 
For the next deliverable, in particular for the closing of our model focus we hope to test all states individually, with the designation of either brand 1, 2, or 3. 
Our hope is to uncover if one of the brands contains lacking or noisy data and to also observe trends by states. Upon completion of these model tests, we expect to build a visualization explaining which state and brand benefited the most and least from our neural networks. 

## Final Optimization
### Neural Network Models: 
### SVM Models: 
![image](https://user-images.githubusercontent.com/102266450/189461068-c534888d-1d63-4f0e-8d89-18f9dfb01b8a.png)

