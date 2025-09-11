
# IBM Data Science Capstone — SpaceX Falcon 9 Landing Prediction

> **Project goal:** Predict whether the first stage of a SpaceX Falcon 9 rocket will land successfully. The capstone simulates a startup ("SpaceY") competing with SpaceX and uses historical launch data to build an end-to-end data science solution.

---

## Summary

This repository contains the notebooks, data and code for the IBM Data Science capstone project. The aim is to collect SpaceX launch data (SpaceX REST API and public sources), clean and explore it, create interactive visualizations (Folium maps and a Plotly Dash dashboard), and build classification models to predict first-stage landing success.

## Datasets & key features

**Raw data sources (typical):**

* SpaceX REST API (launch records, rocket & core info)
* Wikipedia tables / other public sources (used for additional fields or cross-checks)

**Typical processed dataset(s):**

* `spacex_launch_dash.csv` — a well-known consolidated CSV used by the dashboard and modelling notebooks.

**Common features you'll see / create:**

* `FlightNumber` (int) — mission/flight sequence
* `LaunchSite` (categorical) — e.g., CCAFS LC-40, KSC LC-39A
* `PayloadMass (kg)` (numeric) — payload mass
* `Orbit` (categorical) — target orbit (LEO, GTO, SSO, etc.)
* `BoosterVersion` / `BoosterVersionCategory` (categorical)
* `Class` or `LandingOutcome` (binary target) — 1 = success, 0 = failure
* `Date` / `Year` (datetime / int)

*Feature engineering notes:* create `Year`/`Month`, bucket `PayloadMass`, one-hot encode categorical fields, and compute derived metrics such as previous-flight count for a booster.

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

* Final Jupyter notebook summarizing the approach, artifacts and results.
* Export or serialize final model(s) (pickle / joblib) into `models/`.
* Include the Folium map(s) and link to the Dash app (or instructions for local deployment).
* Write a short conclusion and recommendations for stakeholders (e.g., which features most affect landing success).

---

## Typical repo structure

```
ibm-spacex-capstone/
├─ data/
│  ├─ raw/
│  └─ processed/
├─ notebooks/
│  ├─ 1_data_collection.ipynb
│  ├─ 2_data_wrangling.ipynb
│  ├─ 3_eda.ipynb
│  ├─ 4_mapping_folium.ipynb
│  └─ 5_modeling.ipynb
├─ dash/
│  └─ app.py
├─ models/
├─ requirements.txt
└─ README.md
```

## How to run (quickstart)

```bash
# create env & install
python -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows
pip install -r requirements.txt

# Jupyter
jupyter notebook notebooks/1_data_collection.ipynb

# Run dash app (local)
cd dash
python app.py
# open http://127.0.0.1:8050 in your browser
```

## Tips & common pitfalls

* Make sure to consistently interpret the target label: many students use `Class` or `LandingOutcome` and mix definitions. Document yours.
* Imputation choices for `PayloadMass` can affect model performance — try mean, median, and model-based imputation.
* One-hot encoding can explode dimensionality if you keep very granular categorical fields (e.g., many unique booster names). Consider grouping.
* When comparing models, prefer stratified cross-validation if the target is imbalanced.

## Credits & references

This project follows the IBM Data Science capstone template (SpaceX Falcon 9 first-stage landing prediction).

---

If you want, I can also:

* provide ready-to-copy badges and a short license header, or
* generate a `requirements.txt` tuned for this project, or
* convert this into a ready-to-paste `README.md` file in your repo.





# SpaceX Data and ML

In this project, we will predict if the Falcon 9 first stage will land successfully. SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is because SpaceX can reuse the first stage. Therefore if we can determine if the first stage will land, we can determine the cost of a launch. This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.


For any questions about this repository, please contact me via juan.fernandez.sea@gmail.com

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
