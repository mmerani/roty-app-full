# Predicting the NBA Rookie of the Year using Machine Learning

This project uses several Regression algorithms to predict the 2020 NBA rookie of the year. 

Tools Used: Python, Flask, SKLearn, Jupyter Notebooks, Conda, ReactJS, Visual Studio code, Git, Github, Heroku

3 major components:
1. Data mining, analysis, and building models
2. Create the backend service
3. Building frontend UI

## Data Mining, analysis and models

The first step was finding a suitable dataset. I decided to web scrape a site called basketball-refence who provides data on all the rookie of the year votings dating back to 1956. However for the purpose of this project I decided to use only data from 1979-present, which consisted of 230 players.

### The data set

As I mentioned, I webscraped data from basketball-reference which gave me a data set of 230 players dating back to 1979. Using this data I picked out the features that had the best correlation to the target value, which in this case was award share. Players with the highest award share were the winners of the rookie of the year award. After features were selected, I preprocessed the data by filling null values and scaling the features that I was going to use to build the models.

### Building the models

After the data was preprocessed, I seperated the data for training and testing. In this case, I used all data from dates 1979-2018 for my training data and last years (2018-2019) voting data for validation. I built 5 different models that I have recently studied (Linear Regression, Gradient Descent, Ridge Regression, Lasso Regression, Elastic Net). After tweaking the models, the best accuracy I could find was with Lasso and Ridge regression both with a 80% accuracy. All of the models predicted the winner correctly. However, the rankings after that differed from model to model. After I was satisfied with my models, I packaged them and saved them to a local file using joblib so I could use them in the following step.

## Creating the backend

After building the models, the next step for me was to build the backend service. First, I needed up to date data on this years rookies. Again I used basketball-reference to scrape data. Then narrowed my data set for rookies that have only played 500+ minutes. This way I only apply the models to players with significant amounts of data. Once I have this data I apply the models to them and save the top 5 results (in order) for each in a json file. Since the data set and scale of this project is so small I decided to just save a json file with the data instead of setting up a database. The json file will be a faux database of sorts for the next step in the process. 


### Flask and Rest

Next I built the service for the app. This is what is called by the frontend to populate UI features. The service is built in Python using the Flask library. Depending on the model requested by the frontend pull RESTful request, the service retrieves the data from the json file and returns a dictionary with an array of players and their team names for that specific regression model. 

![web](https://github.com/mmerani/roty-app-full/blob/master/images/service.JPG)
![web](https://github.com/mmerani/roty-app-full/blob/master/images/response_example.JPG)


## Building the frontend

Before this project I had no expereince in ReactJS. Using the ReactJS tutorials provided online I was able to build out a simple UI which included a table and a drop down. Although these are simple features, I wanted them to have some specific functionality. On page load the app automatically makes a pull request to my backend to retreive the first model on the drop down menu and popluates the table. Which in this case is Linear Regression. On each click of the drop menu, a pull request is made to retrieve the data for that model listed and the table updates. 


![web](https://github.com/mmerani/roty-app-full/blob/master/images/test_app.JPG)

## Conclusion
My predictions are consistent with what the majority of the basketball world believes: Ja Morant will win the 2020 rookie of the year. Not only did my models predict the winner, but it is also said that Kendrick Nunn will be a close second in the race. Now that number 1 overall pick and pre-season favorite to win the award, Zion Williamson, has begun to play in games, it will be interesting to see how this prediction changes in the coming months. 

When all the components were completed I deployed the UI and service to Github and Heroku where the app is live now

link: https://roty-prediction-app.herokuapp.com/

![web](https://github.com/mmerani/roty-app-full/blob/master/images/live_app.JPG)


## Next Steps
- Figure out deployed app slow load bug. 
- Add more Machine Learning algorithms to the project. 
- Include MVP predictions.
- Include more advanced player data for models. 
- Schedule Heroku to run script to update rookie data daily.