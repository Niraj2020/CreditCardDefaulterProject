# CreditCardDefaulterProject

## Problem Statement:
Financial threats underscores the pressing need for commercial banks to address credit risk effectively. With advancements in the financial sector, predicting the likelihood of credit default emerges as a paramount concern for these institutions. Our primary objective revolves around forecasting credit default probabilities by analyzing the attributes of credit card holders alongside their payment histories. Through this endeavor, we aim to furnish commercial banks with robust tools to fortify their risk assessment mechanisms and safeguard against potential financial instabilities.

## Data Description
The client will send data in multiple sets of files in batches at a given location. The data has been extracted from the census bureau. The data contains 32561 instances with the following attributes: Features:

1. LIMIT_BAL: continuous Credit Limit of the person.

2. SEX: Categorical: 1 = male; 2 = female

3. EDUCATION: Categorical: 1 = graduate school; 2 = university; 3 = high school; 4 = others

4. MARRIAGE: 1 = married; 2 = single; 3 = others

5. AGE-num: continuous.

6. PAY_0 to PAY_6: History of past payment. We tracked the past monthly payment records (from April to September, 2005)

7. BILL_AMT1 to BILL_AMT6: Amount of bill statements. Target Label: Whether a person shall default in the credit card payment or not.

8. default payment next month: Yes = 1, No = 0.

In addition to the training data, a "schema" file from the client is essential, encompassing crucial details pertaining to the training files. This includes file names, the length of date values within filenames, time value length within filenames, column count, column names, and their corresponding data types. This comprehensive schema serves as a blueprint, providing essential guidance for seamless data processing and model training.

## Data Validation
 #### In This step, we perform different sets of validation on the given set of training files.

 - Name Validation: We validate the name of the files based on the given name in the schema file. We have 
created a regex patterg as per the name given in the schema fileto use for validation. After validating 
the pattern in the name, we check for the length of the date in the file name as well as the length of time 
in the file name. If all the values are as per requirements, we move such files to "Good_Data_Folder" else
we move such files to "Bad_Data_Folder."

- Number of Columns: We validate the number of columns present in the files, and if it doesn't match with the
value given in the schema file, then the file id moves to "Bad_Data_Folder."

- Name of Columns: The name of the columns is validated and should be the same as given in the schema file. 
If not, then the file is moved to "Bad_Data_Folder".

- The datatype of columns: The datatype of columns is given in the schema file. This is validated when we insert
the files into Database. If the datatype is wrong, then the file is moved to "Bad_Data_Folder."

- Null values in columns: If any of the columns in a file have all the values as NULL or missing, we discard such
a file and move it to "Bad_Data_Folder".

## Data Insertion in Database

- Database Creation and Connection: Create a database with the given name passed. If the database is already created,
 open the connection to the database. 

- Table creation in the database: Table with name - "Good_Data", is created in the database for inserting the files 
 in the "Good_Data_Folder" based on given column names and datatype in the schema file. If the table is already
 present, then the new table is not created and new files are inserted in the already present table as we want 
 training to be done on new as well as old training files.
 
 - Insertion of file in the table: All the files in the "Good_Data_Folder" are inserted in the above-created table. If
 any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to 
 "Bad_Data_Folder".

## Model Training

-  Data Export from Db: The data in a stored database is exported as a CSV file to be used for model training.

- Data Preprocessing: 
             
    1. Check for null values in the columns. If present, impute the null values using the KNN imputer.

    2. Check if any column has zero standard deviation, remove such columns as they don't give any information during 
        model training.

-  Clustering: KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters 
 is selected    

 ## Create a file "Dockerfile" with below content  

     FROM python:3.7
     COPY . /app
     WORKDIR /app
     RUN pip install -r requirements.txt
     ENTRYPOINT [ "python" ]
     CMD [ "app.py" ]  

### To Build the Docker Image on DockerHub
     docker build -t "docker_profile_name/app_name": latest .

### To Upload the Docker Image on DockerHub
      docker push "docker_profile_name/app_name": latest

### To run the container Image
      docker container run -d -p "port number:EX-5000" "docker_profile_name/app_name": latest

     
## Create a "Procfile" with following content
     web: gunicorn main:app    


## create a file ".github\workflows\main.yaml" with the above given content in .github\workflows\main.yaml this file.
 ### Select project setting in github and below environment variable
    HEROKU_API_KEY
    HEROKU_APP_NAME
    HEROKU_EMAIL_ADDRESS

## Initialize the Git Repositry
    git init
    git add .
    git commit -m "first commit"
    git branch -M main
    git remote add origin <github_url>
    git push -u origin main


 ## To update the modification or modification on github repositry
    git add .
    git commit -m "proper message"
    git push -u origin main 

 ## deployment link:-     
 AWS : https://13.51.85.45:8002/

 LinkedIn link: https://www.linkedin.com/in/neeraj-kumar-sharma-a4734b280/

 Project Video Link : https://youtu.be/AXolhU8mR0o?si=bWMlkEF16Gppqr-_

 






