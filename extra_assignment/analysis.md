# Sleep

In this report, I will analyse the sleep75 dataset. I will focus on sleep data and explore its correlation with other variables from the analysed set.

First, I will import the dataset and convert it into a workable form


```python
import pandas as pd

def read_column_names(txt_path):
    names = []
    with open(txt_path, "r") as f:
        lines = [line.rstrip() for line in f]
    for line in lines[1:]:
        if line.strip().startswith("Obs:"):
            break
        if not line.strip():
            continue
        names.extend(line.split())
    return names

sleep75_cols = read_column_names("SLEEP75_description.txt")
sleep75_df   = pd.read_csv("sleep75.csv", sep=";", header=None, names=sleep75_cols)
```

Our dataset looks like this:


```python
sleep75_df
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
      <th>age</th>
      <th>black</th>
      <th>case</th>
      <th>clerical</th>
      <th>construc</th>
      <th>educ</th>
      <th>earns74</th>
      <th>gdhlth</th>
      <th>inlf</th>
      <th>leis1</th>
      <th>...</th>
      <th>spwrk75</th>
      <th>totwrk</th>
      <th>union</th>
      <th>worknrm</th>
      <th>workscnd</th>
      <th>exper</th>
      <th>yngkid</th>
      <th>yrsmarr</th>
      <th>hrwage</th>
      <th>agesq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>32</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>3529</td>
      <td>...</td>
      <td>0</td>
      <td>3438</td>
      <td>0</td>
      <td>3438</td>
      <td>0</td>
      <td>14</td>
      <td>0</td>
      <td>13</td>
      <td>7,070004</td>
      <td>1024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>31</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>14</td>
      <td>9500</td>
      <td>1</td>
      <td>1</td>
      <td>2140</td>
      <td>...</td>
      <td>0</td>
      <td>5020</td>
      <td>0</td>
      <td>5020</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>1,429999</td>
      <td>961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>17</td>
      <td>42500</td>
      <td>1</td>
      <td>1</td>
      <td>4595</td>
      <td>...</td>
      <td>1</td>
      <td>2815</td>
      <td>0</td>
      <td>2815</td>
      <td>0</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>20,53</td>
      <td>1936</td>
    </tr>
    <tr>
      <th>3</th>
      <td>30</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>12</td>
      <td>42500</td>
      <td>1</td>
      <td>1</td>
      <td>3211</td>
      <td>...</td>
      <td>1</td>
      <td>3786</td>
      <td>0</td>
      <td>3786</td>
      <td>0</td>
      <td>12</td>
      <td>0</td>
      <td>12</td>
      <td>9,619998</td>
      <td>900</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>14</td>
      <td>2500</td>
      <td>1</td>
      <td>1</td>
      <td>4052</td>
      <td>...</td>
      <td>1</td>
      <td>2580</td>
      <td>0</td>
      <td>2580</td>
      <td>0</td>
      <td>44</td>
      <td>0</td>
      <td>33</td>
      <td>2,75</td>
      <td>4096</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>701</th>
      <td>45</td>
      <td>0</td>
      <td>702</td>
      <td>0,182331</td>
      <td>0,030075</td>
      <td>12</td>
      <td>5500</td>
      <td>1</td>
      <td>0</td>
      <td>5069</td>
      <td>...</td>
      <td>1</td>
      <td>2026</td>
      <td>0</td>
      <td>2026</td>
      <td>0</td>
      <td>27</td>
      <td>0</td>
      <td>18</td>
      <td>.</td>
      <td>2025</td>
    </tr>
    <tr>
      <th>702</th>
      <td>34</td>
      <td>0</td>
      <td>703</td>
      <td>0,182331</td>
      <td>0,030075</td>
      <td>10</td>
      <td>2500</td>
      <td>0</td>
      <td>0</td>
      <td>5885</td>
      <td>...</td>
      <td>0</td>
      <td>675</td>
      <td>1</td>
      <td>465</td>
      <td>210</td>
      <td>18</td>
      <td>0</td>
      <td>4</td>
      <td>.</td>
      <td>1156</td>
    </tr>
    <tr>
      <th>703</th>
      <td>37</td>
      <td>0</td>
      <td>704</td>
      <td>0,182331</td>
      <td>0,030075</td>
      <td>12</td>
      <td>3500</td>
      <td>1</td>
      <td>0</td>
      <td>4719</td>
      <td>...</td>
      <td>1</td>
      <td>1851</td>
      <td>0</td>
      <td>1851</td>
      <td>0</td>
      <td>19</td>
      <td>0</td>
      <td>17</td>
      <td>.</td>
      <td>1369</td>
    </tr>
    <tr>
      <th>704</th>
      <td>54</td>
      <td>0</td>
      <td>705</td>
      <td>0,182331</td>
      <td>0,030075</td>
      <td>17</td>
      <td>32500</td>
      <td>1</td>
      <td>0</td>
      <td>5149</td>
      <td>...</td>
      <td>1</td>
      <td>1961</td>
      <td>1</td>
      <td>1481</td>
      <td>480</td>
      <td>31</td>
      <td>0</td>
      <td>22</td>
      <td>.</td>
      <td>2916</td>
    </tr>
    <tr>
      <th>705</th>
      <td>30</td>
      <td>0</td>
      <td>706</td>
      <td>0,182331</td>
      <td>0,030075</td>
      <td>16</td>
      <td>6750</td>
      <td>1</td>
      <td>0</td>
      <td>4747</td>
      <td>...</td>
      <td>0</td>
      <td>2363</td>
      <td>0</td>
      <td>2363</td>
      <td>0</td>
      <td>8</td>
      <td>1</td>
      <td>9</td>
      <td>.</td>
      <td>900</td>
    </tr>
  </tbody>
</table>
<p>706 rows × 34 columns</p>
</div>



We can see many columns with ambiguous names - I'll paste their exact meaning below. Some of the data is missing, some of it has an unsuitable datatype. In next steps, I will clean and impute some data.

### Meaning of columns in sleep75_df:

This dataframe shows statistics for 1975

1. age -                     in years
2. black -                   = 1 if black
3. case -                    identifier
4. clerical -                 = 1 if clerical worker
5. construc -                = 1 if construction worker
6. educ -                    years of schooling
7. earns74 -                  total earnings, 1974
8. gdhlth -                   = 1 if in good or excellent health
9. inlf -                    = 1 if in labor force
10. leis1 -                  sleep - totwrk
11. leis2 -                  slpnaps - totwrk
12. leis3 -                  rlxall - totwrk
13. smsa -                   = 1 if live in smsa
14. lhrwage -                 log hourly wage
15. lothinc -                log othinc, unless othinc < 0
16. male -                   = 1 if male
17. marr -                    = 1 if married
18. prot -                    = 1 if Protestant
19. rlxall -                  slpnaps + personal activs
20. selfe -                   = 1 if self employed
21. sleep -                  mins sleep at night, per week
22. slpnaps -                 mins sleep, including naps, per week
23. south -                  = 1 if live in south
24. spsepay -                spousal wage income
25. spwrk75 -                = 1 if spouse works
26. totwrk -                 mins worked per week
27. union -                  = 1 if belong to union
28. worknrm -                mins work main job
29. workscnd -               mins work second job
30. exper -                  age - educ - 6
31. yngkid -                 = 1 if children < 3 present
32. yrsmarr -                years married
33. hrwage -                 hourly wage
34. agesq -                  age^2



```python
sleep75_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 706 entries, 0 to 705
    Data columns (total 34 columns):
     #   Column    Non-Null Count  Dtype 
    ---  ------    --------------  ----- 
     0   age       706 non-null    int64 
     1   black     706 non-null    int64 
     2   case      706 non-null    int64 
     3   clerical  706 non-null    object
     4   construc  706 non-null    object
     5   educ      706 non-null    int64 
     6   earns74   706 non-null    int64 
     7   gdhlth    706 non-null    int64 
     8   inlf      706 non-null    int64 
     9   leis1     706 non-null    int64 
     10  leis2     706 non-null    int64 
     11  leis3     706 non-null    int64 
     12  smsa      706 non-null    int64 
     13  lhrwage   706 non-null    object
     14  lothinc   706 non-null    object
     15  male      706 non-null    int64 
     16  marr      706 non-null    int64 
     17  prot      706 non-null    int64 
     18  rlxall    706 non-null    int64 
     19  selfe     706 non-null    int64 
     20  sleep     706 non-null    int64 
     21  slpnaps   706 non-null    int64 
     22  south     706 non-null    int64 
     23  spsepay   706 non-null    int64 
     24  spwrk75   706 non-null    int64 
     25  totwrk    706 non-null    int64 
     26  union     706 non-null    int64 
     27  worknrm   706 non-null    int64 
     28  workscnd  706 non-null    int64 
     29  exper     706 non-null    int64 
     30  yngkid    706 non-null    int64 
     31  yrsmarr   706 non-null    int64 
     32  hrwage    706 non-null    object
     33  agesq     706 non-null    int64 
    dtypes: int64(29), object(5)
    memory usage: 187.7+ KB


