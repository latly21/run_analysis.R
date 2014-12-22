# CodeBook

The run_analysis.R script downloads a zip file and manipulates the data. The scripts ability to manipulate the data should demonstrate our ability to collect, work with, and clean a data set.

######Get the data

1. Download the file into the data folder. These are the files that were used:
  * Test files:
     * x_test.txt
     * y_test.txt
  * Train files:
     * x_train.txt
     * y_train.txt
  * Subject files:
     * subject_test.txt
     * subject_train.txt

2. Read the data from the files into variables.
   * y_test_data
   * y_train_data
   * x_test_data
   * x_train_data
   * subject_train
   * subject_test

######Merge testing and training files 
3. rbind the files based on the file type. For example, y_test.txt is merged with x_test.txt
  * Variables:
     * subject
     * activity
     * features

######Get the mean and standard deviation

######Name the activities in the data set


   


