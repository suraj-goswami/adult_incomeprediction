# Adult Income Prediction
<h2>Introduction</h2>
An individual’s annual income results from various factors. Intuitively, it is influenced by the individual’s education level, age, gender, occupation, and etc.

<img src="images/young-adult-make-money.jpg" width="600">
Fields
The dataset contains 16 columns
Target filed: Income
-- The income is divide into two classes: <=50K and >50K
Number of attributes: 14
-- These are the demographics and other features to describe a person

We can explore the possibility in predicting income level based on the individual’s personal information.

Acknowledgements
This dataset named “adult” is found in the UCI machine learning repository
http://www.cs.toronto.edu/~delve/data/adult/desc.html

The detailed description on the dataset can be found in the original UCI documentation
http://www.cs.toronto.edu/~delve/data/adult/adultDetail.html

Done as a Internship under Ineuron Intelligence
https://ineuron.ai/

<h2>Objective</h2>
To build a classification methodology to determine whether a person makes over 50K per year.

<h2>Architecture</h2>

<img src="images/Picture1.png" >

<h2>Data Validation and Data Transformation </h2>
<p>
i) Name Validation - Validation of files name as per the DSA. We have created a regex pattern for validation. After it checks for date format and time format if these    
   requirements are satisfied, we move such files to <b>"Good_Data_Folder"</b> else <b>"Bad_Data_Folder"</b>.

ii) Number of Columns – Validation of number of columns present in the files, and if it doesn't match then the file is moved to "Bad_Data_Folder.“

iii) Name of Columns - The name of the columns is validated and should be the same as given in the schema file. If not, then the file is moved to "Bad_Data_Folder".

iv) Data type of columns - The data type of columns is given in the schema file. It is validated when we insert the files into Database. If the datatype is wrong, then the file     is moved to "Bad_Data_Folder".

v) Null values in columns - If any of the columns in a file have all the values as NULL or missing, we discard such a file and move it to "Bad_Data_Folder".
</p>


<h2>Data Insertion in Database</h2>

i) Table creation :- Table name  “Good_Data" is created in the database for inserting the files. If the table is already present then new files are inserted in the same table.

ii) Insertion of files in the table - All the files in the "Good_Data_Folder" are inserted in the above-created table. If any file has invalid data type in any of the columns, the file is not loaded in the table 

<h2>Model Training</h2>

<h4>Data Export from Db</h4>
     The accumulated data from db is exported in csv format for model training
<h4>Data Preprocessing</h4>  
     Performing EDA to get insight of data like  identifying distribution , outliers ,trend
     among data etc.

     a)	Drop the columns not required for prediction.
     b)	Remove the unwanted spaces in data.
     c)	For this dataset, the null values were replaced with ‘?’ in the client data. Those ‘?’ have been replaced with NaN values.
     d)	Check for null values in the columns. If present, impute the null values using the categorical imputer.
     e)	Replace and encode the categorical values with numeric values.
     f)	Scale the numeric values using the standard scaler.
     g)	Handle the imbalanced dataset using oversampling.

<h4>Clustering</h4>  KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
The Kmeans model is trained over preprocessed data, and the model is saved for further use in prediction.
<h4>Model Selection</h4>  After the clusters have been created, we find the best model for each cluster. We are using two algorithms, <b>"Random Forest"</b> and <b>"XGBoost"</b>. For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the AUC scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction.

<h2>Prediction</h2>
 <ol>
   <li> The testing files are shared in the batches and we perform the same Validation operations ,data transformation and data insertion on them.</li>
   <li> The accumulated data from db is exported in csv format for  prediction.</li>
   <li>  We perform data pre-processing techniques on it.</li>
   <li> KMeans model created during training is loaded and clusters for the preprocessed data is predicted.</li>
   <li> Based on the cluster number respective model is loaded and is used to predict the data for that cluster.</li>
   <li> Once the prediction is done for all the clusters. The predictions  are saved in csv format and shared.</li>
</ol>
