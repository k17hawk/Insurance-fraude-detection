## Demo </br>
<img src="https://github.com/k17hawk/Insurance-fraude-detection/blob/main/demo.png"/>
## Architecture
<img src="https://github.com/k17hawk/Insurance-fraude-detection/blob/main/156880590-5f640a12-a1df-4fc6-86bc-f844bdf66c00.png"/>
# Overview </br> 
This is an Insurance Fraud Classification Flask app trained on KMeans, KNN, and Xgboost. Here in this app data is given by the user in the form of CSV format.</br> 

**Code is organized in a Modular Format.** </br> 
First user input data is stored in a Sqlite database where a given CSV file is separated as a good file or a bad file according to the specified Schema file thus separate good file is given for model training.</br> 
After preprocessing the data we select a sample by the means of the Clustering technique and perform hyperparameter tuning then we train a model according to that cluster and select the best model according to their AUC score. </br> 

# Technical Aspect 
This project is divided into two parts </br> 

1 Data preprocessing, model building, and selection. </br> 
# Data Validation </br> 
**Name Validation**- We validate the name of the files based on the given name in the schema file. We have created a regex pattern as per the name given in the schema file to use for validation. After validating the pattern in the name,
we check for the length of the date in the file name as well as the length of time in the file name. If all the values are as per requirement, we move such files to "Good_Data_Folder" else we move such files to "Bad_Data_Folder." </br> 
**Number of Columns** - We validate the number of columns present in the files, and if it doesn't match the value given in the schema file, then the file is moved to "Bad_Data_Folder." </br> 
**Name of Columns** - The name of the columns is validated and should be the same as given in the schema file. If not, then the file is moved to "Bad_Data_Folder". </br> 
**The datatype of columns** - The datatype of columns is given in the schema file. It is validated when we insert the files into the Database. If the datatype is wrong, then the file is moved to "Bad_Data_Folder". </br> 
**Null values in columns** - If any of the columns in a file have all the values as NULL or missing, we discard such a file and move it to "Bad_Data_Folder". </br> 
# Data Insertion in Database </br> 
**Database Creation and connection.** </br> 
**Table creation in the database:** A table with the name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" 
based on the given column names and datatype in the schema file. If the table is already present, then the new table is not created, and new files are
inserted in the already present table as we want training to be done on new as well as old training files.  </br> 
**Insertion of files in the table.** </br> 
# Model Training </br> 
**Data Export from Db**- The data in a stored database is exported as a CSV file to be used for model training. </br> 
# Data Preprocessing </br> 
**Drop the columns not required for prediction.** </br> 
**For this dataset, the null values were replaced with ‘?’ in the client data. Those ‘?’ have been replaced with NaN values.** </br> 
**Check for null values in the columns. If present, impute the null values using the categorical imputer.** </br> 
**Replace and encode the categorical values with numeric values.** </br> 
**Scale the numeric values using the standard scaler**</br> 
# Clustering </br> 
**KMeans algorithm is used to create clusters in the preprocessed data.** </br> 
The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using the "KneeLocator" function. The idea behind clustering is to implement different algorithms.
Model Selection </br> 
We are using two algorithms, “SVM” and "XGBoost". </br> 
For each cluster, both algorithms are passed with the best parameters derived from GridSearch. </br> 
We calculate the AUC scores for both models and select the model with the best score. </br> 
The model is selected for each cluster and all the models for every cluster are saved for use in prediction. </br> 
Prediction </br> 
**Data Export from Db** - The data in the stored database is exported as a CSV file to be used for prediction. </br> 
**Data Preprocessing**(Same steps as above) </br> 
Clustering </br> 
**Prediction** - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.</br> 
Once the prediction is made for all the clusters, the predictions along with the Wafer names are saved in a CSV file at a given location, and the location is returned to the client.

# Installation </br> 
The Code is written in Python 3.7. If you don't have Python installed you can find it here. If you are using a lower version of Python you can upgrade using the pip package, ensuring you have the latest version of pip. To install the required packages and libraries, run this command in the project directory after cloning the repository: </br> 
```pip install -r requirements.txt```

# Run </br> 
**Step 1**: Clone the repository. </br> 

```git clone https://github.com/dipesg/Insurance_Fraud.git``` </br> 
**Step 2**: Create a virtual environment, either by using conda, pyenv, or venv. </br> 

```conda create -n fraud python=3.7 -y```  </br> 
**Step 3**: Install dependencies. </br> 

```pip install -r requirements.txt``` </br> 
**Step 4**: Run the app from the terminal. </br> 

```python main.py```
