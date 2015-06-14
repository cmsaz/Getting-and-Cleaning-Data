
# 1 - Merge the training and test sets to create one data set.

x_te <- read.table("test/X_test.txt")
y_te <- read.table("test/y_test.txt")
sub_te <- read.table("test/subject_test.txt")

x_tr <- read.table("train/X_train.txt")
y_tr <- read.table("train/y_train.txt")
sub_tr <- read.table("train/subject_train.txt")

x_dat <- rbind(x_tr, x_te)
y_dat <- rbind(y_tr, y_te)
sub_dat <- rbind(sub_tr, sub_te)

# 2 - Extract only the measurements on the mean and standard deviation for each measurement.

features <- read.table("features.txt")
mean_std_features <- grep("-(mean|std)\\(\\)", features[, 2])
x_dat <- x_dat[, mean_std_features]
names(x_dat) <- features[mean_std_features, 2]


# 3 - Use descriptive activity names to name the activities in the data set.

activities <- read.table("activity_labels.txt")
y_dat[, 1] <- activities[y_dat[, 1], 2]
names(y_dat) <- "activity"


# 4 - Appropriately labels the data set with descriptive variable names. 
names(sub_dat) <- "subject"
all_data <- cbind(x_dat, y_dat, sub_dat)


# 5 - From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

data_avg <- ddply(all_data, .(subject, activity), function(x) colMeans(x[, 1:66]))

write.table(data_avg, "data_avg.txt", row.name=FALSE)
