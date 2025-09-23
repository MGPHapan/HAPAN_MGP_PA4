## HAPAN_MGP_PA4


### ECE Board Exam Problem 1

1) A Python script that shows a data frame provided: Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon.

**We start by importing the Pandas library and loading the dataset board2.csv.**
- Use Pandas as it allows us to store tabular data in a DataFrame.
- Use .read_csv() since our dataset is in CSV format, we need this function to read it into Python as a DataFrame.
- Output: A table showing all the rows and columns in the dataset.

```Python
import pandas as pd                # Import pandas from the library

board = pd.read_csv('board2.csv')  # Loads the 'board2.csv' file into a DataFrame
board                              # Displays the dataset
```

**Creating the Instru DataFrame**
- We need to create Instru so that we can focus only on students from the Instrumentation track, with hometown = Luzon, and Electronics > 70. This helps us filter out only the qualified students based on the given conditions.
- We use .loc[] because it lets us filter rows by applying multiple conditions at once (Track, Hometown, Electronics).
- We only display the columns Name, GEAS, Electronics because the problem requires us to highlight the identity of the student (Name), one subject (GEAS), and the qualified score (Electronics).
- Output: A DataFrame of Instrumentation students from Luzon with Electronics > 70, showing only Name, GEAS, and Electronics.

```Python
Instru = board.loc[(board['Track'] == 'Instrumentation') &          # Rows where Track = Instrumentation
                   (board['Hometown'] == 'Luzon') &                 # Rows where Hometown = Luzon
                   (board['Electronics']>70),                       # Rows where Electronics score > 70
                   ['Name', 'GEAS', 'Electronics']]                 # Display only the Name, GEAS, and Electronics columns
Instru = Instru.rename(columns={'Electronics': 'Electronics >70'})  # Rename the Electronics column to Electronics >70
Instru                                                              # Display the DataFrame
```

**Adding the Average Column**
- We need to add an Average column so we can calculate each student’s overall performance across all subjects.
- We use .mean(axis=1) to compute the row-wise mean, since each row represents one student.
- We include Math, GEAS, Electronics, and Communication in the calculation because these are the four exam subjects.
  Output: A new column Average is added to the dataset.
```Python
board['Average'] = board[['Math', 'GEAS', 'Electronics','Communication']].mean(axis=1)  # Add new column 'Average' as mean score per student
board                                                                                   # Display dataset
```

**Creating the Mindy DataFrame**
- We need to create Mindy so we can focus only on Female students from Mindanao with an Average ≥ 55.
- We use .loc[] to filter based on Gender, Hometown, and Average simultaneously.
- We keep the columns Name, Track, Electronics, Average to show student identity, program, one subject score, and overall performance.
- We use .rename() to change the column name from "Average" to "Average ≥55" for clarity.
- Output: A DataFrame of Female students from Mindanao with Average ≥ 55.
```Python
Mindy = board.loc[(board['Gender'] == 'Female') &               # Rows where Gender = Female
                (board['Hometown'] == 'Mindanao') &             # Rows where Hometown = Mindanao  
                (board['Average'] >= 55),                       # Rows where Average score is ≥ 55
                ['Name', 'Track', 'Electronics', 'Average']]    # Display only Name, Track, Electronics, Average
Mindy = Mindy.rename(columns={'Average': 'Average >=55'})       # Rename Average column
Mindy                                                           # Display the DataFrame
```

2) Using Python script, we create a visualization that shows how the different features contributes to average grade

**Importing Matplotlib**
- We need to import Matplotlib because it allows us to create plots and graphs in Python.
- Specifically, we use pyplot (as plt) for generating bar charts of average scores.
```Python
import matplotlib.pyplot as plt  #Import matplotlib for visualization
```

**Visualization 1: Average Scores by Track**
- We need .groupby('Track') to group students by their Track.
- We use .mean() on the Average column to calculate the mean score per Track.
- We plot the results as a bar chart to compare Track performance visually.
- Output: A bar chart showing the average scores of students grouped by Track.
```Python
track_avg = board.groupby('Track')['Average'].mean()  # Group students by Track and compute average score

plt.figure(figsize=(8,5))             # Set the size of the figure
track_avg.plot(kind="bar")            # Plot the grouped data as a bar chart
plt.title('Average Scores by Track')  # Add title to the chart
plt.ylabel('Average Score')           # Label the y-axis
plt.xlabel('Track')                   # Label the x-axis
plt.xticks(rotation=-25)              # Rotate x-axis labels for readability
plt.show()                            # Display the chart
```

**Visualization 2: Average Scores by Gender**
- We need .groupby('Gender') to separate students into Male and Female categories.
- We use .mean() on the Average column to calculate mean scores for each gender.
- We plot a bar chart so that differences between Male and Female performance can be seen clearly.
- Output: A bar chart showing the average scores of Male and Female students.

```Python
track_avg = board.groupby('Gender')['Average'].mean() # Group students by Gender and compute average score
    
plt.figure(figsize=(8,5))                 # Set the size of the figure
track_avg.plot(kind="bar")                # Plot the grouped data as a bar chart
plt.title('Average Scores by Gender')     # Add title to the chart
plt.ylabel('Average Score')               # Label the y-axis
plt.xlabel('Gender')                      # Label the x-axis
plt.xticks(rotation=-25)                  # Rotate x-axis labels for readability
plt.show()                                # Display the chart
```

**Visualization 3: Average Scores by Hometown**
- We need .groupby('Hometown') to group students by Luzon, Visayas, and Mindanao.
- We use .mean() on the Average column to calculate mean scores per region.
- We plot a bar chart to visually compare regional student performance.
- Output: A bar chart showing the average scores of students grouped by Hometown.
```Python
hometown_avg = board.groupby('Hometown')['Average'].mean()  # Group students by Hometown and compute mean Average

plt.figure(figsize=(8,5))                     # Set the size of the figure
track_avg.plot(kind="bar")                    # Plot the grouped data as a bar chart
plt.title('Average Scores by Hometown')       # Add title to the chart
plt.ylabel('Average Score')                   # Label the y-axis
plt.xlabel('Hometown')                        # Label the x-axis
plt.xticks(rotation=-25)                      # Rotate x-axis labels for readability
plt.show()                                    # Display the chart
```

VERSION 2
