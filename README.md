# Impact_Orange

## Overview
What makes one country happier than another? What factors around the world have the highest correlation to a country's happiness? A country's happines is calculated using 6 standard factors along with an additional factor - Dystopia Residual to create one happiness score. From initial analysis the main contributing factor to happiness is the Dystopia Residual. The Dsytopia Residual is a number left over from the normalization of variables that cannot be explained. The main focus of this project is to determine what external factor(s) make up the Dystopia Residual score. Analysis of population density, infant mortality rates, suicide rates, unemployment, and yearly precipitation against the top and bottom scoring countries will help determine whether or not these factors contribute to happiness. 

### Questions to Answer
- Who are the top 5 and bottom 5 happiest countries?
- What are the top 3 factors that contribute to the happiest countries?
- What other factors are related to world happiness score? (Suicide rates, infant mortality, average precipitation, unemployment rates)
- How does the U.S. compare?
- What other areas do the happiest countries excel in as well?
- As a member of the U.S. government, what world happiness factors do I need to improve so I can have a happier country?

## Datasets
2021 Wold Happiness - [2021 World Happiness](https://www.kaggle.com/ajaypalsinghlo/world-happiness-report-2021)

## Group Members
Rabbikul Islam, Taylor Downes, John Thomas, Avery Corniell

## Database
We have set up a database using AWS that is linked to PgAdmin. We are accessing the data from PgAdmin using SqlAlchmey in Python. 

## Presentation
[World Happiness Presentation](https://docs.google.com/presentation/d/1DQCJWWW_E6fGEbxMv9UcxUlvG9ovxFiaSAVMZq7xELc/edit#slide=id.g100744b09ef_0_29)

## Dashboard
[World Happiness Dashboard | Tableau](https://public.tableau.com/app/profile/john6384/viz/2021WorldHappinessMap/Dashboard1?publish=yes) 

## Data Vizualization
Create charts using Matplotlib (a few already created - see cleanup.ipynb)
Create maps using javascript leaflet. 

## Machine Learning - Linear Regression

- Resources:
    - World_Happiness_Machine_Learning.ipynb - initial model
    - Machine_Learning_Feature_Importance.ipynb - Includes the initial model and the feature importance process of dropping each feature and re-running the model.

### Data Preprocessing
- In order to get our data ready for testing, we connected and pulled our data through our database, dropped null data, and created boxplots for our data to determine and drop any outliers in the dataset.

### Feature Selection
- In order to select our features, we created a multicorrelation matrix to visualize the relationships between the different world happiness factors. Here we can see Log GDP per capita, Social Support, and Healthy Life Expectancy at Birth correlate the most to life ladder / world happiness.

![image](https://user-images.githubusercontent.com/84201614/141652400-912dcba4-1edc-4fb0-b2bd-11a7c34ae497.png)

- We also created scatter plots of the different world happiness factors to visualize the linearity between life ladder and the world happiness factors. Again, we see Log GDP per capita, Social Support and Healthy Life Expectancy at Birth having the strongest linear relationship to life ladder. Since we have a limited number of factors, we decided to keep all the happiness score factors as features in the model in our first round of testing.

![image](https://user-images.githubusercontent.com/84201614/141652668-bd9d7a4c-e3f8-4d11-96d3-7b1cc2729dea.png)


### Training and testing sets
- Features
    - Log GDP per Capita
    - Social Support
    - Healthy Life Expectancy at Birth
    - Freedom to Make Life Choices
    - Generosity
    - Perceptions of Corruption

- Target
    - Life Ladder


- Splitting data to training and testing sets:
![image](https://user-images.githubusercontent.com/84201614/141652789-a7ae4c1f-bdf2-41b6-b271-6e2d03fe2282.png)

- Predicted data:
![image](https://user-images.githubusercontent.com/84201614/141652815-5ea1e04f-95e9-4fc7-94c5-5a61be18374c.png)

- Results
    - R^2 Score = 0.6687
    
![image](https://user-images.githubusercontent.com/84201614/141652839-0c07504e-9853-4c5c-8840-1697469c46ca.png)

### Additional Training
- In order to see if we could improve our accuracy score of our linear regression model, we dropped each feature from the dataset and re-ran the model to test the relationship between the features and the accuracy of our model. 

![image](https://user-images.githubusercontent.com/84201614/141653033-f9e0e7ee-e629-414b-9be6-e07b49a436ab.png)

- We can see that when dropping social support from the dataset, the accuracy score drops the most by -0.004. This means social support is the most valuable feature to our model. Perceptions of corruption is the least impactful to our machine learning accuracy score, increasing the score by .02 when corruption was dropped.

## Machine Learning - Random Forest Regression
Random forest classifiers are a type of ensemble learning model that combines multiple smaller models into a more robust and accurate model. Random forest models use a number of weak learner algorithms (decision trees) and combine their output to make a final classification (or regression) decision. 

Steps taken:
- Imported data and created a dataframe for our features and target
- Split the data into training and testing sets
    - Training (75%)
    - Testing (25%)
- Calculated the average baseline error (3.81 for our data) to provide a goal for our model
- Use Random Forest Regression (1,000 decision trees to predict the data)
- Calculated the mean absolute percentage error and R^2 score
    - MAPE : 0.38 (beat our baseline!)
    - R^2 : 92.95% (beat our linear regression model!)
- After our initial model, we limited the depth of the tree to 3 levels and decision trees to 10 and used the top 3 features to see how that would impact the accuracy
    - R^2 decreased from 92.95% to 92.53%
- Determined feature importances:
    - The top 3 features appear to be the same as the linear regression model (GDP, Social Support, and Healthy life expectancy), however, the most important feature in this model was Healthy life expectancy as opposed to social support in our linear regression model.
    
![image](https://user-images.githubusercontent.com/84201614/141703121-b43450fb-2898-4736-aa02-2fd80a44059c.png)


