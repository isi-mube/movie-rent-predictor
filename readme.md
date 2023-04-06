# MovieRent Predictor

<p align="center">
  <img src="https://i.postimg.cc/q7RTS9DF/230295258-7abb4af1-36f4-489c-a99b-62d2dbaa99a2.png">
</p>

1. [SQL script](https://github.com/isi-mube/movie-rent-predictor/blob/main/notebook/00_sql_database_extraction_process.sql)
2. [Python script](https://github.com/isi-mube/movie-rent-predictor/blob/main/notebook/01_logistic_regression_v2.ipynb)

## About the Project
The objective of this **project** is to determine the probability of a movie to being rented again based on a collection of over **one-year** historical data (from 2005/05/24 to 2006/02/14).

This reposatory is build upon [my previous knowledge in Linear Regression](https://github.com/isi-mube/mbappe-project), to do a Logistic Regression model for predictive analysis.

## About the Dataset
For a complete description of the dataset extraction process, please refer to the [SQL script](https://github.com/isi-mube/movie-rent-predictor/blob/main/notebook/sql_database_extraction_process.sql).
Also, to read all documentation regarding `feture` selection and creating the `target` refer to the [Python script](https://github.com/isi-mube/movie-rent-predictor/blob/main/notebook/imb_solution_lab_logistic_regression.ipynb).


## Improvements from previous project
* **Organization**: We have two separate scripts for SQL and Python.
* **SQL**: Not my strongest point. For this project, it was important to decide whether RIGHT, LEFT or INNER JOIN to not loose data.
* **Entropy-Bonus**: We fixed a GitHub formatting issue that displayed code horizontally due to HTML boxes.

## Changes (28/03/23)
* **Structure**: Small changes for a better structure.
* **Libraries**: We reduced the number.
* **Roc curve plot**: Up2date. Ty, [Nati](https://github.com/natnaelfe)!.
* **LEFT JOIN**: Fixed. We use an INNER JOIN instead. It made no sense to extract films with 0 rentals.
* **Treshold**: Last time was defined by the mean. Now it's by the median since our target `movie_demand` has a different distribution.
* **Normalization**: This time we will normalize numericals with StandScaler.
* **Encoding**: Get dummies instead of LabelEncoder.
* **Results**: Better accuaracy (99% compared to our previous 92%) and confussion matrix results.

## Changes (06/04/2023)
* **SQL**: Small changes.
* **Python**: We used color headers, inspired by [Nara](https://github.com/ainaraguerraf).
* **Functions**: Imported from a library.
* **Documentation**: Small changes, also added a table with each column and it's description in step 01. Inspired by [Luis](https://github.com/lj90pot).
* **Encoding numericals**: Current knowledge. We did an extra ordinal encoding (again, ty [Luis](https://github.com/lj90pot)) to ratings and we cleaned some numericals.
* **NaN's**: We got many after creating each dataset. To solve it we reseted the index in some cases and in others we did fillna.
* **Metrics**: Added. Before we did not know how to read the results appart from accuracy. Now we added recall, precision, f1-score, macro avg and weighted avg

## Model Results

### Roc curve:
![image](https://user-images.githubusercontent.com/90038586/230299599-57e7fbf5-047f-4b32-92b9-edea9208b5d4.png)


### Confussion matrix:
![image](https://user-images.githubusercontent.com/90038586/230299778-7c36a27f-85c2-4472-b79a-defa83e429be.png)


Our model has:

* 99 **True Negatives** Vs 39 False Positive
* & 88 **True Positives** Vs 31 False Negatives
* The model is slightly better predicting True Negatives rather than positives. 
* Our precision is balanced in both low (0) or high demand (1) and recall has a higher score for low demand movies.

## Comparision with previous attemp (unrealistic)

![image](https://user-images.githubusercontent.com/90038586/230300706-0ddde30e-9687-4b3c-a2b6-4e6b91c280ac.png)


## Testing the Model

### Top 15 movie rentals
![image](https://user-images.githubusercontent.com/90038586/230303226-ce70d383-e3d7-42a7-be24-ca4cf36ed4b2.png)

So, for example, **film_id** `1000` is a movie with high demand, and we should keep more copies to our inventory. 

To find a name of the film, we simply do `SELECT * FROM film WHERE film_id = 1000`  in SQL or Python. 

In this case, `1000` corresponds to `ZORRO ARK`.

### Less rented film
![image](https://user-images.githubusercontent.com/90038586/230303154-615c0e2f-009c-439c-9aca-a00269a8de62.png)

And, **film_id** `400` had been rented 4 times during 2005/05/24 and it's not expected to be in demanand. Again, to get the name of the film; `SELECT * FROM film WHERE film_id = 400`:

In this case, `400` corresponds to `HARDLY ROBBERS`.


## Tools
**Enviornments**
* JupyterLab (mostly) & JupyterNotebook

**Libraries**
* **Data manipulation:** pandas
* **Numerical operations:** numpy
* **Enhanced EDA:** ydata profiling
* **Visualization:** matplotlib, seaborn
* **Settings:** warnings
* **SQL connection:** getpass, create_engine
* **Machine Learning:** scikit-learn
* **Skewness:** skew
* **Preprocessing:** StandScaler
* **Model selection:** train test split
* **Logistic model:** LogisticRegression
* **Metrics evaluation:** roc curve, confusion matrix & classification report
* **Confussion Displayer:** ConfusionMatrixDisplay