We can see that some columns that should have a numeric datatype have an 'object' data type. I'll convert them to actual floats


```python
float_columns1 = ['lhrwage', 'hrwage', 'lothinc']

df_fixed = sleep75_df.copy()
for col in float_columns1:
    s = df_fixed[col].astype(str).str.replace(',', '.', regex=False)
    df_fixed[col] = pd.to_numeric(s, errors='coerce')

for col in df_fixed.columns:
    if df_fixed[col].dtype == 'object':
        df_fixed[col] = pd.to_numeric(df_fixed[col], errors='coerce')

negative_counts = (df_fixed < 0).sum() # only lhrwage contains negative values, likely because hrwage was between 0 and 1, which is why I won't be changing that

min_cols = ['leis1', 'leis2', 'leis3', 'rlxall', 'sleep', 'slpnaps', 'totwrk', 'worknrm', 'workscnd']

for col in min_cols:
    df_fixed[col] = (df_fixed[col] / 60).round(2) # converting mins per week to hours per week


```

Then I'll check for negative values. We can see that only lhrwage contains negative values, likely because hrwage was between 0 and 1, which is why I won't be changing that.


```python
negative_counts = (df_fixed < 0).sum() 
print(negative_counts)
```

    age          0
    black        0
    case         0
    clerical     0
    construc     0
    educ         0
    earns74      0
    gdhlth       0
    inlf         0
    leis1        0
    leis2        0
    leis3        0
    smsa         0
    lhrwage     10
    lothinc      0
    male         0
    marr         0
    prot         0
    rlxall       0
    selfe        0
    sleep        0
    slpnaps      0
    south        0
    spsepay      0
    spwrk75      0
    totwrk       0
    union        0
    worknrm      0
    workscnd     0
    exper        0
    yngkid       0
    yrsmarr      0
    hrwage       0
    agesq        0
    dtype: int64


