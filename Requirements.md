This Assignment assesses the following module Learning Outcomes (from Definitive Module Document): 

Be able to demonstrate conceptual understanding of how established techniques of research are used to create and extend existing knowledge in data science. 

Be able to demonstrate originality in proposing alternative solutions to problems within a chosen area. 

Critically evaluate research literature and identify research problems to solve. 

Demonstrate ability to propose alternative approaches for future work in a chosen area. 

Communicate research knowledge effectively in a scholarly manner. 

In this assignment, we will conduct a case study: modelling some real time-series data - German electricity demand - with a variety of models, then make a forecast into the future. 

There are python scripts in the  Assignment Supplementary Information section, which will be useful starting places for acquiring the data and building your modelling workflow. 

The assignment is split into these parts; 

Download and prepare the data, initial time series plots. 

Model and forecast weekly data with several benchmark models. 

Model and forecast weekly data a SARIMA model. 

Add Temperature data to help improve the modelling and forecast 

Model and forecast weekly data a feature-based model. 

Using hourly data - build an LSTM to model and forecast. 

Answer several questions about the analysis. 

Write a 6-8 page report describing the analysis. 

Maintain and document code pipelines in a github repository. 

Assignment Tasks: 

Part 1: 

## Retrieve the data: 

We will be using the publicly available data from here: 

https://data.open-power-system-data.org/time_series/. This contains data from many countries up to October 2020. We are interested in the German data, which is known by it's country identifier 'DE'. 

Download the 60 minute data file: https://data.open-power-system-data.org/time_series/2020-1006/time_series_60min_singleindex.csv 

You will need to bin the data up using e.g. Pandas, to weekly and daily values. 

Keep only values from January 1st 2015 until the end of the file, October 2020. 

Make initial plots of the data and perform any EDA 

Identify what components there are in the time series. Is there and seasonal component? 

Perform all the time series analysis tasks to test for non-stationarity 

Part 2: 

Model with a range of benchmark models that have been discussed in lecture 1. 

For example: Mean, Naive, Seasonal naive and Drift forecasts. 

Use a 2 year forecast horizon. (see my example plot). 

Part 3: 

Define an autoregressive model: use SARIMA if you believe there to be a seasonal component (hint, use the statsmodel package). 

Find the best model parameters: p,d,q(P,D<Q) using the AIC likelihood method discussed in class. You must loop over all possible parameter combinations for p=[0,6], d=[0,2] and q=[0,6] 

Assess the model fit by inspecting the data-model residuals - i.e making another ACF plot on the model residuals and also inspecting the distribution of the residuals. 

Forecast the last 2 years of the available data. 

Test model performance predictions using e.g. rmse. 

Add confidence intervals on forecasts 

Part 4: 

Add in an additional weekly variable of Temperature to be used as an exogenous variable to make an 'explanatory' or 'conditional' forecast. This can be retrieved from https://archive-api.openmeteo.com/v1/archive 

Use Berlin as a representative location for German temperature. The file "A1_temperature_features" will help you here. Temperature features are not known in advance unless they come from a weather forecast. If we use observed future temperature in the test set, this should be described as an explanatory or conditional forecast rather than a true operational forecast 

Add this variable to make the SARIMAX forecast and model and make a weekly forecast. hint: the file 'A1_exogenous_regressors' will show you how these can be added to the model so that we now have the 'X' in SARIMAX model. 

## Part 5: 

Model the weekly electricity load and temperature data with a feature-based regression model. For example, Random Forest or Gradient Boosting Regressor. Forecast the last 2 years of the avalailable data. 

## Part 6: 

Using hourly data, use and LSTM to model and forecast the data. Conduct literature review around the use of LSTM for this task Build model and hypertune the parameters and layer design Forecast the last 2 years of the available data. Compute appropriate evaluation metrics 

## Part 7: 

Answer these questions about the analysis. The answers must be included in the report. 

Compare all models against the seasonal naive benchmark. Which models, if any, provide a meaningful improvement? 

