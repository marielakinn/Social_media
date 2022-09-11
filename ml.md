# Machine Learning
## Primary Objective: 
Can we create a binary classifier on a target variable, leads, based off 4-5 columns/features? 
## Question: 
For every campaign ad (one row of data), can we predict for if a lead will occur based off impressions, spend, clicks, and reach?

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
## ML Phase Two:
## Deliverable 2-3: ML Optimization: 
Following the preprocessing notebooks and CSVs mentioned above, we currently stand at 80.2% model accuracy, when using a Neural Network approach, for the state of CA. 
We decided to use CA as it contained nearly 25,000 rows of data after the cleaning process and due to its consistent 55% mark regardless of modeling in the earlier stages. 
For the next deliverable, in particular for the closing of our model focus we hope to test all states individually, with the designation of either brand 1, 2, or 3. 
Our hope is to uncover if one of the brands contains lacking or noisy data and to also observe trends by states. Upon completion of these model tests, we expect to build a visualization explaining which state and brand benefited the most and least from our neural networks. 

## ML Phase Three:
## Final Optimization

### General Note:
In the final step, we narrowed our focus to brand 1, and created a notebook by ML focus: 
'ML(NN)-B1', 'ML(SVM)-B1', 'ML(RF)-B1'. Although we did track and replicate a neural network, SVM, and random forest book for brands 2 and 3, we committed to brand 1 results as it included the most cumulative data. 
Below you will find the process for the NN and RF models. Please note there are only slight differences in their approach, mainly after the splitting/training. We chose not to feature the SVM notebook here, but feel free to open it up within the "model tests" folder. 