We can see that the hourly wage data for some of the workers is missing, due to the fact that they do not work. For the sake of the analysis, I will create a separate dataframe for workers only, where I will drop the rows with missing values for this column. But first, I will convert some of the numeric columns to booleans.


```python
bool_columns1 = ['black', 'clerical', 'construc', 'gdhlth', 'inlf', 'smsa', 'male', 'marr', 'prot', 'selfe', 'south', 'spwrk75', 'union', 'yngkid']
df_bool = df_fixed.copy()
for col in bool_columns1 :
    df_bool[col] = (df_bool[col] == 1)
```


```python
df_copy = df_bool.copy()
df_workers = df_copy.dropna()
```

Our dataset for workers now looks like this.


```python
df_workers
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
      <th>age</th>
      <th>black</th>
      <th>case</th>
      <th>clerical</th>
      <th>construc</th>
      <th>educ</th>
      <th>earns74</th>
      <th>gdhlth</th>
      <th>inlf</th>
      <th>leis1</th>
      <th>...</th>
      <th>spwrk75</th>
      <th>totwrk</th>
      <th>union</th>
      <th>worknrm</th>
      <th>workscnd</th>
      <th>exper</th>
      <th>yngkid</th>
      <th>yrsmarr</th>
      <th>hrwage</th>
      <th>agesq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>32</td>
      <td>False</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>0</td>
      <td>False</td>
      <td>True</td>
      <td>58.82</td>
      <td>...</td>
      <td>False</td>
      <td>57.30</td>
      <td>False</td>
      <td>57.30</td>
      <td>0.0</td>
      <td>14</td>
      <td>False</td>
      <td>13</td>
      <td>7.070004</td>
      <td>1024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>31</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>14</td>
      <td>9500</td>
      <td>True</td>
      <td>True</td>
      <td>35.67</td>
      <td>...</td>
      <td>False</td>
      <td>83.67</td>
      <td>False</td>
      <td>83.67</td>
      <td>0.0</td>
      <td>11</td>
      <td>False</td>
      <td>0</td>
      <td>1.429999</td>
      <td>961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>False</td>
      <td>17</td>
      <td>42500</td>
      <td>True</td>
      <td>True</td>
      <td>76.58</td>
      <td>...</td>
      <td>True</td>
      <td>46.92</td>
      <td>False</td>
      <td>46.92</td>
      <td>0.0</td>
      <td>21</td>
      <td>False</td>
      <td>0</td>
      <td>20.530000</td>
      <td>1936</td>
    </tr>
    <tr>
      <th>3</th>
      <td>30</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>42500</td>
      <td>True</td>
      <td>True</td>
      <td>53.52</td>
      <td>...</td>
      <td>True</td>
      <td>63.10</td>
      <td>False</td>
      <td>63.10</td>
      <td>0.0</td>
      <td>12</td>
      <td>False</td>
      <td>12</td>
      <td>9.619998</td>
      <td>900</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>False</td>
      <td>14</td>
      <td>2500</td>
      <td>True</td>
      <td>True</td>
      <td>67.53</td>
      <td>...</td>
      <td>True</td>
      <td>43.00</td>
      <td>False</td>
      <td>43.00</td>
      <td>0.0</td>
      <td>44</td>
      <td>False</td>
      <td>33</td>
      <td>2.750000</td>
      <td>4096</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>527</th>
      <td>26</td>
      <td>False</td>
      <td>528</td>
      <td>False</td>
      <td>False</td>
      <td>10</td>
      <td>10500</td>
      <td>True</td>
      <td>True</td>
      <td>65.25</td>
      <td>...</td>
      <td>True</td>
      <td>45.00</td>
      <td>False</td>
      <td>45.00</td>
      <td>0.0</td>
      <td>10</td>
      <td>True</td>
      <td>11</td>
      <td>11.550010</td>
      <td>676</td>
    </tr>
    <tr>
      <th>528</th>
      <td>27</td>
      <td>False</td>
      <td>529</td>
      <td>False</td>
      <td>False</td>
      <td>14</td>
      <td>1000</td>
      <td>True</td>
      <td>True</td>
      <td>110.33</td>
      <td>...</td>
      <td>True</td>
      <td>0.00</td>
      <td>False</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>7</td>
      <td>False</td>
      <td>0</td>
      <td>1.390000</td>
      <td>729</td>
    </tr>
    <tr>
      <th>529</th>
      <td>23</td>
      <td>False</td>
      <td>530</td>
      <td>True</td>
      <td>False</td>
      <td>12</td>
      <td>1000</td>
      <td>True</td>
      <td>True</td>
      <td>112.00</td>
      <td>...</td>
      <td>True</td>
      <td>0.00</td>
      <td>False</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>5</td>
      <td>False</td>
      <td>6</td>
      <td>2.890002</td>
      <td>529</td>
    </tr>
    <tr>
      <th>530</th>
      <td>62</td>
      <td>False</td>
      <td>531</td>
      <td>False</td>
      <td>False</td>
      <td>1</td>
      <td>1000</td>
      <td>False</td>
      <td>True</td>
      <td>103.62</td>
      <td>...</td>
      <td>False</td>
      <td>0.00</td>
      <td>False</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>55</td>
      <td>False</td>
      <td>43</td>
      <td>1.920000</td>
      <td>3844</td>
    </tr>
    <tr>
      <th>531</th>
      <td>39</td>
      <td>False</td>
      <td>532</td>
      <td>True</td>
      <td>False</td>
      <td>17</td>
      <td>42500</td>
      <td>True</td>
      <td>True</td>
      <td>116.25</td>
      <td>...</td>
      <td>True</td>
      <td>0.00</td>
      <td>False</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>16</td>
      <td>False</td>
      <td>18</td>
      <td>2.309999</td>
      <td>1521</td>
    </tr>
  </tbody>
</table>
<p>532 rows × 34 columns</p>
</div>



And our regular dataset looks like this.


```python
df_bool
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
      <th>age</th>
      <th>black</th>
      <th>case</th>
      <th>clerical</th>
      <th>construc</th>
      <th>educ</th>
      <th>earns74</th>
      <th>gdhlth</th>
      <th>inlf</th>
      <th>leis1</th>
      <th>...</th>
      <th>spwrk75</th>
      <th>totwrk</th>
      <th>union</th>
      <th>worknrm</th>
      <th>workscnd</th>
      <th>exper</th>
      <th>yngkid</th>
      <th>yrsmarr</th>
      <th>hrwage</th>
      <th>agesq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>32</td>
      <td>False</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>0</td>
      <td>False</td>
      <td>True</td>
      <td>58.82</td>
      <td>...</td>
      <td>False</td>
      <td>57.30</td>
      <td>False</td>
      <td>57.30</td>
      <td>0.0</td>
      <td>14</td>
      <td>False</td>
      <td>13</td>
      <td>7.070004</td>
      <td>1024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>31</td>
      <td>False</td>
      <td>2</td>
      <td>False</td>
      <td>False</td>
      <td>14</td>
      <td>9500</td>
      <td>True</td>
      <td>True</td>
      <td>35.67</td>
      <td>...</td>
      <td>False</td>
      <td>83.67</td>
      <td>False</td>
      <td>83.67</td>
      <td>0.0</td>
      <td>11</td>
      <td>False</td>
      <td>0</td>
      <td>1.429999</td>
      <td>961</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>False</td>
      <td>3</td>
      <td>False</td>
      <td>False</td>
      <td>17</td>
      <td>42500</td>
      <td>True</td>
      <td>True</td>
      <td>76.58</td>
      <td>...</td>
      <td>True</td>
      <td>46.92</td>
      <td>False</td>
      <td>46.92</td>
      <td>0.0</td>
      <td>21</td>
      <td>False</td>
      <td>0</td>
      <td>20.530000</td>
      <td>1936</td>
    </tr>
    <tr>
      <th>3</th>
      <td>30</td>
      <td>False</td>
      <td>4</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>42500</td>
      <td>True</td>
      <td>True</td>
      <td>53.52</td>
      <td>...</td>
      <td>True</td>
      <td>63.10</td>
      <td>False</td>
      <td>63.10</td>
      <td>0.0</td>
      <td>12</td>
      <td>False</td>
      <td>12</td>
      <td>9.619998</td>
      <td>900</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
      <td>False</td>
      <td>5</td>
      <td>False</td>
      <td>False</td>
      <td>14</td>
      <td>2500</td>
      <td>True</td>
      <td>True</td>
      <td>67.53</td>
      <td>...</td>
      <td>True</td>
      <td>43.00</td>
      <td>False</td>
      <td>43.00</td>
      <td>0.0</td>
      <td>44</td>
      <td>False</td>
      <td>33</td>
      <td>2.750000</td>
      <td>4096</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>701</th>
      <td>45</td>
      <td>False</td>
      <td>702</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>5500</td>
      <td>True</td>
      <td>False</td>
      <td>84.48</td>
      <td>...</td>
      <td>True</td>
      <td>33.77</td>
      <td>False</td>
      <td>33.77</td>
      <td>0.0</td>
      <td>27</td>
      <td>False</td>
      <td>18</td>
      <td>NaN</td>
      <td>2025</td>
    </tr>
    <tr>
      <th>702</th>
      <td>34</td>
      <td>False</td>
      <td>703</td>
      <td>False</td>
      <td>False</td>
      <td>10</td>
      <td>2500</td>
      <td>False</td>
      <td>False</td>
      <td>98.08</td>
      <td>...</td>
      <td>False</td>
      <td>11.25</td>
      <td>True</td>
      <td>7.75</td>
      <td>3.5</td>
      <td>18</td>
      <td>False</td>
      <td>4</td>
      <td>NaN</td>
      <td>1156</td>
    </tr>
    <tr>
      <th>703</th>
      <td>37</td>
      <td>False</td>
      <td>704</td>
      <td>False</td>
      <td>False</td>
      <td>12</td>
      <td>3500</td>
      <td>True</td>
      <td>False</td>
      <td>78.65</td>
      <td>...</td>
      <td>True</td>
      <td>30.85</td>
      <td>False</td>
      <td>30.85</td>
      <td>0.0</td>
      <td>19</td>
      <td>False</td>
      <td>17</td>
      <td>NaN</td>
      <td>1369</td>
    </tr>
    <tr>
      <th>704</th>
      <td>54</td>
      <td>False</td>
      <td>705</td>
      <td>False</td>
      <td>False</td>
      <td>17</td>
      <td>32500</td>
      <td>True</td>
      <td>False</td>
      <td>85.82</td>
      <td>...</td>
      <td>True</td>
      <td>32.68</td>
      <td>True</td>
      <td>24.68</td>
      <td>8.0</td>
      <td>31</td>
      <td>False</td>
      <td>22</td>
      <td>NaN</td>
      <td>2916</td>
    </tr>
    <tr>
      <th>705</th>
      <td>30</td>
      <td>False</td>
      <td>706</td>
      <td>False</td>
      <td>False</td>
      <td>16</td>
      <td>6750</td>
      <td>True</td>
      <td>False</td>
      <td>79.12</td>
      <td>...</td>
      <td>False</td>
      <td>39.38</td>
      <td>False</td>
      <td>39.38</td>
      <td>0.0</td>
      <td>8</td>
      <td>True</td>
      <td>9</td>
      <td>NaN</td>
      <td>900</td>
    </tr>
  </tbody>
