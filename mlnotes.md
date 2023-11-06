
## Import packages

pip install pandas
pip install seaborn

import pandas as pd
import seaborn as sns

## read csv - 

df = pd.read_csv("csvfile")

parameters - pd.read_csv("file", .....)

Specify separator: sep = ",", "\t", ..
Give names to headers: names = ["colname1", "colname2", ...]
Get only Selected cols: usecols = ["colname1", "colname2", ...]
Make specific col as index: index_col = 'colname'
Make 1st row as headers: header=0/1
Skip certain rows: skiprows = [rownum1, rownum2...]
Import number of rows: nrows = N
Specify encoding (default is utf-8): encoding="encodingtype"
Skip rows with errors: error_bad_lines=False
Change datatype of column (to save space?): dtype={"colname": datatype}
Treat columns as date values (normally stored as object): parse_dates=["colname", ...]
Convert col values based on function (e.g. abbreviate): def rename(name): if name == "foo": return "bar" else: return name. converters={"colname", rename}
Treat specific values as NA: na_values=["na", "-", ...]
Load dataset in chunks: chunksize=N


-------------
## read json - 

df = pd.read_json("jsonfile")

response = requests.get('url')
df = pd.DataFrame(response.json()['results'])


-------------
## dataframes

get specific cols - df[["colname1", "colname2", ...]]
append - df.append(df1, ignore_index=True)
convert to csv - df.to_csv('csv_name')

kaggle datasets 
rapidapi


## exploratory data analysis

df = pd.read_csv("csvfile")

df = sns.load_dataset('tips')
titanic = pd.read_csv('train.csv')
flights = sns.load_dataset('flights')
iris = sns.load_dataset('iris')

### basic

df.shape
df.info()
df.describe()
df.sample(10)
df.head(5)

cols with null values - df.isnull()		df.isnull().sum()
duplicated rows - df.duplicated()		df.duplicated().sum()
df.corr()		df.corr()['ColName']

### basic

#### average per group

    df.groupby(col1).mean()[col2]

#### sum per group

    df.groupby(col1).sum()[col2]

e.g. percentage of survivors per passenger class (titanic dataset)

    df.groupby('Pclass').mean()['Survived']

### plotting - numerical

#### Bivariate 

    sns.scatterplot(x = dataset[col1], y = dataset[col2])

#### Multivariate

3 vars - Add color

    sns.scatterplot(x = dataset[col1], y = dataset[col2], hue = dataset[col3])

4 vars - add style (represet datapoint as circle vs cross)

    sns.scatterplot(x = dataset[col1], y = dataset[col2], hue = dataset[col3], style = dataset[col4])

5 vars - add size (of dot based on col value)

    sns.scatterplot(x = dataset[col1], y = dataset[col2], hue = dataset[col3], style = dataset[col4], size = data[col5])

### plotting - categorical and numerical

#### Barplot

##### Bivariate 

Show distribution of numerical value (Y) according to categorical value (X)

    sns.barplot(df[col1], df[col2])

##### Multivariate 

3 vars - add color

    sns.barplot(df[col1], df[col2], hue = df[col3])

#### Box Plot

##### Bivariate 

Show distribution of numerical value (Y) according to categorical value (X)

    sns.boxplot(df[col1], df[col2])

##### Multivariate 

3 vars - add color

    sns.boxplot(df[col1], df[col2], hue = df[col3])

#### Distplot - plot the probability distribution function


    sns.distplot(df[col1])
    sns.distplot(df[col1], hist = False) --- to turn off the histogram 

Add a filter to the dataset: 

Choose only those col1 value equal to VAL

    sns.distplot(df[df[col1] = VAL])

### plotting - categorical and categorical

#### Heatmaps

    sns.heatmap(pd.crosstab(df[col1], df[col2]))

#### ClusterMap

    sns.clustermap(pd.crosstab(df[col1], df[col2]))


#### Pairplot

plot scatterplots of all cols of a dataset against each other

    sns.pairplot(df)
    sns.pairplot(df, hue = "col1")

produces a grid of scatterplots

### numerical - numerical 

#### Lineplot

when one of the cols is time-based

    df_new = df.groupby('year').sum()

    ## plot number of passengers per year 

    sns.lineplot(df_new['year'], df_new['passengers'])


### Pivottable

    flights.pivot_table(value='passengers', index = 'month', columns = 'year')

    sns.heatmap(flights.pivot_table(value='passengers', index = 'month', columns = 'year'))

--------

EDA - tool -

pandas profiling

    pip install pandas-profiling

    from pandas_profiling import ProfileReport 
    prof = ProfileReport(df)
    prof.to_file(output_file = 'output.html')


