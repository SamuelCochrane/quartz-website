---
aliases: 
date: 2019-10-25
dateModified: 2024-07-07
fileClass:
  - Page
image: 
share: true
stage: 🌿 Fern
title: Does this coffee taste like dirt (Machine Learning)
---

Question: Given the aroma/bitterness/etc of a cup of coffee, can we predict if it will be a 'good' cup of coffee as rated by professional coffee tasters?

Check out the [Jupyter Notebook](https://github.com/SamuelCochrane/CoffeeML/blob/master/CoffeeML.ipynb) to follow along.

We'll bring in the data, do preliminary exploration, transform it for analysis, separate it into training/test sets, determine which model results in the highest accuracy predictions, and predict the rating a new cup of coffee might receive.

Info from [The Coffee Institute](https://coffeeinstitute.org), data scraped by [James LeDoux](https://github.com/jldbc/coffee-quality-database).

***

Let's start with our initial imports. This will bring in everything we'll need for the project, including ways to manipulate data (pandas), visualize data (matplotlib), and do ML analysis (sklearn)

```python
#importing
##data tools
import pandas as pd
pd.set_option('display.max_columns', 500)
import matplotlib.pyplot as plt
import matplotlib.colors as mcolors
##ML tools
from sklearn.ensemble import RandomForestClassifier
from sklearn import svm
from sklearn.svm import SVC
from sklearn.neural_network import MLPClassifier
from sklearn.metrics import confusion_matrix, classification_report
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.model_selection import train_test_split
%matplotlib inline
```

Next let's get the data and take a quick look at it.

```python
coffeeRaw = pd.read_csv('arabica_data_cleaned.csv')
```

```python
coffeeRaw.head()
```

<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
}

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Unnamed: 0</th>
<th>Species</th>
<th>Owner</th>
<th>Country.of.Origin</th>
<th>Farm.Name</th>
<th>Lot.Number</th>
<th>Mill</th>
<th>ICO.Number</th>
<th>Company</th>
<th>Altitude</th>
<th>Region</th>
<th>Producer</th>
<th>Number.of.Bags</th>
<th>Bag.Weight</th>
<th>In.Country.Partner</th>
<th>Harvest.Year</th>
<th>Grading.Date</th>
<th>Owner.1</th>
<th>Variety</th>
<th>Processing.Method</th>
<th>Aroma</th>
<th>Flavor</th>
<th>Aftertaste</th>
<th>Acidity</th>
<th>Body</th>
<th>Balance</th>
<th>Uniformity</th>
<th>Clean.Cup</th>
<th>Sweetness</th>
<th>Cupper.Points</th>
<th>Total.Cup.Points</th>
<th>Moisture</th>
<th>Category.One.Defects</th>
<th>Quakers</th>
<th>Color</th>
<th>Category.Two.Defects</th>
<th>Expiration</th>
<th>Certification.Body</th>
<th>Certification.Address</th>
<th>Certification.Contact</th>
<th>unit_of_measurement</th>
<th>altitude_low_meters</th>
<th>altitude_high_meters</th>
<th>altitude_mean_meters</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>1</td>
<td>Arabica</td>
<td>metad plc</td>
<td>Ethiopia</td>
<td>metad plc</td>
<td>NaN</td>
<td>metad plc</td>
<td>2014/2015</td>
<td>metad agricultural developmet plc</td>
<td>1950-2200</td>
<td>guji-hambela</td>
<td>METAD PLC</td>
<td>300</td>
<td>60 kg</td>
<td>METAD Agricultural Development plc</td>
<td>2014</td>
<td>April 4th, 2015</td>
<td>metad plc</td>
<td>NaN</td>
<td>Washed / Wet</td>
<td>8.67</td>
<td>8.83</td>
<td>8.67</td>
<td>8.75</td>
<td>8.50</td>
<td>8.42</td>
<td>10.0</td>
<td>10.0</td>
<td>10.0</td>
<td>8.75</td>
<td>90.58</td>
<td>0.12</td>
<td>0</td>
<td>0.0</td>
<td>Green</td>
<td>0</td>
<td>April 3rd, 2016</td>
<td>METAD Agricultural Development plc</td>
<td>309fcf77415a3661ae83e027f7e5f05dad786e44</td>
<td>19fef5a731de2db57d16da10287413f5f99bc2dd</td>
<td>m</td>
<td>1950.0</td>
<td>2200.0</td>
<td>2075.0</td>
</tr>
<tr>
<th>1</th>
<td>2</td>
<td>Arabica</td>
<td>metad plc</td>
<td>Ethiopia</td>
<td>metad plc</td>
<td>NaN</td>
<td>metad plc</td>
<td>2014/2015</td>
<td>metad agricultural developmet plc</td>
<td>1950-2200</td>
<td>guji-hambela</td>
<td>METAD PLC</td>
<td>300</td>
<td>60 kg</td>
<td>METAD Agricultural Development plc</td>
<td>2014</td>
<td>April 4th, 2015</td>
<td>metad plc</td>
<td>Other</td>
<td>Washed / Wet</td>
<td>8.75</td>
<td>8.67</td>
<td>8.50</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>10.0</td>
<td>10.0</td>
<td>10.0</td>
<td>8.58</td>
<td>89.92</td>
<td>0.12</td>
<td>0</td>
<td>0.0</td>
<td>Green</td>
<td>1</td>
<td>April 3rd, 2016</td>
<td>METAD Agricultural Development plc</td>
<td>309fcf77415a3661ae83e027f7e5f05dad786e44</td>
<td>19fef5a731de2db57d16da10287413f5f99bc2dd</td>
<td>m</td>
<td>1950.0</td>
<td>2200.0</td>
<td>2075.0</td>
</tr>
<tr>
<th>2</th>
<td>3</td>
<td>Arabica</td>
<td>grounds for health admin</td>
<td>Guatemala</td>
<td>san marcos barrancas "san cristobal cuch</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>1600 - 1800 m</td>
<td>NaN</td>
<td>NaN</td>
<td>5</td>
<td>1</td>
<td>Specialty Coffee Association</td>
<td>NaN</td>
<td>May 31st, 2010</td>
<td>Grounds for Health Admin</td>
<td>Bourbon</td>
<td>NaN</td>
<td>8.42</td>
<td>8.50</td>
<td>8.42</td>
<td>8.42</td>
<td>8.33</td>
<td>8.42</td>
<td>10.0</td>
<td>10.0</td>
<td>10.0</td>
<td>9.25</td>
<td>89.75</td>
<td>0.00</td>
<td>0</td>
<td>0.0</td>
<td>NaN</td>
<td>0</td>
<td>May 31st, 2011</td>
<td>Specialty Coffee Association</td>
<td>36d0d00a3724338ba7937c52a378d085f2172daa</td>
<td>0878a7d4b9d35ddbf0fe2ce69a2062cceb45a660</td>
<td>m</td>
<td>1600.0</td>
<td>1800.0</td>
<td>1700.0</td>
</tr>
<tr>
<th>3</th>
<td>4</td>
<td>Arabica</td>
<td>yidnekachew dabessa</td>
<td>Ethiopia</td>
<td>yidnekachew dabessa coffee plantation</td>
<td>NaN</td>
<td>wolensu</td>
<td>NaN</td>
<td>yidnekachew debessa coffee plantation</td>
<td>1800-2200</td>
<td>oromia</td>
<td>Yidnekachew Dabessa Coffee Plantation</td>
<td>320</td>
<td>60 kg</td>
<td>METAD Agricultural Development plc</td>
<td>2014</td>
<td>March 26th, 2015</td>
<td>Yidnekachew Dabessa</td>
<td>NaN</td>
<td>Natural / Dry</td>
<td>8.17</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>8.50</td>
<td>8.25</td>
<td>10.0</td>
<td>10.0</td>
<td>10.0</td>
<td>8.67</td>
<td>89.00</td>
<td>0.11</td>
<td>0</td>
<td>0.0</td>
<td>Green</td>
<td>2</td>
<td>March 25th, 2016</td>
<td>METAD Agricultural Development plc</td>
<td>309fcf77415a3661ae83e027f7e5f05dad786e44</td>
<td>19fef5a731de2db57d16da10287413f5f99bc2dd</td>
<td>m</td>
<td>1800.0</td>
<td>2200.0</td>
<td>2000.0</td>
</tr>
<tr>
<th>4</th>
<td>5</td>
<td>Arabica</td>
<td>metad plc</td>
<td>Ethiopia</td>
<td>metad plc</td>
<td>NaN</td>
<td>metad plc</td>
<td>2014/2015</td>
<td>metad agricultural developmet plc</td>
<td>1950-2200</td>
<td>guji-hambela</td>
<td>METAD PLC</td>
<td>300</td>
<td>60 kg</td>
<td>METAD Agricultural Development plc</td>
<td>2014</td>
<td>April 4th, 2015</td>
<td>metad plc</td>
<td>Other</td>
<td>Washed / Wet</td>
<td>8.25</td>
<td>8.50</td>
<td>8.25</td>
<td>8.50</td>
<td>8.42</td>
<td>8.33</td>
<td>10.0</td>
<td>10.0</td>
<td>10.0</td>
<td>8.58</td>
<td>88.83</td>
<td>0.12</td>
<td>0</td>
<td>0.0</td>
<td>Green</td>
<td>2</td>
<td>April 3rd, 2016</td>
<td>METAD Agricultural Development plc</td>
<td>309fcf77415a3661ae83e027f7e5f05dad786e44</td>
<td>19fef5a731de2db57d16da10287413f5f99bc2dd</td>
<td>m</td>
<td>1950.0</td>
<td>2200.0</td>
<td>2075.0</td>
</tr>
</tbody>
</table>
</div>

Ok. That's a _lot_ of info, far more than we need really.
Remember, our goal is to build something that can predict a value using only information we might have about a cup of coffee right in front of us. We won't know the elevation, processing method, etc.
So let's trim this down to a more useful dataset..

```python
coffee = coffeeRaw[['Aroma','Flavor', 'Aftertaste', 'Acidity', 'Body', 'Balance',
                     'Total.Cup.Points']].copy()
coffee.head()
```

<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
}

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Aroma</th>
<th>Flavor</th>
<th>Aftertaste</th>
<th>Acidity</th>
<th>Body</th>
<th>Balance</th>
<th>Total.Cup.Points</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>8.67</td>
<td>8.83</td>
<td>8.67</td>
<td>8.75</td>
<td>8.50</td>
<td>8.42</td>
<td>90.58</td>
</tr>
<tr>
<th>1</th>
<td>8.75</td>
<td>8.67</td>
<td>8.50</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>89.92</td>
</tr>
<tr>
<th>2</th>
<td>8.42</td>
<td>8.50</td>
<td>8.42</td>
<td>8.42</td>
<td>8.33</td>
<td>8.42</td>
<td>89.75</td>
</tr>
<tr>
<th>3</th>
<td>8.17</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>8.50</td>
<td>8.25</td>
<td>89.00</td>
</tr>
<tr>
<th>4</th>
<td>8.25</td>
<td>8.50</td>
<td>8.25</td>
<td>8.50</td>
<td>8.42</td>
<td>8.33</td>
<td>88.83</td>
</tr>
</tbody>
</table>
</div>