</table>
<p>706 rows × 34 columns</p>
</div>



We'll use the first one to analyse the statistics related to workers and the second one for other statistics.

Let's first plot the matrix of correlations between the variables. We will exclude binary columns, as they are not conducive in this case


```python
import matplotlib.pyplot as plt 
import seaborn as sns

binary_cols = [
    col for col in df_workers.columns 
    if set(df_workers[col].dropna().unique()) <= {0, 1}
]

df_no_binary = df_workers.drop(columns=binary_cols)

corr = df_no_binary.corr(numeric_only=True)
plt.figure(figsize=(12, 9))
sns.heatmap(corr, 
            annot=False,     
            fmt=".2f",          
            cmap="coolwarm",    
            vmin=-1, vmax=1,  
            square=True,       
            linewidths=0.5,     
            cbar_kws={"shrink": .75})  

plt.title("Correlation Heatmap", fontsize=16)
plt.tight_layout()
plt.show()
```


    
![png](analysis_files/analysis_20_0.png)
    


We can see that sleep has the highest correlation with rlxall and slpnaps - which makes sense, as these two parameters were calculated using i.e. sleep time.
Otherwise, the highest correlation coefficient seems to be with totwrk and worknrm. Let's plot it and calculate the precise correlation coefficient.


```python
import scipy.stats as ss 

plt.scatter(df_workers['totwrk'], df_workers['sleep'])
plt.xlabel("Total work time per week [h]")
plt.ylabel("Total sleep time per week [h]")
plt.show()

correlation1 = ss.pearsonr(df_workers['sleep'], df_workers['totwrk'])
print(correlation1)
```


    
![png](analysis_files/analysis_22_0.png)
    


    PearsonRResult(statistic=np.float64(-0.3240050961145081), pvalue=np.float64(1.8117963160130172e-14))


