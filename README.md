# Ames Housing Prediction

The project looks at a dataset containing information from the Ames Assessor’s Office used in computing assessed values for individual residential properties sold in Ames, IA from 2006 to 2010 and tries to predict with minimal error the values based on the features provided.

## Getting Started

Detailed info located here: http://ww2.amstat.org/publications/jse/v19n3/decock.pdf

[The data can be found here](https://github.com/jjaniuk/ames_housing_prediction/blob/master/AmesHousing.csv)

[Detailed info on the dataset](https://github.com/jjaniuk/ames_housing_prediction/blob/master/AmesHousing.txt)

### Prerequisites

If you decide to fork the repo, you will have to make sure to have Python 3.6 installed, with jupyter notebook (reccomended) and the required modules that are used within this notebook.

You will need the below modules
```
Pandas
Numpy
seaborn
matplotlib
scipy
scikit-learn
```

## Authors

* **Jakub Janiuk** - *Initial work* - [jjaniuk](https://github.com/jjaniuk)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Background

Detailed info located here: http://ww2.amstat.org/publications/jse/v19n3/decock.pdf

This project looks at a housing dataset (2930 observations and 82 variables which includes 23 nominal, 23 ordinal, 14 discrete, and 20 continuous variables)

The goal is to predict the price of a house given the large range of variables.

## Data Exploration

The first thing that needs to be done is we should explore the dataset to make sure that we are dealing with a "clean" dataset without too much outliers and without many missing values.

As we look into the dataset we find out that there is a few outliers (very expensive houses and cheaper houses w.r.t. the grade (ground) living area)

We remove any of the datapoints with grade living area of 4000 square feet.

## Missing data / Handling missing data

We need to look at the missing data. From a quick check we can see that there is missing data in 27 variables. Rather than removing these variables, we will try to either fill these based on the [detailed file about the dataset](https://github.com/jjaniuk/ames_housing_prediction/blob/master/AmesHousing.txt), or use [imputation](https://en.wikipedia.org/wiki/Imputation_(statistics)).

Taking some time looking in the detailed dataset file, we can see that we can fill the missing values as most of them as missing due to values like "none", "missing".

## Feature Engineering

Before we do any modeling, we need to look at feature engineering. Better features means more flexibility, simpler models, and better results. This will allow us to spend less time or no time on tweaking our machine learning model coefficients and also will allow us to avoid overfitting to a greater degree.

We focus on 3 differnt types of feature engineering:
1. Simplifying exsiting features, like months into seasons, overall quality rating 1-10 to simplified overall quality of 1-3 etc.
2. Combinations of exsiting features like total area, house area etc.
3. Power transformations (squares, cubes and square roots)

## Modeling

We try applying three different types of algorithms, starting from the simplest, [linear regression model](https://en.wikipedia.org/wiki/Linear_regression), a [ridge regression model](https://en.wikipedia.org/wiki/Tikhonov_regularization), and a [lasso regression model](https://en.wikipedia.org/wiki/Lasso_(statistics)), and we compare the differences in results.

### Linear Regression Model
This model performs  without some of the engineered features. Once we take out the cubed and square root features our simplest model gives us a decent Root Mean Squared Logarithmic Error (RMSLE) of 0.1255 on the training set,
and 0.2207 on the test set.

Side note: RMSLE is simply the ratio between the actual and predicted values. In this case it's the price values of the houses. 

## Ridge Regression
Using the ridge regression we can add more complex power transform features (cubes, logs and square root). With those features we see a nice improvement from our simple model to 0.1206 on the training set and 0.1103 and the test set.

## Lasso Regression
The lasso regression model gives us even a better RMSLE of 0.1197 on the training set and 0.1084 on the test set.