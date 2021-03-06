<style type="text/css">.main-container { max-width: 940px; margin-left: auto; margin-right: auto; } code { color: inherit; background-color: rgba(0, 0, 0, 0.04); } img { max-width:100%; height: auto; } .tabbed-pane { padding-top: 12px; } .html-widget { margin-bottom: 20px; } button.code-folding-btn:focus { outline: none; }</style>

<div class="container-fluid main-container"><script>$(document).ready(function () { window.buildTabsets("TOC"); });</script>

<div class="fluid-row" id="header">

# run_analysis.R

#### _nopal_

#### _Sun Nov 11 07:41:00 2018_

</div>

    library(dplyr)

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    library(tidyr)
    library(data.table)

    ## 
    ## Attaching package: 'data.table'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     between, first, last

    ## Read train data, test data and feature names
    train <- fread("./UCI HAR Dataset/train/X_train.txt")
    test <- fread("./UCI HAR Dataset/test/X_test.txt")
    features <- scan("./UCI HAR Dataset/features.txt",character(), quote = "")
    activity_labels <- scan("./UCI HAR Dataset/activity_labels.txt",character(), quote = "")
    activity_labels <- activity_labels[c(seq(2,12, by = 2))]

    ## Read Subject, Activity details for train data
    subject_train <- scan("./UCI HAR Dataset/train/subject_train.txt", numeric(), quote = "")
    train_activity_details <- scan("./UCI HAR Dataset/train/y_train.txt",numeric(), quote = "") 
    train_activity_label <- activity_labels[train_activity_details[]]

    ## Read Subject, Activity details for test data
    subject_test <- scan("./UCI HAR Dataset/test/subject_test.txt", numeric(), quote = "")
    test_activity_details <- scan("./UCI HAR Dataset/test/y_test.txt",numeric(), quote = "") 
    test_activity_label <- activity_labels[test_activity_details[]]

    ## Step - 1 Intermediate - Merge the training and the test sets to create one data set.
    merged_data <- rbind(train, test)

    ## Step - 1a - Setting the names of columns for the merged_data
    ## Ignore the numbers from the features.txt to get the feature names
    featurenames <- features[c(seq(2,1122, by = 2))]
    setnames(merged_data, featurenames)

    ## Extract column indices of mean() and std(). 
    ## Concatenate the mean & std columns to extract
    mean_columns <- grep('?mean\\(\\)?', names(merged_data))
    std_columns <- grep('?std\\(\\)?', names(merged_data))
    mean_std_columns <-  c(mean_columns, std_columns)
    ## Step - 2 - Extracts only the measurements on the mean and standard deviation for each measurement.
    mean_std_extract <- subset(merged_data, select = mean_std_columns)

    ## Step - 3 - Uses descriptive activity names to name the activities in the data set
    activity <- c(train_activity_label, test_activity_label) 
    subject <- c(subject_train, subject_test)
    merged_activity_data <- cbind(merged_data, activity)
    merged_activity_data <- cbind(merged_activity_data, subject)

    ## Step - 4 - Appropriately label the data set with descriptive variable names
    featurenames <- gsub("\\(\\)", "", featurenames)
    featurenames <- gsub(",", "_", featurenames)
    featurenames <- gsub("\\(", "_", featurenames)
    featurenames <- gsub("\\)$", "", featurenames)
    featurenames <- gsub("\\)", "", featurenames)
    featurenames <- c(featurenames, c("activity", "subject"))
    setnames(merged_activity_data, featurenames)

    ## Step - 1 - Final tidy data
    final_tidy_data <- subset(merged_activity_data, select = -mean_std_columns)

    ## Step - 5 - Independent tidy data set with the average of each variable for each activity and each subject.
    avgdata <- aggregate(. ~subject + activity, data = final_tidy_data, FUN = mean)
    write.table(avgdata , file = "average_data.txt", row.name = FALSE)

</div>

<script>// add bootstrap table styles to pandoc tables function bootstrapStylePandocTables() { $('tr.header').parent('thead').parent('table').addClass('table table-condensed'); } $(document).ready(function () { bootstrapStylePandocTables(); });</script> <script>(function () { var script = document.createElement("script"); script.type = "text/javascript"; script.src = "https://mathjax.rstudio.com/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"; document.getElementsByTagName("head")[0].appendChild(script); })();</script>