Much better.

Real quick, let's make sure there's no weirdness in our data.

```python
coffee.info()
coffee.isnull().sum()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1311 entries, 0 to 1310
    Data columns (total 7 columns):
    Aroma               1311 non-null float64
    Flavor              1311 non-null float64
    Aftertaste          1311 non-null float64
    Acidity             1311 non-null float64
    Body                1311 non-null float64
    Balance             1311 non-null float64
    Total.Cup.Points    1311 non-null float64
    dtypes: float64(7)
    memory usage: 71.8 KB
    
    
    
    
    
    Aroma               0
    Flavor              0
    Aftertaste          0
    Acidity             0
    Body                0
    Balance             0
    Total.Cup.Points    0
    dtype: int64

Yay, no blanks!

# Pre-Processing & Basic Analysis

Since all we really want to algorithmically determine is if a certain cup is 'good' or 'bad', let's bin our data into those categories.

```python
#preprocessing into Good/Bad coffee
bins = [-1, 85, 100] #anything scoring 85 or above is good coffee™
labels = ['bad', 'good']
coffee['goodCoffee'] = pd.cut(coffee['Total.Cup.Points'], bins = bins, labels = labels)
coffee = coffee.drop(columns=['Total.Cup.Points'])
coffee['goodCoffee'].unique()
```

    [good, bad]
    Categories (2, object): [bad < good]

```python
coffee['goodCoffee'].value_counts()
```

    bad     1215
    good      96
    Name: goodCoffee, dtype: int64

```python
```

```python
#transform 'good' and 'bad' to 1 & 0
encoder = LabelEncoder()
coffee['goodCoffee'] = encoder.fit_transform(coffee['goodCoffee'])
coffee.head()
```

<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
}

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Aroma</th>
<th>Flavor</th>
<th>Aftertaste</th>
<th>Acidity</th>
<th>Body</th>
<th>Balance</th>
<th>goodCoffee</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>8.67</td>
<td>8.83</td>
<td>8.67</td>
<td>8.75</td>
<td>8.50</td>
<td>8.42</td>
<td>1</td>
</tr>
<tr>
<th>1</th>
<td>8.75</td>
<td>8.67</td>
<td>8.50</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>1</td>
</tr>
<tr>
<th>2</th>
<td>8.42</td>
<td>8.50</td>
<td>8.42</td>
<td>8.42</td>
<td>8.33</td>
<td>8.42</td>
<td>1</td>
</tr>
<tr>
<th>3</th>
<td>8.17</td>
<td>8.58</td>
<td>8.42</td>
<td>8.42</td>
<td>8.50</td>
<td>8.25</td>
<td>1</td>
</tr>
<tr>
<th>4</th>
<td>8.25</td>
<td>8.50</td>
<td>8.25</td>
<td>8.50</td>
<td>8.42</td>
<td>8.33</td>
<td>1</td>
</tr>
</tbody>
</table>
</div>

We can see we have way more bad coffee than good coffee. (Sad)
Let's quickly graph this.

```python
# Plot the data
plt.xkcd()
plt.bar(coffee['goodCoffee'].unique(), coffee['goodCoffee'].value_counts(),
        width=0.75, align='center', color=mcolors.XKCD_COLORS)
