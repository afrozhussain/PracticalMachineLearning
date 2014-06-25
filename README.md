Practical Machine Learning Assignment
========================================================

```{r}
library(caret)
```

### Reading Training data set
```{r}
data = read.csv(file="pml-training.csv")
```

### Creating Training and Testing Data Set, 80% (training) to 20% (testing)
```{r}
inTrain = createDataPartition(data$classe, 
                              p=0.8,
                              list=F)
training = data[inTrain,]
testing = data[-inTrain,]
```
### Model Fitting - in this case randomForest Classifier with k-fold cross validation, with 4 folds
```{r}
trControl = trainControl(method="cv", number=4)
model = train(training$classe~num_window, method="rf", data= training, trControl=trControl)
```

### Print Model

```{r}
print(model)

```
###  Checking the model accuracy on test data set

```{r}
confusionMatrix(training$classe , predict(model, training) )
```

### Predicting on provided test data set
```{r}
testData = read.csv(file="pml-testing.csv")
pred = predict(model, testData)
```