Explain how you avoided data leakage when creating temperature lag features. 

For the SARIMAX model, justify the chosen differencing orders and seasonal period. 

Evaluate whether temperature and holiday covariates improve forecast accuracy. Are these covariates known at the forecast origin? 

Compare the interpretability and complexity of SARIMAX, feature-based,  and neural network models. 

Recommend one model for operational use and justify your choice using accuracy, uncertainty, interpretability, and maintenance considerations. 

Part 8: 

Write a 6-8 page report describing the modelling, forecasts and inferences. This includes figures and references. References should be no more than 0.5 pages 

Include plots of all the model forecasts 

Include a table of the evaluation metrics used to compare the different models 

An essential element to scoring high marks in this assignment is a critical analysis of your work and results. You should not merely state your numerical results. 

Instead, make sure to discuss why the results are as they are based on your code and model. Think about the motivation behind your choices and how they may have affected the results. 

Comment on how the forecasts compare to the real data collected after the modelling/forecasted part. 

To convey this, construct a narrative of your analysis including images, plots and summary statistics. Discuss future improvements that could be made to this analysis. Cite papers where appropriate. 

Part 9: 

Build a github repository for the codebase 

Follow best coding practices 

Follow Readme.md example in Assignment Supplementary Information. 

Submission Requirements: 

Report: a pdf or word doc only. In the report, describe what analysis steps you have done, why you have taken the approach you have and what you have interpreted. You must also give brief descriptions of the models used and include references. 

Code: you can submit the code as an additional file or you can share a link to a colab or github repository. If we can not access the code you may lose marks in the code section. The code must include all the figures, modelling and numerical values presented in the report. It must also run when we test it. 

Submissions will go through Turnitin. You will have two submission attempts. 

Marks awarded for: 

1. Code submission: (60%) 

Completion of the modelling and forecasting task (50%) 

The final plot of all the modelling and forecasts are presented 

Completion of the modelling tasks 

Performing all the tests for Stationarity (e.g. ADF, ACF, PACF, differencing) 

Code quality and annotation (10%) 

Follow github repository style 

Developing functions to complete parts of the coding problems 

Annotating your code so that another user can understand it 

2. Report (6-8 pages): (40%) 

Discussion of the analysis and inferences (30%) 

A brief overview of the method(s) 

Why are these particular ML methods used 

Do not just give me a textbook definition of the method/statistic 

Describe the results (hint use figures, evaluation metrics) 

Compare the methods used 

Quality of the report writing - (10%) 

How well does the document flow and how easy is it to follow the review and analysis presented The document is correctly formatted 

Figures are used appropriately – axis labels are readable. 

The appropriate references are used throughout 

Is the correct scientific english language used throughout 

Type of Feedback to be given for this assignment: 

Written feedback on report and code, following rubric breakdown. 

Additional information: 

Please familiarise yourself with regulations governing assessment offences including Plagiarism and Collusion (UPR AS14). 

Engage with guidance for avoiding plagiarism via the University SkillUp module and 1-2-1 sessions with our specialist SASH team. 

For undergraduate modules: 

a score of 40% or above represents a pass performance at honours level. 

late submission of any item of coursework for each day or part thereof (or for hard copy submission only, working day or part thereof) for up to five days after the published deadline, coursework relating to modules at Levels 0, 4, 5, 6 submitted late (including deferred coursework, but with the exception of referred coursework), will have the numeric grade reduced by 10 grade points until or unless the numeric grade reaches or is 40. Where the numeric grade awarded for the assessment is less than 40, no lateness penalty will be applied. 

For postgraduate modules: 

a score of 50% or above represents a pass mark. 

late submission of any item of coursework for each day or part thereof (or for hard copy submission only, working day or part thereof) for up to five days after the published deadline, coursework relating to modules at Level 7 submitted late (including deferred coursework, but with the exception of referred coursework), will have the numeric grade reduced by 10 grade points until or unless the numeric grade reaches or is 50. Where the numeric grade awarded for the assessment is less than 50, no lateness penalty will be applied. 