The pearson's correlation coefficient is -0.32, which means the relation is weak and negative. Let's plot the second relation:


```python
plt.scatter(df_workers['worknrm'], df_workers['sleep'])
plt.xlabel("Total time spent in main job per week [h]")
plt.ylabel("Total sleep time per week [h]")
plt.show()

correlation2 = ss.pearsonr(df_workers['sleep'], df_workers['worknrm'])
print(correlation2)
```


    
![png](analysis_files/analysis_24_0.png)
    


    PearsonRResult(statistic=np.float64(-0.3230844048281091), pvalue=np.float64(2.1671390472366313e-14))


It makes sense that this plot is very similar to the first one, as total work and time spent in the main job are tightly correlated. We will focus only on the first one.  

Let's now examine the sleep vs hrwage relationship


```python
plt.scatter(df_workers['hrwage'], df_workers['sleep'])
plt.xlabel("Hourly wage")
plt.ylabel("Total sleep time per week [h]")
plt.show()

correlation3 = ss.pearsonr(df_workers['sleep'], df_workers['hrwage'])
print(correlation3)
```


    
![png](analysis_files/analysis_26_0.png)
    


    PearsonRResult(statistic=np.float64(-0.04945278601973278), pvalue=np.float64(0.254849788487443))


The relationship is close to 0 - the majority of people earns low wages, which makes it difficult to capture the relationship. Transforming hrwage, i.e. logarithmically, might make the relationship more visible. We already have such a column in our dataframe.


