## HAPAN_MGP_PA4


### ECE Board Exam Problem

// Import pandas

    import pandas as pd

// Read board2.csv file

    board = pd.read_csv('board2.csv')
    board

// Provide Vis data frame

    Vis = board.loc[(board['Math'] <70) & (board['Hometown'] == 'Visayas'), 
                ['Name', 'Gender', 'Track', 'Math']]
    Vis

// Provide Instru data frame and rename Electronics to Electronics >70

    Instru = board.loc[(board['Track'] == 'Instrumentation') &
                   (board['Hometown'] == 'Luzon') &
                   (board['Electronics']>70),
                   ['Name', 'GEAS', 'Electronics']]
    Instru = Instru.rename(columns={'Electronics': 'Electronics >70'})
    Instru

// Add Average Column

    board['Average'] = board[['Math', 'GEAS', 'Electronics','Communication']].mean(axis=1)
    board

// Provide Mindy data frame and rename Electronics to Electronics >70

    Mindy = board.loc[(board['Gender'] == 'Female') & 
                      (board['Hometown'] == 'Mindanao') & 
                      (board['Average'] >= 55), 
                      ['Name', 'Track', 'Electronics', 'Average']]
    Mindy = Mindy.rename(columns={'Average': 'Average >=55'})
    Mindy

// Import matplotlib

    import matplotlib.pyplot as plt

// Show visualization of the Average Scores by Track using bar graph

    track_avg = board.groupby('Track')['Average'].mean()

    plt.figure(figsize=(8,5))
    track_avg.plot(kind="bar")
    plt.title('Average Scores by Track')
    plt.ylabel('Average Score')
    plt.xlabel('Track')
    plt.xticks(rotation=-25)
    plt.show()

// Show visualization of the Average Scores by Gender using bar graph

    track_avg = board.groupby('Gender')['Average'].mean()
    
    plt.figure(figsize=(8,5))
    track_avg.plot(kind="bar")
    plt.title('Average Scores by Gender')
    plt.ylabel('Average score')
    plt.xlabel('Gender')
    plt.xticks(rotation=-25)
    plt.show()

// Show visualization of the Average Scores by Hometown using bar graph

    track_avg = board.groupby('Hometown')['Average'].mean()
    
    plt.figure(figsize=(8,5))
    track_avg.plot(kind="bar")
    plt.title('Average Scores by Hometown')
    plt.ylabel('Average score')
    plt.xlabel('Hometown')
    plt.xticks(rotation=-25)
    plt.show()
