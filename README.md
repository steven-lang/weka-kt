[![Maven Central](https://img.shields.io/maven-central/v/com.github.slang03/weka-kt.svg?label=Maven%20Central)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.github.slang03%22%20a%3A%22weka-kt%22)

# Weka-Kt: Kotlin Extensions for Weka
A set of Kotlin extensions for [Weka](https://www.cs.waikato.ac.nz/ml/weka/). The goal is to make the use of Weka more convenient and idiomatic.

Available extensions:
- [Loading Data](#Loading-Data)
- [Getting/Setting Data](#Getting/Setting-Data)
- [Using Filters](#Using-Filters)
- [Create Holdout Split](#Create-Holdout-Split)
- [Perform Holdout Evaluation](#Perform-Holdout-Evaluation)
- [Perform Cross Validation](#Perform-Cross-Validation)

## Getting Started
To add Weka-Kt to your project, add the following dependency to your dependency manager:

**Maven** 
```xml
<dependency>
    <groupId>com.github.slang03</groupId>
    <artifactId>weka-kt</artifactId>
    <version>0.0.2</version>
</dependency>
```

**Gradle**
```
compile 'com.github.slang03:weka-kt:0.0.2'
```
___

## Extensions

### Loading Data

**Java**

```java
ArffLoader loader = new ArffLoader();
loader.setFile(new File("src/test/resources/datasets/iris.arff"));
Instances irisData = loader.getDataSet();
irisData.setClassIndex(4);
```

**Kotlin**

```kotlin
var irisData = Instances("src/test/resources/datasets/iris.arff", classIndex = 4)
```

### Getting/Setting Data

**Java**

```java
// Get row
Instance row = irisData.get(5);

// Get value
double valueByIndex = irisData.get(5).value(3);

// Get attribute
Attribute attribute = irisData.attribute(3);

// Get value by attribute
double valueByAttribute = row.value(attribute);

// Set row
irisData.set(6, row);

// Set value at index (6,3)
Instance editRow = irisData.get(6);
editRow.setValue(3, 100.0);
irisData.set(6, editRow);
```

**Kotlin**

```kotlin
// Get row
val row = irisData[5]

// Get value
val valueByIndex = irisData[5, 3]

// Get attribute
val attribute = irisData.attributes[3]

// Get value by attribute
val valueByAttribute = row[attribute]

// Set row
irisData[6] = row

// Set value at index (6,3)
irisData[6, 3] = 100.0
```
### Using Filters

**Java**

```java
// Filter percentage
RemovePercentage removePercentage = new RemovePercentage();
removePercentage.setPercentage(20.0);
removePercentage.setInvertSelection(true);
removePercentage.setInputFormat(irisData);
irisData = Filter.useFilter(irisData, removePercentage);

// Filter attributes
Remove remove = new Remove();
remove.setAttributeIndices("1,2");
remove.setInvertSelection(false);
remove.setInputFormat(irisData);
irisData = Filter.useFilter(irisData, remove);

// Resample data
Resample resample = new Resample();
resample.setRandomSeed(42);
resample.setNoReplacement(false);
resample.setSampleSizePercent(66.0);
resample.setInputFormat(irisData);
irisData = Filter.useFilter(irisData, resample);
```

**Kotlin**

```kotlin
// Filter percentage
irisData = irisData.filter(RemovePercentage()) {
    percentage = 20.0
    invertSelection = true
}

// Filter attributes
irisData = irisData.filter(Remove()) {
    attributeIndices = "1,2"
    invertSelection = false
}

// Resample data
irisData = irisData.filter(Resample()) {
    noReplacement = false
    randomSeed = 42
    sampleSizePercent = 66.0
}
```

**Kotlin** (Chaining Filters)

```kotlin
// Chain Filters
irisData = irisData.filter(RemovePercentage()) { // Filter percentage
    percentage = 20.0
    invertSelection = true
}.filter(Remove()) { // Filter attributes
    attributeIndices = "1,2"
    invertSelection = false
}.filter(Resample()) { // Resample data
    noReplacement = false
    randomSeed = 42
    sampleSizePercent = 66.0
}
```

### Create Holdout Split

**Java**

```java
// Create filter for train set
RemovePercentage removePercentageTrain = new RemovePercentage();
removePercentageTrain.setPercentage(33.0);
removePercentageTrain.setInputFormat(irisData);

// Create filter for test set
RemovePercentage removePercentageTest = new RemovePercentage();
removePercentageTest.setPercentage(33.0);
removePercentageTest.setInvertSelection(true);
removePercentageTest.setInputFormat(irisData);

// User filters and generate train/test sets
Instances train = Filter.useFilter(irisData, removePercentageTrain);
Instances test = Filter.useFilter(irisData, removePercentageTest);
```

**Kotlin**

```kotlin
val (train, test) = irisData.split(testPercentage = 33.0)
```

### Perform Holdout Evaluation

**Java**

```java
// Create and build classifier
J48 j48 = new J48();
j48.buildClassifier(train);

// Evaluate model
Evaluation eval = new Evaluation(train);
eval.evaluateModel(j48, test);
System.out.println(eval.toSummaryString());
```

**Kotlin**

```kotlin
// Create classifier
val j48 = J48()

// Evaluate classifier
val eval = j48.evaluateHoldout(trainData = train, testData = test)
println(eval.toSummaryString())
```

**Kotlin** (Implicit Split)

```kotlin
...
val eval = j48.evaluateHoldout(data = data, testPercentage = 33.0)
```
### Perform Cross Validation

**Java**

```java
// Create classifier
J48 j48 = new J48();

// Create cross validation
int numFolds = 10;
Random rand = new Random(1);
Evaluation eval = new Evaluation(irisData);
eval.crossValidateModel(j48, irisData, numFolds, rand);
System.out.println(eval.toSummaryString());
```

**Kotlin**

```kotlin
// Create classifier
val j48 = J48()

// Create cross validation
val eval = j48.evaluateCrossValidation(data = irisData, numFolds = 10, seed = 1)
println(eval.toSummaryString())
```