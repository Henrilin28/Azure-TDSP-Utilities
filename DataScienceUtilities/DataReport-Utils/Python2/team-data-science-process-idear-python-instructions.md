<properties
	pageTitle="Instructions for using Interactive Data Exploration, Analysis and Reporting (IDEAR) in Jupyter Notebooks"
	description="To provide a flexible and interactive tool for data exploration, visualization, analysis, and pattern recognition."  
	services="machine-learning"
	documentationCenter=""
	authors="bradsev"
	manager="jhubbard"
	editor="cgronlun" />

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="01/10/2017"
	ms.author="bradsev;hangzh;"/>


# Instructions for using Interactive Data Exploration, Analysis and Reporting (IDEAR) in Jupyter Notebook (Python 2.7)

The Interactive Data Exploration, Analysis and Reporting (IDEAR) tool enables data scientists to explore and visualize data interactively, facilitating the analysis and recognition of patterns that a data set contains. These instructions provide a step-by-step guide on using IDEAR in a Jupyter Notebook (Python 2.7) to explore and analyze sample data interactively, and also how to export the results of the visualization and analysis to a report with a few clicks.

## Prerequisites

The following programs are needed to use IDEAR in Jupyter Notebook (Python 2.7):

1. Set up Jupyter Notebook server. Here are the [instructions](http://jupyter.readthedocs.io/en/latest/install.html). 
2. Install the list of required Python modules in [readme.md](readme.md). 
3. If you have deployed a [Data Science Virtual Machine](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-provision-vm), Jupyter Notebook server is already set up for you. If you are using a Linux DSVM on a Windows machine, you can [install X2Go on your client](https://azure.microsoft.com/en-us/documentation/articles/machine-learning-data-science-linux-dsvm-intro/#installing-and-configuring-x2go-client) to log into the Linux DSVM.

## Conventions, limitations, and the configuration of IDEAR

### Column name conventions for IDEAR in Jupyter Notebook 

Before you run IDEAR in Jupyter Notebook (Python 2.7), make sure that the **column names** in the data file or in the SQL query result, use the following conventions:

- Column names have to **start with alphabet letters**. Column names cannot start with numbers or special characters. 
- **Special characters**, except the underscore, are **not allowed** in any part of column names, nor is the **space character**.  


### IDEAR in Jupyter Notebook (Python 2.7) works on data frames in memory

Currently, IDEAR in Jupyter Notebook (Python 2.7) only works with data that has been loaded into Python as a Pandas data frame. If you have data that is too large to fit into the Python workspace, you may need to sample the data before running IDEAR on it. 


### Use a YAML file to provide data source, data format, and column information to IDEAR

A YAML file is needed to provide information about the data, such as the location of the data, the format of the data file (specifying, for example, the column separator used and whether or not there is a headerline), and various other parameters (itemized in the following tables) that IDEAR needs.

>[!NOTE] 
>In the YAML file, you need to set the path to your data file correctly. The path should be an absolute path, or a path relative to the working directory you are setting. Becuse Windows and Linux have different conventions for directory structures (“\\” for Windows and “/” for Linux), the path must be set using the appropriate conventions for the OS of your machine.

The following two tables list the parameters you need to set in the YAML file, depending on where the data is. We currently support two types of data files:

- Data that is in a local flat text file
- Data that is a query result from a SQL Server database.

An example YAML file can be found at [para-bike-rental-hour.yaml](para-bike-rental-hour.yaml).
 

** Data stays in a local flat text file: **

| Parameter Name | Value | Description | Example |
|:---------------|:-------------|:----------------------|:-----------------|
|DataFilePath    | Path to the local data | **Required**. (Full or relative) path and name to the data file. Use '\\' to separate directories and file names. | ..\\..\\Data\\Common\\data.csv |
|HasHeader | Yes or No | **Required**. Specifies whether the first line is a headerline. | Yes |
|Separator | ',', '\t', etc| **Required**. The separator of columns in the data file. | ',' |
|Target | Name of the machine learning target column | **Optional**. If not provided, this is just a data exploration task. | is_fraud |
|CategoricalColumns | Names of categorical columns | **Optional**. If not provided, IDEAR automatically detects the column type. | - gender |
|NumericalColumns | Names of numerical columns | **Optional**. If not provided, IDEAR automatically detects the column type. | - education_years |
|ColumnsToExclude | Names of columns to exclude | **Optional**. If not provided, IDEAR analyzes all columns. | - UserID |

** Data is a query result from a SQL database: **

If the data is the result of a SQL query on a SQL database, you do not need the first three parameters in the table above. Instead, you need the following parameters:

| Parameter Name | Value | Description | Example |
|:---------------|:-------------|:----------------------|:-----------------|
|DataSource    | SQLServer | **Required**. _SQLServer_ is the only valid value for now. But this value is valid for both SQL database, and SQL Data Warehouse.| SQLServer |
|Server | URL to the database server | **Required**. URL to the database server | mysqlserver.database.windows.net |
e|Database | Database name | **Required**. Name of the database from which to query | SQLDWTDSP |
|Username | username | **Required**. User name that can log in to the Server to run query. | datascience |
|Password | password of the username | **Required**. Password of the user that can log in to the Server to run query. | HelloWorld! |
|Query | SQL query | **Required**. Query to get the data from the database. Can be query on a single or joining multiple tables.| select * from table1 |

During interactive data exploration, you can:

- choose which variable to explore and visualize. 
- export interesting results with **EXPORT** button.
- generate a final report of your data exploration by clicking the **Generate Final Report** button. 

## Sample Dataset

To get you started with IDEAR in Jupyter Notebook (Python 2.7) quickly, two sample datasets come packaged with IDEAR in directory [Data\\Common]( ../../../Data/Common/).  

In this tutorial, we show how to run IDEAR in Jupyter Notebook (Python 2.7) using the [UCI Census Income](https://archive.ics.uci.edu/ml/datasets/Census+Income) dataset as an example. The data is located in directory [Data\\Common\\UCI_Income](../../../Data/Common/UCI_Income). The [para-adult.yaml](para-adult.yaml) file for this dataset is also provided. 

In the following example, **label_IsOver50**K (the income is over 50K) is specified as the target (dependent) variable in the YAML file.


## How to Launch IDEAR

Here are the instructions to launch IDEAR in a Jupyter Notebook (Python):

- Open a browser, and log in to the Jupyter Notebook server. If you are logging in to the Jupyter Notebook server using a browser on the Jupyter Notebook server itself, typically you type in _https://localhost:9999_ to access the Jupyter Notebook server. 

	![log-in](./media/log-in-jupyter-notebook.png)

- Upload the IDEAR.ipynb to the Jupyter Notebook server. Find the IDEAR.ipynb notebook that is located in the directory that contains these instruction on the Jupyter Notebook server. Drag and drop the IDEAR.ipynb file to the Jupyter Notebook home page. Then click **Upload** to upload the IDEAR.ipynb file to the home directory of the Jupyter Notebook server. 

	![upload](./media/upload.png)

- Open IDEAR.ipynb. If you have multiple Python kernels (such as Python 2.7 and Python 3.5), you need to select Python 2.7 as the kernel. Once IDEAR.ipynb is opened, the first cell provides some basic instructions on how to run IDEAR in Jupyter Notebook (Python 2.7).

	![basic-instructions](./media/basic_instructions.png)

- Configure and set up IDEAR by providing some global parameters. The global parameters you need to provide include:
	- _Working directory_: the absolute path to the directory containing these instruction on the Jupyter Notebook server machine. You need to set the same working directory in the first two cells. 
	- _YAML file_: the name and the path to the YAML file. The path can be an absolute path, or a relative path to the working directory. In this example, the _para\_adult.yaml_ is just in the working directory. So, we set `conf_file = '.\\para-adult.yaml'` 
	- _Name of the final report_ (a Jupyter Notebook file) that you plan to generate using IDEAR. In this example, we name it `IDEAR_Report.ipynb`.
	- _Directory to save the temporary files_: Later on, when you use IDEAR to explore the data, you will be able to export the Python scripts that are generating the results you produce with IDEAR to some temporary Jupyter Notebooks. All the Jupyter Notebooks in the directory will be merged to generate the final report. To keep the reports for each dataset you are exploring using IDEAR, create a separate directory to host these temporary files. 
	- _Sample_Size_: Large dataset can slow down the interactivity when you are using IDEAR. By default, we random sample the data to 10000 observations, if the original data has more than 10000 observations. IDEAR will use the entire dataset to generate the general statistics. When interactivity is needed, the sampled dataset is used. 

	![configure](./media/configure.png)

Now you are all set to run IDEAR to explore and visualize your dataset!

## How to use IDEAR

IDEAR guides you through the exploration of a dataset in an evolving manner:

- from a general data summary to specific variable statistics
- from simple to complex
- from single variable to multiple variables 

It is recommended that you run the code cells in IDEAR in the order provided, since some cells depend on the outputs from previous cells. 
Cells _**Global Configuration and Setting Up**_, _**Import necessary packages and set up environment parameters**_, and _**Define some functions for generating reports**_ need to run first in order to import necessary modules or define functions that are going to be used by IDEAR. 

During the interactive process of data exploration, analysis, and visualization, you can click the **Export** button for each analysis and visualization. The Python scripts used to generate the results of your analysis and visualization are output/appended to some temporary Jupyter Notebooks in the directory _export\_dir_ you specified in the second code cell of the IDEAR Jupyter Notebook. You can generate a final data report from the temporary Jupyter Notebooks in this directory. Click the **Generate Final Report** button to merge all the temporary Jupyter Notebooks in this directory to a single Jupyter Notebook. You can share this report with your project teammates or with your clients to discuss what insights you obtained from your exploration of the data. 

## 1. Read and Summarize the Data

This section of cells complete the following tasks:

- Reads data into Pandas data frame, and infers the column types (numerical or categorical).
- Prints the first n rows of the data.- Prints the dimensions, column names and types of data in the data frame.

### 1.1. Read data and infer column types

This cell completes the following tasks:

- Parses the yaml file into a dictionary.
- Reads the data into a Pandas data frame and samples the data.
- Infers whether the columns are categorical or numerical if the yaml file does not specify the type of data contained in the columns. 
- Prints which column is the target column, which columns contain categorical data, and which contain numerical data. 
![read-data](./media/read-data.png)

### 1.2. Print the first n rows of the data

This cell prints the first n (n=5 by default) of the data. Draging the scroll bar left or right prints less or more rows of data. This allows users to take a quick peek at various quantities of the data. 

![print-n-rows](./media/print-n-rows.png)

### 1.3 Print the dimensions, column names and types of the data

The following three cells print the dimensions, column names and types of the data. 

![print-dimensions](./media/print-dimensions.png)

## 2. Extract Descriptive Statistics of Each Column

In this section, descriptive statistics of numerical and categorical columns are extracted and printed separately. 

You need to run the following cell first in order to define functions needed for this section.

![descriptive-functions](./media/descriptive-functions.png)

### 2.1. Print the descriptive statistics of numerical columns.

![numerical-statistics](./media/numerical-statistics.png)

### 2.2. Print the descriptive statistics of categorical columns.

![categorical-statistics](./media/categorical-statistics.png)

## 3. Explore Individual Variables

In this section, you explore variables individually, including the target variable, numerical variables, and categorical variables. For numerical variables, a histogram, probability density plot, QQ-plot, and a box-plot are plotted. A normality test is also conducted. For categorical variables, a histogram and pie chart are plotted. 

A drop box is provided that allows you to select the variable you want to explore. 

Categorical column exploration is based on the entire dataset, and numerical column exploration is based on the sampled dataset. 

If you would like the result of an exploration and visualization on a variable to be included in your final report, click the **Export** button to export the Python code behind the exploration and visualization to a temporary Jupyter Notebook file. This temporary Jupyter Notebook will be used to generate the final report later. 

### 3.1. Explore the target variable

![explore-target](./media/explore-target.png)

### 3.2. Explore individual numeric variables and test for normality (on the sampled data)

![explore-numerical](./media/explore-numerical.png)

Click the drop down list box to select another numerical variable to explore. 

### 3.3. Explore individual categorical variables (sorted by frequencies)

![explore-categorical](./media/explore-categorical.png)

Click the drop down list box to select another categorical variable to explore. 

## 4. Explore Interactions Between Variables

Investigating the interactions and association between variables is an important type of analysis for understanding a dataset and for determining whether a dataset is suitable for a machine learning task before actually investing in building a machine learning model. In this section, we show how to evaluate and visualize inter-variable associations. The subsections correspond to the following IDEAR panes:

- 4.1 Rank variables
- 4.2 Explore interactions between categorical variables
- 4.3 Explore interactions between numerical variables (on sampled data)
- 4.4 Explore correlation matrix between numerical variables
- 4.5 Explore interactions between numerical and categorical variables
- 4.6 Explore interactions between two numerical variables and a categorical variable (on sampled data)

### 4.1. Rank variables

IDEAR calculates the strength of linear relationships between variables in the dataset with a selected reference variable. By default, the reference variable is the target variable. You can choose a different reference variable from the drop list and specify the number of top numerical and categorical variables to analyze. IDEAR then shows the top n variables in two bar charts, one for the top numerical variables, and the other one for the top categorical variables. 

- The associations between categorical and numerical variables are computed using the [eta-squared metric](https://en.wikiversity.org/wiki/Eta-squared "Eta-squared metric"). 
- The associations between categorical variables are computed using the [Cramer' V metric](https://en.wikipedia.org/wiki/Cram%C3%A9r%27s_V "Cramer's V metric").

![rank-variables](./media/rank-variables.png)

>[!ALERT] 
> If you notice that certain variables have significantly stronger associations with the target variable than others, they might be **target leakers** that already contain information from the target variable. Consider this possibility and consult someone who has domain expertise if this situation arises.

### 4.2. Explore interactions between categorical variables

A [mosaic plot](http://www.datavis.ca/online/mosaics/about.html#toc1 "two-way mosaic plot") shows the proportion of one categorical variable within the classes of another using tiles whose size is proportional to the cell frequency of a 2-way contingency table. The two categorical variables are selected from the drop-down menu boxes. The tiles are colored according to Standardized Pearson residuals (see the previous link). This plot helps you understand whether two categorical variables are dependent or not.

If the target variable is a categorical variable, by default, Categorical Var 1 is the target variable.
*
![interaction-categorical](./media/interaction-categorical.png)


### 4.3. Explore interactions between numerical variables (on sampled data)

A scatter plot shows the association between pairs of numerical variables in the dataset. The two numerical variables are selected from the drop-down menu boxes. The best fit line from a linear model fit is shown in red, and the loss fit line is shown in blue.

If the target variable is a numerical variable, by default, Numerical Var 1 is the target variable.

*![interaction-numerical](./media/interaction-numerical.png)


### 4.4. Explore correlation matrix between numerical variables

An all-by-all pair-wise correlation plot shows the association between all pairs of numerical variables the dataset. You can choose one of the three correlation methods: pearson, kendall, or spearman. 

![explore-correlation](./media/explore-correlation.png)

### 4.5. Explore interactions between numerical and categorical variables

The association between a numerical and a categorical variable can be evaluated using a box plot. ANOVA is conducted to test the null hypothesis that the mean values of the numerical variable are the same across the levels of the categorical variable. The p-value of the ANOVA test is shown. If the categorical variable is the target variable for a classification problem, this function indicates whether the numerical variable helps differentiate the different levels of the target variable.

If the target variable is a numerical variable, then by default Numerical Variable is the target variable; if a categorical variable, then by default Categorical Variable is the target variable. 

![numerical-categorical](./media/numerical-categorical.png)

### 4.6. Explore interactions between two numerical variables and a categorical variable (on sampled data)

A scatter plot of two numerical variables are plotted, and points are legended by the selected categorical variable. If the target variable is numerical, Numerical Var 1 is the target variable by default. If the target variable is categorical, Categorical Var is the target variable by default. 

This plot helps understand whether the categorical variable can be separated by the two numerical variables. If the categorical variable is the target variable, it can help determine whether these two numerical variables can differentiate the levels of the target variable. If you see a clear clustering pattern, where one cluster is dominated by one single level of the target variable, that is a good indicator that these two numerical variables are good predictors. 

![2num-1cat.png](./media/2num-1cat.png)

## 5. Visualize Numerical Data by Projecting to Principal Component Spaces

When the dimension of the data is high, data visualization is challenging. But visualizing the data can help us understand the clustering pattern in the data. For classification tasks, if you see separated clusters in the data that are dominated by different classes of the target variable, it is possible that this classification task might be tractable. Otherwise, the classification task might not be easy. You can also use this function to infer the quality of your feature set. 

This function projects the numerical sub-dataset onto a lower 2-D or 3-D space spanned by the principal components. For 2-D projection, you can choose the principal components for x, y using the dropdown menus provided in the IDEAR pane. Changing principal components for these two axes might help reveal some clustering patterns that would be hidden when viewing in other principal component axis.  

The bar chart of the percentage of variance explained by the number of principal components can help you understand how severe the multicollinearity is in the numerical sub-dataset. Put another way, it describes how singular the variance-covariance matrix is. 

For 3-D projection, the data is simply projected to the 1st, 2nd, and 3rd principal components, as the x, y, z axis respectively. In the 3-D projection scatter plot, there is a horizontal scroll bar for you to change the viewing perspective. Some clusters might be hidden behind others when looked at from one angle. Changing to another angles might help reveal these hidden clusters. 

![2d-pca](./media/2d-pca.png)

![3d-pca](./media/3d-pca.png)

## 6. Show and Hide Codes in IDEAR

After you have all ipywidgets show up in IDEAR, you might want to hide the source code in the Jupyter Notebook to make it look neater. Then, you just need to play with the ipywidgets to select the variables you want to explore and the analysis you want to conduct. You can do so by running the cell _**Show/Hide the Source Code**_. Then, you can switch on and off the display of the source codes in the Jupyter Notebook by clicking the **Toggle Raw Code** button.
 
![toggle-codes](./media/toggle-codes.png)

## 7. Generate the Final Report

When you are ready to generate the data report, click the **Generate Final Report** button. This merges the temporary Jupyter Notebook files into a single Jupyter Notebook file called IDEAR_Report.ipynb. 

![generate-report](./media/generate-report.png)

Then, you need to upload the IDEAR_Report.ipynb to your Jupyter Notebook home directory, and run the cells in order to generate the visualization and alaysis results in the final report. The final report also provides the general statistics for the data.

![final-report](./media/final-report.png)

If you want to export the report, click ***File->Download as*** in Jupyter notebook. You can save to formats such as pdf, md, and html.

![save-final-report](./media/save.png)

If you are using a source control platform to manage the artifacts of your data science project, we recommend that you check the generated data report into the platform as well. With the support of source control, the data analysis report can be versioned and shared by multiple collaborating parties. The report provides a 360 view of your dataset, summarizes insights from your analysis, and helps guide subsequent machine learning steps such as feature engineering and model building. 