plt.xticks([0, 1], ['Good', 'Not Good'])
plt.yticks(coffee['goodCoffee'].value_counts())

plt.gca().spines['top'].set_visible(False)
plt.gca().spines['right'].set_visible(False)

plt.ylabel('# of entries')
plt.title('HOW MUCH OF THIS COFFEE SUCKS?')

plt.show()
```

![png1]({{site.url}}{{site.baseurl}}/assets/images/output_10_0.png)

```python
# and a pie chart
plt.xkcd()
plt.pie(coffee['goodCoffee'].value_counts(), explode=(0, 0.1), labels=(['Not Good', 'Good']), autopct='%1.1f%%',
        shadow=True, startangle=90, colors=mcolors.XKCD_COLORS)
plt.title('HOW MUCH OF THIS COFFEE SUCKS?')

plt.show()
```

![png2](./assets/images/10302019.png)

Finally, let's finish getting our data ready for analysis by splitting it into training/test sets and standardizing the values to remove a bit of bias from the system.

```python
#seperate feature/response vars
X = coffee.drop(columns=['goodCoffee'])
y = coffee['goodCoffee']
#train/test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

```python
#standardize values
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test)
```

# Test the Models

## Random Forest Classifier

```python
#better for mid-size datasets
rfc = RandomForestClassifier(n_estimators = 200)
rfc.fit(X_train, y_train)
pred_rfc = rfc.predict(X_test)
```