### Filters: 
Upon loading our cleaned data, we checked the value counts by state and began to test by state tiers. For instance, a tier 1 state would hold 5000+ datapoints, whereas a tier state could contain less than 500 data rows. 
Here is an example as we loc by the state of Kentucky, a tier 2 state with 1200 datapoints: 
![image](https://user-images.githubusercontent.com/102266450/189549979-3755ed97-4cf5-4a26-8a8b-4a114073b251.png)

### Training/Testing: 
Our split, train, and scaling instances are excactly as shown in the module. 
#### NN Model:
However, here is the construction of our neural layers in the neural network: 
![image](https://user-images.githubusercontent.com/102266450/189550019-6ae80e38-f72c-4e87-90eb-30b6b75975a0.png)
One note---we did find that the best mix relied on a combination of relu/elu and hard sigmoid activation functions. Upon running, we stuck to 100 epochs and tested the keras library for activation functions. 
#### RF Model:
##### Feature Importance Addition: 
Unique to the RF algorithm is the feature importance module, which allowed us to confirm that the 'spend' column was the most important to predict on leads. Although we have scaled back to only four features here, we have considered expanding to a larger list of columns and checking the importance matrix again! 
Here is the output for "importance": 
![image](https://user-images.githubusercontent.com/102266450/189550053-05a3ba42-95f1-499f-838e-7698c4d780c7.png)

### Accuracy:
#### NN Model:
Lastly, we created a dictionary and displayed a dataframe to hold the state, accuracy, and tier designation accordingly: 
![image](https://user-images.githubusercontent.com/102266450/189550074-c1b0db0b-37b3-4de6-9549-0bfdeee91470.png)

In terms of results, we found a variance of results for state tiers and model accuracies. Although our lowest model accuracy was 74% for the state of NJ and NC; our highest accuracy came from KY, at 98%.

#### RF Model: 
Here are is the classification report (only state of KY as an example), followed by our results dataframe: 
![image](https://user-images.githubusercontent.com/102266450/189550098-3669d165-4e36-4403-aa05-5b56f1110d18.png)

#### SVM Model: 
Although we have largely not tracked the process with our SVM model, we thought it relevant to at least display the following accuracy outputs:
![image](https://user-images.githubusercontent.com/102266450/189550121-f3d796b8-fc96-4b4c-ba33-6162e551c65c.png)

### Making Sense of the Accuracy: 
Although the results dataframe displayed accuracies by state and tier, we wanted to dig deeper into what these numbers meant. We leveraged tableau to create the bottom two visuals. Please note, we replicated the visuals for brand 1, neural network against the SVM and RF outputs: 
![image](https://user-images.githubusercontent.com/102266450/189550144-32721b34-d644-4030-83ea-2084a834039f.png)

The accuracy reports between the three are nearly identical by state, with only a +-1% (more on this later). In terms of selecting models to run, we recommend random forest as it includes the feature importance code and runs faster than both the SVM and NN models. 

### Dashboard 1: Quick View
![image](https://user-images.githubusercontent.com/102266450/189550173-0b08ab54-a949-4c59-a0e1-6afcf287c273.png)
In this first view, we can see each model mapped on the bottom axis, with their respective accuracy by state. Although this is only sampling one state by tier, in practice we explored nearly three states/tier. We found our accuracies to be consistent, showing only a percentage change by model of +-1%. 

### Dashboard 2: State Heatmap
Although the above chart shows little variance in model accuracy, we then decided do a heatmap.
Here we are displaying the neural network sampling of states and tiers: 
![image](https://user-images.githubusercontent.com/102266450/189550215-825b6c57-abf2-4428-bb9c-9d42088e1898.png)

We did the same process for SVM and RF, but found no meaninful changes/differences. 
However, we did find an odd irregularity in the tier 1 designation of California versus the state of Ohio. Both of these states contained 7000+ datapoints (each datapoint being one campaign ad). 

Yet, we see that the CA only hit about 78-79% predictive accuracy versus OH's 91-93% accuracy. We attribute this to external factors on demographics, seasonality, and more directly, a possible need to adjust the weight of importance for each feature. 

### Dashboard 3: Boxplot
As a result, we moved away from the heatmap visual to a boxplot chart to check on our tier's average model accuracy: 
![image](https://user-images.githubusercontent.com/102266450/189550204-e1cd7636-b65a-4392-9843-de0e8ed740f8.png)
We see less variance in tiers 3 and 4, but hold reservations on the amount of data/campaign ads ran. How appropriate is to compare tier 4 states (less than 1000 ads) to tier 1 (<7000 ads)?

If we accept that tier 4 has enough data, then we can confidently recommend that due to its lower amount of variance from the lowest and highest performing states, it is optimal to include this in our model accuracies. 

Again, a quick clarification on what this model truly indicates: leads predicted, to a certain % accuracy from a set of features including spend, clicks, and impressions. 

A more appropriate next time would be to move away from the binary classifcation modeling of yes or no success on leads, towards a seasonality or ROI by date model such as ARIMA (Autoregressive integrated moving average). 

Time-permitting, this would serve to then observe once again by state and their respective tier (amount of ads/bin) against the "date start" column. We do however recommend more than the given sample of data, as it only held one-full calendar year of ad results. In the ARIMA construction, we would once again reduce the data by brand, and likely predict the amount of leads as a user inputs a mix of impressions, clicks, and dollars spent. 

This is by no means an attempt to dismiss our results, but we feel that the binary classifcation models above can only go so far, without then accounting for time-series predictions! 

Once again, here is quick snapshot of the accuracies dataframes---
NN Results: 
![image](https://user-images.githubusercontent.com/102266450/189550257-180f6814-bcff-47a6-8867-d179cc943e3d.png)

SVM Results: 
![image](https://user-images.githubusercontent.com/102266450/189550246-40d48035-5513-4ffc-87b8-a788d9b360f5.png)

RF Results: 
![image](https://user-images.githubusercontent.com/102266450/189550253-184c972c-3d0e-475a-aade-1616e14ec3d0.png)

In order, NN, RF, and SVM when compared on overlaping states: 
![image](https://user-images.githubusercontent.com/102266450/189550237-fe9a7fbb-56a8-498c-aaff-876569d1b19a.png)
