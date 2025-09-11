
# SpaceX Falcon 9 Landing Prediction: Data and ML

SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is because SpaceX can reuse the first stage. Therefore if we can determine if the first stage will land, we can determine the cost of a launch. This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.

This repository contains the notebooks, data and code for the IBM Data Science capstone project. The aim is to collect SpaceX launch data (SpaceX REST API and public sources), clean and explore it, create interactive visualizations (Folium maps and a Plotly Dash dashboard), and build classification models to predict first-stage landing success.

For any questions about this repository, please contact me via juan.fernandez.sea@gmail.com


---

## Step-by-step (lab-by-lab breakdown)

Below is a practical workflow you can follow — each step corresponds to a notebook or a script in the repo.

### 1. Project setup

* Initialize a Git repository and create a structured folder layout (`data/`, `notebooks/`, `dash/`, `models/`, `reports/`).
* Create a `requirements.txt` or `environment.yml` and a `README.md`.
* (Optional) Set up IBM Watson Studio / IBM Cloud project if you plan to use IBM-hosted notebooks.

### 2. Data collection

* Use the SpaceX REST API to GET launch data (JSON). Save raw JSON responses to `data/raw/`.
* Optionally scrape or copy relevant Wikipedia tables to get complementary fields (if needed).
* Convert / flatten JSON to a tabular CSV (e.g. `data/processed/spacex_raw.csv`).

### 3. Data wrangling & cleaning

* Filter to Falcon 9 launches if the exercise requires.
* Handle missing values (e.g., impute `PayloadMass` with mean or median).
* Normalize / rename fields to friendly column names (e.g., `Payload Mass (kg)` → `PayloadMassKg`).
* Create the target label `Class` or boolean `LandingSuccess`.
* Save cleaned dataset (e.g. `data/processed/spacex_clean.csv`).

### 4. Exploratory Data Analysis (EDA)

* Univariate: histograms of payload, flight counts by year.
* Bivariate: payload vs. landing success; flight number vs. success rate.
* Grouped: success rate per launch site, orbit, booster version.
* Use Pandas, Matplotlib / Plotly for interactive charts.

### 5. Geospatial visualizations (Folium)

* Map launch sites and landing sites using Folium markers.
* Add popup info and simple chloropleth or marker clusters where appropriate.
* Save maps as HTML for inclusion in the report or dashboard.

### 6. Interactive dashboard (Plotly Dash)

* Prepare `spacex_launch_dash.csv` as the dataset for the Dash app.
* Implement components: dropdown (launch site), range slider (payload), scatter/box charts, and callbacks to update figures.
* Single-page Dash app typically contains:

  * Launch site dropdown
  * Payload range slider
  * Success vs payload scatter + booster color
* Provide instructions to run: `python app.py` (or `gunicorn` for production).

### 7. Feature engineering & machine learning

* Select features (numeric + one-hot categorical).
* Split data into train/test (common: 70/30) and scale numeric features where needed.
* Train classification models: Logistic Regression, SVM, K-Nearest Neighbors, Decision Trees, Random Forests. Use `GridSearchCV` or `cross_val_score` to tune hyperparameters.

### 8. Model evaluation

* Evaluate with accuracy, precision, recall, F1-score, confusion matrix, and ROC-AUC.
* Use cross-validation to check generalization.
* Compare models and choose the best performer.

### 9. Final report & deliverables

* Final report summarizing the approach, artifacts and results.
* Include the Dash app (or instructions for local deployment).

---


## References & Sources

*  [SpaceX REST API](https://github.com/r-spacex/SpaceX-API) (launch records, rocket & core info)
*  [List of Falcon 9 and Falcon Heavy launches](http://en.wikipedia.org/wiki/List_of_Falcon_9_and_Falcon_Heavy_launches) Wikipedia Website with other public sources (used for additional fields or cross-checks)








## Authors

* [**Juan Fernandez**](mailto://juan.fernandez.sea@gmail.com) - [Linkedin](https://www.linkedin.com/in/juan-fernandez-martinez/)



## Prerequisites

You will require `Jupyter Notebook` to run this code. We recommend that you install 
the latest [Anaconda Python distribution](https://www.anaconda.com/) for your 
operating system. Anaconda Python distributions include Jupyter Notebook.


This collection supports Python 3.10. Although many options are possible, the 
authors highly recommend that users install the appropriate Anaconda package 
for their operating system. In order to ensure that you have all the required 
dependencies, we recommend that you build a suitable Python environment, as 
discussed below.


## Dependencies

|item|version|licence|package info|
|---|---|---|---|
|python|3.10.13|PSF|https://docs.python.org/3/license.html|
|matplotlib|3.8.3|PSFL|https://matplotlib.org/stable/users/project/license.html|
|beautifulsoup4|4.12.3|MIT|https://pypi.org/project/beautifulsoup4/|
|pandas|2.2.1|BSD-3|https://pandas.pydata.org|
|numpy|1.3.0|BSD-3|https://numpy.org/doc/stable/index.html|
|scikit-learn|1.7.1|BSD-3|https://scikit-learn.org/stable/|
