---
interact_link: content/notebooks/04-python/04-intro-python-groupby.ipynb
kernel_name: python3
has_widgets: false
title: 'Groupby and Pivot Tables'
prev_page:
  url: /notebooks/04-python/03-intro-python-null-values.html
  title: 'Null Values'
next_page:
  url: /notebooks/04-python/05-intro-kaggle-baseline.html
  title: 'Kaggle Baseline'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---


[![AnalyticsDojo](https://github.com/rpi-techfundamentals/spring2019-materials/blob/master/fig/final-logo.png?raw=1)](http://rpi.analyticsdojo.com)
<center><h1>Introduction to Python - Groupby and Pivot Tables</h1></center>
<center><h3><a href = 'http://rpi.analyticsdojo.com'>rpi.analyticsdojo.com</a></h3></center>






<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
!wget https://raw.githubusercontent.com/rpi-techfundamentals/spring2019-materials/master/input/train.csv
!wget https://raw.githubusercontent.com/rpi-techfundamentals/spring2019-materials/master/input/test.csv

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
import numpy as np 
import pandas as pd 

# Input data files are available in the "../input/" directory.
# Let's input them into a Pandas DataFrame
train = pd.read_csv("train.csv")
test  = pd.read_csv("test.csv")

```
</div>

</div>



### Groupby
- Often it is useful to see statistics by different classes.
- Can be used to examine different subpopulations



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
train.head()

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
print(train.dtypes)

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#What does this tell us?  
train.groupby(['Sex']).Survived.mean()

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#What does this tell us?  
train.groupby(['Sex','Pclass']).Survived.mean()

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#What does this tell us?  Here it doesn't look so clear. We could separate by set age ranges.
train.groupby(['Sex','Age']).Survived.mean()

```
</div>

</div>



### Combining Multiple Operations
- *Splitting* the data into groups based on some criteria
- *Applying* a function to each group independently
- *Combining* the results into a data structure



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
s = train.groupby(['Sex','Pclass'], as_index=False).Survived.sum()
s['PerSurv'] = train.groupby(['Sex','Pclass'], as_index=False).Survived.mean().Survived
s['PerSurv']=s['PerSurv']*100
s['Count'] = train.groupby(['Sex','Pclass'], as_index=False).Survived.count().Survived
survived =s.Survived
s

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#What does this tell us?  
spmean=train.groupby(['Sex','Pclass']).Survived.mean()
spcount=train.groupby(['Sex','Pclass']).Survived.sum()
spsum=train.groupby(['Sex','Pclass']).Survived.count()
spsum

```
</div>

</div>



### Pivot Tables
- A pivot table is a data summarization tool, much easier than the syntax of groupBy. 
- It can be used to that sum, sort, averge, count, over a pandas dataframe. 
- Download and open data in excel to appreciate the ways that you can use Pivot Tables. 



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#Load it and create a pivot table.
from google.colab import files
files.download('train.csv')

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
#List the index and the functions you want to aggregage by. 
pd.pivot_table(train,index=["Sex","Pclass"],values=["Survived"],aggfunc=['count','sum','mean',])

```
</div>

</div>
