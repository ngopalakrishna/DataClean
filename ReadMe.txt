The dataset includes the following files:
=========================================

- 'run_analysis.R' - The R script file which analysis the data and creates required variable outputs for your analysis

- 'CodeBook.md': Shows information about the R script.

- 'average_data.txt' - Output average data output as a table for your reference. This is the contents of the 'avgdata' variable in the R environment


The following variables are the output of the script once executed:

- 'final_tidy_data': The final merged data between Train and Test. 

- 'avgdata': The average of each variable in the final_tidy_data grouped by Activity and Subject


Notes: 
======
- Variables starting with t are time series variables.
- Variables starting with f are derived fourier series variables
- The Samsung wearable data for performing this analysis has to be stored in folder 'UCI HAR Dataset'
- The 'UCI HAR Dataset' has to be within your working directory in R

License:
========
Use of this dataset in publications must be acknowledged by referencing the following publication [1] 

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