```python
plt.scatter(df_workers['lhrwage'], df_workers['sleep'])
plt.xlabel("Log hourly wage")
plt.ylabel("Total sleep time per week [h]")
plt.show()

correlation4 = ss.pearsonr(df_workers['sleep'], df_workers['lhrwage'])
print(correlation4)
```


    
![png](analysis_files/analysis_28_0.png)
    


    PearsonRResult(statistic=np.float64(-0.06721500528164952), pvalue=np.float64(0.12151943563002233))


We only stretched out the data, but it did not increase the linearity of our plot. This means that there is no clear trend between how much a person earns and how long it sleeps.   
I will now create a model, in which total work will be an explanatory variable and sleep will be a response variable.


```python
import statsmodels.formula.api as smf

model = smf.ols(formula="sleep ~ totwrk", data=df_workers).fit()

print(model.summary())

```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  sleep   R-squared:                       0.105
    Model:                            OLS   Adj. R-squared:                  0.103
    Method:                 Least Squares   F-statistic:                     62.17
    Date:                Mon, 02 Jun 2025   Prob (F-statistic):           1.81e-14
    Time:                        19:32:27   Log-Likelihood:                -1773.8
    No. Observations:                 532   AIC:                             3552.
    Df Residuals:                     530   BIC:                             3560.
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     59.7109      0.744     80.240      0.000      58.249      61.173
    totwrk        -0.1496      0.019     -7.884      0.000      -0.187      -0.112
    ==============================================================================
    Omnibus:                       14.534   Durbin-Watson:                   1.918
    Prob(Omnibus):                  0.001   Jarque-Bera (JB):               27.022
    Skew:                          -0.119   Prob(JB):                     1.36e-06
    Kurtosis:                       4.078   Cond. No.                         99.0
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.