```python
#how well did model perform?
print(classification_report(y_test, pred_rfc))
print(confusion_matrix(y_test, pred_rfc))
```

precision    recall  f1-score   support
0       0.98      0.98      0.98       244
1       0.74      0.74      0.74        19
accuracy                           0.96       263
macro avg       0.86      0.86      0.86       263
weighted avg       0.96      0.96      0.96       263

## SVM Classifier

```python
#better for smaller datasets
clf = svm.SVC()
clf.fit(X_train, y_train)
pred_clf = clf.predict(X_test)
```

```python
#how well did model perform?
print(classification_report(y_test, pred_clf))
print(confusion_matrix(y_test, pred_clf))
```

precision    recall  f1-score   support
0       0.98      0.98      0.98       244
1       0.78      0.74      0.76        19
 accuracy                           0.97       263
 macro avg       0.88      0.86      0.87       263
 weighted avg       0.97      0.97      0.97       263

## Neural Network (Multi-Layer Percepitron Classifier)

```python
#better for huge amounts of data
mlpc= MLPClassifier(hidden_layer_sizes=(11, 11, 11), max_iter=500)
mlpc.fit(X_train, y_train)
pred_mlpc = mlpc.predict(X_test)
```

```python
print(classification_report(y_test, pred_mlpc))
print(confusion_matrix(y_test, pred_mlpc))
```

