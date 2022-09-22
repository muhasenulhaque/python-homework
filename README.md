
# Printing the Titles for the Assignment
print("Financial Analysis")
print("----------------------------------")

#importing add on from libraries  
from pathlib import Path
import pandas as pd
import csv
filepath = Path('/python-homework/PyBank/budget_data.csv")
data = pd.read_csv(filepath)
#counting number of months and pringint
len(data)
print(f"Total Months : {len(data)}")

# Finding pnl Total and printing it 
pnl_total = data['Profit/Losses'].sum()
print(f"Total Porfit/Losses: {pnl_total}")

#creasting dictionary for the differences
pnl_diff = {}
with open(filepath, 'r') as csvfile:
    csvreader = csv.reader(csvfile, delimiter = ',')
    header = next(csvreader)
    first_row = next(csvreader)
    prev_pnl = int(first_row[1])
    for row in csvreader:
        diff = int(row[1]) - prev_pnl
        prev_pnl = int(row[1])
        pnl_diff[row[0]] = diff

        
#finding average changes of values and printing it         
average =  sum(pnl_diff.values())/len(pnl_diff.values())
print(f"Average Change: ${average}")

#identifying the max and min changes 
Greatest_Increase = max(pnl_diff.values())
Greatest_Decrease = min(pnl_diff.values())

# Finding the Key in dictionary for highest increase and decrease 
increase_date = (list(pnl_diff.keys())
      [list(pnl_diff.values()).index(Greatest_Increase)])
decrease_date = (list(pnl_diff.keys())
      [list(pnl_diff.values()).index(Greatest_Decrease)])

#printing the greatest increase and decrease along with the date
print(f"Greatest Increase in profit in: {increase_date} : ${Greatest_Increase}")
print(f"Greatest Decrease in profit in: {decrease_date}: ${Greatest_Decrease}")
