
# SpaceX Falcon 9 Landing Prediction: Data and ML

SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is because SpaceX can reuse the first stage. Therefore if we can determine if the first stage will land, we can determine the cost of a launch. This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.

This repository contains the notebooks, data and code for the project. The aim is to collect SpaceX launch data (SpaceX REST API and public sources), clean and explore it, create interactive visualizations (Folium maps and a Plotly Dash dashboard), and build classification models to predict first-stage landing success.



## Workflow

The project begins with setting up a Github repository and creating a structured folder layout, with folders for data, notebooks, dashboards, models, and reports. At this stage, a requirements file and a README are added, where the project is divided in different modules.

Next comes data collection. Launch data is pulled from the SpaceX REST API and stored in raw JSON format [(Module 1, APIs)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%201%20Collect%20API%20jupyter-labs-spacex-data-collection-api.ipynb). Wikipedia tables or other sources can be used for complementary information. The raw JSON is flattened and converted to a tabular CSV for processing. The following phase is data wrangling and cleaning [(Module 1, Wrangling)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%201%20Data%20Wrangling%20labs-jupyter-spacex-Data%20wrangling-v2.ipynb). This includes filtering for Falcon 9 launches, handling missing values such as payload mass, renaming fields for consistency, and creating the target label (success or failure). The cleaned dataset is saved for later use.

Once the data is ready, exploratory data analysis (EDA) is performed [(Module 2, EDA)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%202%20EDA%20Visualization%20edadataviz.ipynb). This step involves visualizing distributions of payloads and flight numbers, examining correlations between payload mass and landing success, and calculating success rates per launch site, orbit, and booster version. Both Pandas and visualization libraries like Matplotlib or Plotly are used here. Executed SQL to complete this EDA activities [(Module 2, SQL)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%202%20SQL%20jupyter-labs-eda-sql-edx_sqllite.ipynb).

The geospatial analysis follows with Folium maps [(Module 3, Folium)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%203%20Folium%20lab_jupyter_launch_site_location.ipynb). Launch sites and landing sites are plotted with markers, and additional information can be displayed in popups. The resulting maps are saved as HTML and can be shared or embedded.

The next major step is building an interactive dashboard with Plotly Dash [(Module 3, Plotly Dash)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%203%20Task%20Plotly%20Dash.ipynb). The dataset `spacex_launch_dash.csv` [(Module 3, Dash dataset)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/tree/main/Jupyter%20Files%20and%20Data) is used to create a web app where users can select launch sites and payload ranges, and see dynamic scatter plots and success rate charts. The app is run locally and accessible via a browser [(Dashboard HTML)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/tree/main/Dash_files).

After visualization, the focus shifts to feature engineering and machine learning [(Module 4, Machine Learning Process)](https://github.com/SeaGraphData/SpaceX-Data-and-ML/blob/main/Jupyter%20Files%20and%20Data/Module%204%20SpaceX_Machine%20Learning%20Prediction_Part_5.ipynb). Features are selected and prepared through scaling and one-hot encoding. The dataset is split into training and testing subsets, and several classification algorithms are trained, including Logistic Regression, SVM, KNN, Decision Trees, and Random Forests. Hyperparameters are tuned using grid search or cross-validation.

The models are then evaluated based on accuracy, precision, recall, F1-score, confusion matrices, and ROC-AUC. Stratified cross-validation is often used to handle class imbalance. The models are compared and the best performer is selected.

The project concludes with a final report that summarizes the findings [(Report)](), includes the Jupyter notebooks, and provides artifacts such as the trained models, Folium maps, and the Dash app. Recommendations are presented to stakeholders, with insights into which features most influence landing success.


For any questions about this repository, please contact me via juan.fernandez.sea@gmail.com



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