precision    recall  f1-score   support
 0       0.99      0.98      0.98       244
1       0.76      0.84      0.80        19
accuracy                           0.97       263
macro avg       0.87      0.91      0.89       263
weighted avg       0.97      0.97      0.97       263

## What's Best?

```python
from sklearn.metrics import accuracy_score
acc_rfc = accuracy_score(y_test, pred_rfc)
acc_clf = accuracy_score(y_test, pred_clf)
acc_mlpc = accuracy_score(y_test, pred_mlpc)

print(f"Random Forest was {acc_rfc:.2%} accurate")
print(f"SVM was {acc_clf:.2%} accurate")
print(f"Neural Network was {acc_mlpc:.2%} accurate")
```

    Random Forest was 96.20% accurate
    SVM was 96.58% accurate
    Neural Network was 96.96% accurate

All our models preformed about the same, with the neural net just a little bit better than everyone else.
We'll implement that model. This is doubley nice because now we get to say "I implemented a neural network" which sounds very fancy indeed.

# Predicting Future Values

```python
#a reminder what our data looks like
coffee[90:100]
```

<div>
<style scoped>
.dataframe tbody tr th:only-of-type {
vertical-align: middle;
}

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>Aroma</th>
<th>Flavor</th>
<th>Aftertaste</th>
<th>Acidity</th>
<th>Body</th>
<th>Balance</th>
<th>goodCoffee</th>
</tr>
</thead>
<tbody>
<tr>
<th>90</th>
<td>8.42</td>
<td>8.00</td>
<td>7.42</td>
<td>8.00</td>
<td>7.92</td>
<td>7.92</td>
<td>1</td>
</tr>
<tr>
<th>91</th>
<td>7.58</td>
<td>7.83</td>
<td>7.83</td>
<td>7.92</td>
<td>7.83</td>
<td>8.17</td>
<td>1</td>
</tr>
<tr>
<th>92</th>
<td>7.83</td>
<td>8.00</td>
<td>7.75</td>
<td>7.75</td>
<td>7.83</td>
<td>7.83</td>
<td>1</td>
</tr>
<tr>
<th>93</th>
<td>8.08</td>
<td>8.17</td>
<td>7.92</td>
<td>8.00</td>
<td>8.08</td>
<td>8.00</td>
<td>1</td>
</tr>
<tr>
<th>94</th>
<td>7.67</td>
<td>8.00</td>
<td>7.83</td>
<td>8.00</td>
<td>7.92</td>
<td>7.83</td>
<td>1</td>
</tr>
<tr>
<th>95</th>
<td>7.50</td>
<td>7.92</td>
<td>8.25</td>
<td>7.83</td>
<td>7.92</td>
<td>7.75</td>
<td>1</td>
</tr>
<tr>
<th>96</th>
<td>8.17</td>
<td>7.92</td>
<td>7.75</td>
<td>7.75</td>
<td>7.67</td>
<td>7.75</td>
<td>0</td>
</tr>
<tr>
<th>97</th>
<td>8.00</td>
<td>7.92</td>
<td>7.75</td>
<td>7.92</td>
<td>7.75</td>
<td>7.83</td>
<td>0</td>
</tr>
<tr>
<th>98</th>
<td>7.83</td>
<td>8.00</td>
<td>7.58</td>
<td>7.92</td>
<td>7.92</td>
<td>7.83</td>
<td>0</td>
</tr>
<tr>
<th>99</th>
<td>7.83</td>
<td>8.00</td>
<td>7.83</td>
<td>7.75</td>
<td>7.67</td>
<td>7.83</td>
<td>0</td>
</tr>
</tbody>
</table>
</div>

```python
#---------------
#A theoretical cup of coffee
new_Aroma = 8
new_Flavor = 7.5
new_Aftertaste = 8
new_Acidity = 8
new_Body = 7.9
new_Balance = 8
#---------------
```

```python
X_new = [[new_Aroma, new_Flavor, new_Aftertaste, new_Acidity, new_Body, new_Balance]]
X_new = sc.transform(X_new)
y_new = mlpc.predict(X_new)
print(y_new)
if y_new[0] == 1:
    print("it's good!")
else:
    print ("it's not good!")
```

    [1]
    it's good!
