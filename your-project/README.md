<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Title of My Project
*[Alex Navarro Llecha]*

*[Data October 2019, Barcelona & 19/12/19]*

## Content
- [Project Description](#project-description)
- [Hypotheses / Questions](#hypotheses-questions)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Analysis](#analysis)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Workflow](#workflow)
- [Organization](#organization)
- [Links](#links)

## Project Description
The main objective of this project is to analyze the prediction of 16 different locations in the USA by the waste of energy buildings have in it and help company to identify the best location where the sample of buildings waste the less. We first look for the 4 different types of energy is use in the building of our dataset, and then make a ML to predict the future waste in the next year and decide which one is the perfect one.
The main objective 

## Hypotheses / Questions
The main question is: which is the location I would recommend to have the new facilities for any company, taking into account the energy consumption in the locations during one year.

A company is thinking about making/building some new offices for the next expansion they would have and they need to take care of the waste of energy it could have for the future. The ask to a consultant about different locations.istical/data languages (i.e. define Null and Alternative Hypothesis). You can use formulas if you want but that is not required.

## Dataset
Association about energy efficiency  where they give 5 different dataset: one is the train with the different building of the sample with the energy consumption metric and timestamp for each hour of each day in 2016. The second one is a weather dataset where we found the different location, called site_id, with their proper features as Tº, Wind, etc. The third dataset is the metadata where we find the link from the train table and the weather, and also we have the types of buildings we found, if they are for education, offices and more others. 
The other 2 tables are for the test of the competition, which they are not going to be used in this case.

The size of the files are around 2GB, the three tables, which it make quite difficult to manage them in the git hub. And I had to create a clean data without nan values and reducing the size of the files, but the size of the new dataset for the prediction is 600MB, so there is still a problem with the size.


## Cleaning
For the data clean, I start looking the Train table, which did not have nan values at all. It does have some row the full data, 20 M +. As the main objective was to get a dataframe to make able the prediction model. 

I decide to see the next table which is the metadata. In this table their two columns which are not very necessary which are the building floor and the year_built. I decide to drop the building floor because it has more than 75% of missing values and the other one only 45% but it nice for analyzing later if the year have something to do with the waste of energy. In the primary_use I decide to change the category by grouping the different labels inside of it, only the one with less than 100 counts, and end by having only 6 types of primary_use, when it used to have 15.

Then I jump to the weather table. In this dataset,  the wind columns, one with the power and the other one the direction. I decided to drop the wind direction as the main goal is to use the time series to predict the consumption in the next year. The main columns would be the site_id, to making able the classification and the temperature and the dew_temperature ( possibility of raining) are quite nice to see their performance.
 
After seeing the type and the nan values of each table I start merging the train and the metadata with the building_id and then this dataframe with the weather one with the site_id and the timestamp for having all the possible hours of all the registration of consumption.

Because the prediction model works with time series, I change the timestamp to datetime and create new features as day and month and create a label encoder for the prediction method in the primary_use feature. 



## Analysis
In the analyze part, I decide to have a look in the four different types of energy are used in the datasets. However, I start by looking the general counts of the four of them and we can see the electricity as the main one have 3x more information than the other 3 ( hot water, chilled water and steam). But in what concerns the total sum of the variable, the steam is the one which consumes more of the four, 4 or 5x por than the other, and the electricity being the third one. 

Looking inside each one, we can see that steam and hot water are many use in the winter season where is cold outside and people can not work freezing. The main thing we see about the electricity is the high consumption in summer where the A/C are working at full power, which is something normal and the chilled water is also in summer. However, the level of waste are not the same in both energy, chilled water over pass the electricity with a mean of 1500 in summer, when electricity is in 190. This difference is quite high. The hot water stays at a level of 700 Kwh consumption in the winter season and the steam with 50,000 in the winter season. We can observe the most troubling energy is the steam which has a general consumption of 25,000 in all the year. 
In the boxplot, we can see the same tendency of the different energies o the dataset.

Concerns the primary_use, we can see the education sector as the one with more consumption between the 6 categories we have, follow by entertainment and then the other. This two have an average of 10,000 and 1200. The first one has like 10x more than the second one, this is maybe cause by the fact that schools use steam for heating the building and has a lot of access from outside where the cold come inside the building, so they keep it working all the time. The  residencies, offices, public services buildings and others have an average of 600 Kwh per day approximately, as we can see in the graph from the exploring file. 

You can see the charts in the Data cleaning and exploration file.



## Model Training and Evaluation
For the model i used, prophet. A model which pedicts with time series along the year, month, day and hour variables of the time serie. However, the model has to receive two main input to work and to the forecast for the next year. So I create a dataset with the energy readings of each hour of the year for the different locations in the datasets and start forecating for each of it to see the tendencies they have for the future.

As a result, many of them have a positive tendency for the next year except few of them, which some of those do have a important drop which was not normal at all. The only location having a normal negative tendency was the location nº 10 which even the trend for the week and day has sense. The weekly was only the weekends as the day with proper consumption and during the dayly, the pic time was at 1 pm which is a reasonable hour where everyone is working.


## Conclusion

As the locations where a mix of the different buildings from the datasets and the data was from just 1 year history, we can not predict properly if the location nº10 is the best one to build the new offices. Also, by having a look in the different locations some of them have extrem consumption results.


## Future Work
For future steps, i would like to came to a solution in the management of big datasets for the git hub repositories. Also, try to manage a model to predict the future consumption of the buildings in it self with the features they have, as the Kaggle competition from ASHRAE ask. 

## Workflow
The main steps were: find the Idea, look for the datasets. In this case, the dataset were profide with the concept of the Kaggle competition. Clean any problem inside the datasets and make a proper exploration of it. Look for a model with can predict the future values of the different locations. Use the model to predict the locations and find the best one with a proper future of less consumption and with the other locations decide if the model use in this case was the best one or not.  

## Organization
I did use a Trello for the organizing of the project which you can check the steps I follow for making the project. The main steps for each of the labels in it are inside the file in the repositary.

The repositary has one main folder with the project, and inside there are two folders for the datasets, one with the old dataset and the other one with the dataset por the Machine Learing / Prediction of the model.
Then you have, also two file: one has the Data Cleaning and Exploratory part of the project and the other one has the Model for the different location that has the dataset. 

## Links
Include links to your repository, slides and trello/kanban board. Feel free to include any other links associated with your project.


[Repository](https://github.com/AlexNavarroLlecha/Project-Week-8-Final-Project)  
[Slides](https://docs.google.com/presentation/d/14Sdv2nX0lLluphEywgnwB5PY5I_G9iPuzTmA1CZ5QkI/edit?folder=0AKSpoc8F217bUk9PVA#slide=id.g6cb0f89482_0_697)  
[Trello](https://trello.com/b/ZRl9Dqoo/final-project-alex-navarro)  
