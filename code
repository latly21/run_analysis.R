
##IF NECESSARY ./DATA FILE DOES NOT EXIST THEN CREATE IT
if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
 
##HAD TO USE 'AUTO' INSTEAD OF 'CURL' TO STOP ERROR
download.file(fileUrl,destfile="./data/Dataset.zip",method="auto")
unzip(zipfile="./data/Dataset.zip",exdir="./data")


get_file_path <- file.path("./data" , "UCI HAR Dataset")
files<-list.files(get_file_path, recursive=TRUE)


##READ Y TRAINING AND TEST FILES INTO VARIABLES
y_test_data  <- read.table(file.path(get_file_path, "test" , "Y_test.txt" ),header = FALSE)
y_train_data <- read.table(file.path(get_file_path, "train", "Y_train.txt"),header = FALSE)

##READ X TRAINING AND TEST FILES INTO VARIABLES
X_test_data  <- read.table(file.path(get_file_path, "test" , "X_test.txt" ),header = FALSE)
X_train_data <- read.table(file.path(get_file_path, "train", "X_train.txt"),header = FALSE)

##READ SUBJECT FILES
subject_train <- read.table(file.path(get_file_path, "train", "subject_train.txt"),header = FALSE)
subject_test  <- read.table(file.path(get_file_path, "test" , "subject_test.txt"),header = FALSE)

##MERGE FILES
subject <- rbind(subject_train, subject_test)
activity<- rbind(y_train_data, y_test_data)
features<- rbind(X_train_data, X_test_data)


names(subject)<-c("subject")
names(activity)<- c("activity")
feature_names <- read.table(file.path(get_file_path, "features.txt"),head=FALSE)
names(features)<- feature_names$V2

mush_the_data <- cbind(subject, activity)
just_data <- cbind(features, mush_the_data)

sub_feature_names<-feature_names$V2[grep("mean\\(\\)|std\\(\\)", feature_names$V2)]

selected_names<-c(as.character(sub_feature_names), "subject", "activity" )
just_data<-subset(just_data,select=selected_names)

activityLabels <- read.table(file.path(get_file_path, "activity_labels.txt"),header = FALSE)

##CREATE BETTER NAMING CONVENTION
names(just_data)<-gsub("^t", "time", names(just_data))
names(just_data)<-gsub("^f", "frequency", names(just_data))
names(just_data)<-gsub("Acc", "Accelerometer", names(just_data))
names(just_data)<-gsub("Gyro", "Gyroscope", names(just_data))
names(just_data)<-gsub("Mag", "Magnitude", names(just_data))
names(just_data)<-gsub("BodyBody", "Body", names(just_data))

##TIDY DATA SECTION
##install.packages("plyr")
library(plyr);
tidy_data<-aggregate(. ~subject + activity, just_data, mean)
tidy_data<-tidy_data[order(tidy_data$subject,tidy_data$activity),]
write.table(tidy_data, file = "tidydata.txt",row.name=FALSE)
