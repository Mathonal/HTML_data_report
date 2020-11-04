# HTML REPORTING
Small uses cases of WRITING an HTMLReport DESCRIBING an input dataset in CSV format.

Main result is the report_'filename'.html in output folder

Report contains :
1. structure : shape, column types, counting missing data
2. distributions : computing mean STD and ploting population distribution per column (in quartile)
3. Principal Component Analysis comparing to target or find clusters: 
- count optimal PCA number and explained variances associated and plot graph
- plots column loads for each PC pairing
- projects population in each PC pairing scale (With colorscale on Target if there is one, else try to find the optimal clusters number to categorize data)

### 0.Presentation : 
This is in Jupiter NOTEBOOK Form as a demonstrator.
There is a lot of room for improvements.
1. Full automation : transpose out of notebook in web app.
    Might suppose rendering with FLASK, 
    JSscript to input file and select treatment options
    Encapsulation of the main process in Python functions/classes.
2. HTML content & CSS beautification : better scripting of main page, better CSS organisation
3. Rendering plots with DASH app in order to lighten reports (several kMo in local mode)
4. More in depth describing : suppose a lot more of error management if i want to keep it generalized (able to parse 'any' csv)
5. in case of clustering : might be useful to re-print subsets of clusters and eventually launch another PCA per subset, might give better insight on each cluster properties.

### 1.ERROR gestion :
notebook contains several error checkpoints that should not stop the html writing !

1. ERR at file load : if separator is not recognized ('tab' ',' or ';'), rest of reporting is cancelled ERR at PCA calculation : 

2. ERR if normalization and PCA computing fail, the rest of reporting operations are cancelled. This happens when non-numerical data stealth through dropNonNumerical column and dropNA-screening

3. ERR if target column name is unrecognised or none given : Computation switch to Clustering of the dataset but some error message will be printed in report in case of unrecognised name.


### 2_PCA :
PCA automatically filters : 
1. non numerical column
2. rows with missing values. 

give optimal PCAs number based on :
1. a new PC explains MORE than 10% of variances
2. less than 90% of total variance already explained
3. minimum of 2 PC (to be able to plot a graph)


### 3_Clustering(K-Means) :
Clustering is used when not target column is defined.
it search the best Silhouette result between 2 cluster and Number of column in dataset clusters.

In case clustering is used, a graph of silhouette values is also plotted in order to verify the accuracy of the 'Optimal Value' retained.