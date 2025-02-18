# datafun-06-eda

This repository is for Project 6 of Data Analytics Fundamentals where we will be using Jupyter Notebook for our own Exploratory Data Analysis.

## How to Install and Run the Project

First you must clone the project to your local machine.

1. Copy the URL of the GitHub Repository you would like
2. Open Powershell and run the following commands

```shell
cd \
cd Projects
git clone https://github.com/**account**/**repo-name**
cd **repo-name**
code . 
```

If .gitignore and/or requirements.txt aren't created, create them.

After creating these files we can now Git add-commit-push using the following code in the terminal

```shell
git add . 
git commit -m "YOUR MESSAGE HERE"
git push -u origin main
```

Once pushed, we now create our virtual environment by running the command:

```shell
py -m venv .venv
```

Now we will activate the virtual environment using this command:

```shell
.venv\Scripts\activate
```

Once the virtual environment has been activated, we can install our dependencies from requirements.txt.

Before installing, it's best to update key packages first.

```shell
py -m pip install --upgrade pip setuptools wheel
py -m pip install -r requirements.txt
```

Lastly, we will select our VS Code Interpreter

1. Press Ctrl+Shift+P
2. Search for "Python: Select Interpreter"
3. Choose the Interpreter for the local .venv 

Now your project is ready and the real fun can begin

Don't forget to regularly Git add-commit-push to keep everything up to date

## Workflow for this Jupyter Notebook

The dataset used for this project is the tips dataset from seaborn.

This dataset contains 7 features that relate to restaurant tips.

[dataset](https://github.com/mwaskom/seaborn-data/blob/master/tips.csv)

**Features:**

1. total_bill
    - The total charge that the diners owe
2. tip
    - The amount the diners tipped
3. sex
    - Sex of the server
4. smoker
    - Whether the server is a smoker
5. day
    - What day of the week the diners visited
6. time
    - What time of day the diners visited
7. size
    - The amount of people dining together

### Step 1

1. Add a Title using Markdown
2. Create a header with the author name, purpose, and date
3. Create a numbered list for imports 
4. Create a Python cell for the import statements

### Step 2

Load data into a pandas Dataframe

Example:

```shell
# Load the Tips dataset into pandas DataFrame
tips_df: pd.DataFrame = sns.load_dataset('tips')

# List column names
tips_df.columns

# Inspect first few rows of the DataFrame
tips_df.head()
```

### Step 3

Initial Data Inspection

After loading the data, it's important to know what we're working with, so we take an initial look at our DataFrame.

Example:

```shell
# Specify the number of rows to display
tips_df.head(10)

# Inspect the shape of the DataFrame with shape attribute
# The shape is a tuple with count of rows and columns in the DataFrame
tips_df.shape

# Inspect the data types of the columns with dtypes attribute
# The data types are returned as a pandas Series
tips_df.dtypes
```

### Step 4

Initial Descriptive Statistics

We now look at the summary statistics by using the DataFrame describe() method.

Example:

```shell
# Inspect summary statistics for numerical columns
tips_df.describe()
```

### Step 5 Part 1

Initial Data Distribution for Numerical Columns

We show some histograms using the hist() method

Example:

```shell
# Inspect histograms for ALL numerical columns
tips_df.hist()

# Show all plots
matplotlib.pyplot.show()
```

### Step 5 Part 2

Initial Data Distribution for Categorical Columns

Now we'll show histograms using the value_counts() method and a loop.

Example:

```shell
# Show value counts of the 'day' column
print(tips_df['day'].value_counts())


# Inspect value counts
for col in tips_df.select_dtypes(include='category').columns:
    sns.countplot(x=col, data=tips_df)
    matplotlib.pyplot.title(f'Distribution of {col}')
    matplotlib.pyplot.show()

#Show all plots
matplotlib.pyplot.show()
```

### Step 6

Initial Data Transformation and Feature Engineering

In this part of the project, columns will be renamed and at least one new column will be created.

Example:
```shell
# Renaming Columns
tips_df.rename(columns={'total_bill': 'Total Bill', 'tip': 'Tip',
                        'day': 'Day of Week', 'sex': 'Sex of Server',
                        'size': 'Number of Diners'}, inplace=True)

# Creating a new column
tips_df['Tip Percentage'] = tips_df['Tip'] / tips_df['Total Bill']
```

### Step 7

Initial Visualizations

In this section we create multiple charts to present the data and give insights based on the outcomes.

Example for a pairplot:
```shell
# Create a pairplot
sns.pairplot(tips_df, hue='Day of Week')

# Show all plots
matplotlib.pyplot.show()
```

Example for a scatterplot:
```shell
# Create a scatter plot
scatter_plt = sns.scatterplot(x='Tip Percentage', y='Number of Diners', data=tips_df)

# Set the title and labels
scatter_plt.set_title('Chart 1. Tip Percentage vs. Number of Diners')
scatter_plt.set_xlabel('Tip Percentage')
scatter_plt.set_ylabel('Number of Diners')

# Show the plot
matplotlib.pyplot.show()
```