The model that we got looks like this: y = 59.7109 - 0.1496x 

Let's display the diagnostic plot for this variable


```python
import statsmodels.api as sm

fig = plt.figure(figsize=(12, 10))
sm.graphics.plot_regress_exog(model, 'totwrk', fig=fig)
plt.show()
```


    
![png](analysis_files/analysis_32_0.png)
    


The first plot confirms that there is a slight negative correlation between sleep and totwrk - it makes sense that those who work more have less time to sleep and vice versa.  
The second plot does not reveal any pattern - the scatter is rather random, which means that the simple linear line from the first graph captures most of that relationship accurately.  
The third and fourth plot show that when we take away the effect of other predictors, we'll still see a downward slope.

Let's see the outliers now:


```python
fig, ax = plt.subplots(figsize=(16, 12))
sm.graphics.influence_plot(model, ax=ax, criterion="cooks")
plt.title("Influence Plot (Outliers and High Leverage Points)")
plt.show()
```


    
![png](analysis_files/analysis_35_0.png)
    


Almost all observations have very low leverage (hᵢᵢ < 0.01). It means that most cases lie near the “typical” range of total work hours, so they do not individually pull the regression line much.  
The dot with 10 has disproportionate effect on the regression line and its studentized residual is around -2 / -3, so it is 2-3 standard deviations below what the model would predict.  
This plot suggests that dots like 10 or 242 might be outliers.

