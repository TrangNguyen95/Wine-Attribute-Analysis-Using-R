# Wine-Attribute-Analysis-Using-R
Using R/Rstudio to run analysis on the attributes for Red Wine and White Wine. The purpose of this study is to determine what attributes are important in wine quality.
#Red Wine
# Read in the red dataset
data1<-read.csv("~/wine_red.csv")

# Look at the column names
names(data1)
#data1<- na.omit(data1)
# Split the dataset into a training and test dataset using a split of 75% training
# and 25% test
set.seed(42)
nrow(data1)

trainingObs_red<-sample(nrow(data1),0.75*nrow(data1),replace=FALSE)

# Create the training dataset
trainingDS_red<-data[trainingObs_red,]
View(trainingDS_red)
# Create the test dataset
testDS_red<-data[-trainingObs_red,]
View(testDS_red)
write.csv(testDS_red,file="red_test.csv")

#smote training data
table(trainingDS_red$BQ2_quality)
smoted_red<-SMOTE(BQ2_quality ~ ., trainingDS_red, perc.over=400, perc.under= 125)
table(smoted_red$BQ2_quality)
write.csv(smoted_red, file="red_train_smote.csv")

#White Wine
# Create an RF model for predicting mineral or rock

# We will need these libraries ... install.packages("    "), before running
library(caret)
library(pROC)

# Read in the dataset
data<-read.csv("~/winequality-w.csv")

# Look at the column names
names(data)
#data1<- na.omit(data1)
# Split the dataset into a training and test dataset using a split of 75% training
# and 25% test
set.seed(42)
nrow(data)

trainingObs<-sample(nrow(data),0.75*nrow(data),replace=FALSE)

# Create the training dataset
trainingDS<-data[trainingObs,]
View(trainingDS)
# Create the test dataset
testDS<-data[-trainingObs,]
View(testDS)
write.csv(testDS,file="white_test.csv")

#smote training data
table(trainingDS$BQ2_quality)
smoted_white<-SMOTE(BQ2_quality ~ ., trainingDS, perc.over=330, perc.under= 135)
table(smoted_white$BQ2_quality)
write.csv(smoted_white, file="white_train_smote.csv")

