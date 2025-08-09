# <p align="center"> Country Happiness Predictor
> Break Through Tech AI Final Project - Summer 2025

## Project Goal
This project aims to predict how 'happy' a country would be based on their citizens' perceptions of their national government. In order to predict such, I implemented, trained, and tested two different AI models in Python: Logistic Regression and Random Forest models. The dataset that was used to train the models on is the World Happiness Report from 2018, which has a record of countries, their level of happiness based on a score on the Life Ladder, and other relevant attributes that can affect a person's happiness, including social support, confidence in the national government, and average household income, from 2008 to 2017. The Life Ladder is a way to measure how happy someone is by them scoring their life on a scale of 1 to 10, where scoring 10 means they have the best possible life while scoring 1 means they have the worst possible life.  

## Project Importance
Analyzing these results reveals how public opinion of the government influences national happiness. Governments, policy-makers, or international organizations could use these models to identify key governance areas, such as corruption or trust, to improve in order to boost overall well-being. This could lead to more targeted policy interventions, better governance outcomes, and greater citizen satisfaction. 

## Data Preparation
From the dataset, I isolated a small number of features relevant to my project: 'Perceptions of corruption', 'Confidence in national government', 'Democratic Quality', and 'Delivery Quality.' I chose those four features because all directly related to how a country's people viewed their national goverment. To clarify, 'Delivery Quality' is how well a government fulfills their promises to the people. I chose not to include the country as a feature because I did not want the model to generate biases on different countries and their happiness; I only wanted the model to focus on government perception, regardless of where that country is from. 

The label is the score of the Life Lader, which represents the country's happiness. When creating a new dataset with just the features from above, I added a binary indicator of whether the country was happy or not by having a certain minimum score. If the score was at least a 6.0, the country would be considered happy and be given a "1"; otherwise, the country would be given a "0." 

I then checked for any missing values, which resulted in 330 examples with missing values. I thought this was a small amount as the entire dataset had 1562 examples. Thus, I simply removed any examples with missing values. I did not check for outliers because the values may drastically differ per country (the examples were grouped by country even without having the country mentioned in the dataset). 

To ensure that the features would provide good predictability for the label, I checked the correlation between the features and the labels. A strong correlation score is closer to -1 or 1. All of the features except 'Confidence in national government' had a moderately strong score at around -0.5 or 0.5. 'Confidence in national government' had a correlation score of -0.04. However, after visualizing the correlations with a Seaborn pairplot, there is a noticeable trend where lower values of the features lead to lower values of happiness. In order words, the more negatively perceived a government is, the less happy the country is. 

![Seaborn pairplot of correlation](https://github.com/angeleanne-enriquez/BTTAI-CountryHappinessPredictor/blob/main/Correlation.png)

## Model Approach
I chose two AI models to train and test: Logistic Regression and Random Forest. Logistic Regression is a linear model that allows me to better interpret how each feature affects the predictability of the label and work better for small datasets, like this one, which only has 1232 examples. I thought it would also suit the features well due to their moderately strong correlation with the label. On the other hand, Random Forest is a set of Decision Tree models that samples n examples randomly with replacement, fits a decision tree with that data, and adds that tree to the ensemble. While this model takes more time to train and is more difficult to interpret than Logistic Regression, it typically has a higher accuracy and can handle nonlinear relationships better than Logistic Regression. 

I used grid search on different values for the hyperparameters (n-estimators and max depth) to find which ones gave the best predictions. To evaluate how accurate these models are, I will compare their accuracy scores and cross validation scores.

## Results
After training and comparing the two models, the Random Forest model had a higher accuracy score of 0.8796068796068796 compared to the Logistic Regression's model's accuracy score of 0.8378378378378378. However, the Logistic Regression model had a higher cross validation score of 0.820624732563115 while the Random Forest model had a score of 0.7889700799842008. Accuracy and cross validation scores both indicate how well the model performed on test data. However, cross validation is more accurate in how well a model can generalize to new, unseeen data because it evaluates performance over multiple folds of tze data. Because the Logistic Regression model had a more consistent performance across the folds, it may be less prone to overfitting and more robust overall, even if its test accuracy was slightly lower. 

## Future Considerations and Challenges 
I should have explored my data more thoroughly before only using those four features. Although they were the only features that were directly relevant to this project's goal, there may have been other features that could have improved the model's accuracy. 

I was naive to think that eliminating 330 examples from a 1562-example dataset would not be a problem. Although I thought that was only a small portion of the dataset, that is actually 21% of the data gone. Instead of removing the examples with the missing values, it would have been wiser to fill them in with a mean or median. The challenge with this is being able to replace the missing values with the country's mean, not the entire dataset's mean of that feature, because the values can drastically differ across countries. 

I also failed to address class imbalances in my dataset, which can have a negative impact on my model's predictability. Next time, I could have either downsamples or upsampled my dataset to ensure that there is an even amount of positive and negative cases for the model to train from. 

While the model's predictability was decent, it most definitely could have been better with these revisions. 