I will also examine the relationship between total sleep and each binary (0/1) variable in our dataset. To pick the most interesting candidate for the analysis, I computed a point-biserial correlation between “sleep” and every 0/1 column, then sorted by the absolute value of that correlation.  
I will use the dataset df_bool, which contained all cases, not just working people, as this analysis can be extended to the entire sample.


```python
from scipy.stats import pointbiserialr

scores = []
for b in binary_cols:
    r, p = pointbiserialr(df_bool[b], df_bool["sleep"])
    scores.append((b, r, p))

# Convert to a DataFrame so we can sort by |r|
import pandas as pd
results = pd.DataFrame(scores, columns=["binary_col", "r_pb", "p_value"])
results["abs_r"] = results["r_pb"].abs()
results = results.sort_values("abs_r", ascending=False)

print(results.head(5))

```

       binary_col      r_pb   p_value     abs_r
    3      gdhlth -0.102856  0.006231  0.102856
    10      south  0.078592  0.036819  0.078592
    5        smsa -0.067009  0.075187  0.067009
    7        marr  0.053774  0.153489  0.053774
    1    clerical  0.040592  0.281440  0.040592


'Good health' is the variable with the highest correlation to sleep - let's visualise it with a boxplot


```python
sns.boxplot(
    x="gdhlth",  
    y="sleep",              
    data=df_bool,                
    palette=["lightblue", "lightgreen"] 
);

# Label the axes
plt.xlabel("In Good Health");
plt.ylabel("Total Sleep Time per Week (Hours)");
plt.title("Box‐plot of sleep by health");
plt.show();
```

    /var/folders/x0/x7cf__n51m5g22m9ltzp4k4h0000gn/T/ipykernel_21692/1102341910.py:1: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(



    
![png](analysis_files/analysis_40_1.png)
    


We see that the subset of people in good health contains many outliers. Let's get rid of them and then calculate some basic statistics for these two subsets:


```python
import numpy as np 

df_badhealth = df_bool[df_bool['gdhlth'] == 0]
df_goodhealth = df_bool[df_bool['gdhlth'] == 1]

Q1 = df_goodhealth["sleep"].quantile(0.25)
Q3 = df_goodhealth["sleep"].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

df_gh_no_outliers = df_goodhealth.loc[
    (df_goodhealth["sleep"] >= lower_bound) & (df_goodhealth["sleep"] <= upper_bound)
].copy()
```

For those in bad health:


```python
median_b = np.median(df_badhealth['sleep'])
mean_b = np.mean(df_badhealth['sleep'])
std_b = np.std(df_badhealth['sleep'])

print("For those in bad health: mean - " + str(mean_b) + ", sd - " + str(std_b) +", median - " + str(median_b))
```

    For those in bad health: mean - 56.6148051948052, sd - 8.098348334152572, median - 56.97


And for those in good health:


```python
median_g = np.median(df_gh_no_outliers['sleep'])
mean_g = np.mean(df_gh_no_outliers['sleep'])
std_g = np.std(df_gh_no_outliers['sleep'])

print("For those in good health: mean - " + str(mean_g) + ", sd - " + str(std_g) +", median - " + str(median_g))
```

    For those in good health: mean - 54.35843648208469, sd - 6.284119597758276, median - 54.25


For both groups, the median and mean are similar to one another.  
For those in good health, both median and mean are two hours lower than for those in bad health.  
The standard deviation is higher for people in bad health, which suggests their sleep patterns are slightly more spread than of those with good health.  
However, statistics and boxplots for both groups are very similar, so this variable is not a definite factor which determines how long people sleep per week.

## Conclusions

I started by cleaning our dataset. I ended up with a dataset that contained only workers as well as a set that contained all cases.
I analysed the influence of total work, hourly wage and health on total sleep time per week, using our workers' dataset. 
The correlation between total work and sleep turned out to be weak and negative, but it displayed the general trend that the more you work, the less you sleep.  
There was no correlation between neither hourly wage nor logarithmic hourly wage and sleep, so this parameter was not used in our model.  
Finally, out of all 0/1 variables we had, 'good health' turned out to have the largest point-biserial correlation with sleep. I used a set with all cases for this analysis. People in good health turned to sleep slightly shorter and their patterns were less spread out, but this value is not high enough to extrapolate and draw definite conclusions. 
