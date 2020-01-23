import os
import csv
#csvpath = os.path.join("..","Resources", "budget_data.csv")
# Lists to store data
total_months = []
total_profit = []
monthly_profit_change = []
Avarage_Change = []

#open csv in defult read mode
#with open(csvpath, newline='') as budget_data:
with open("../Instructions/PyBank/Resources/budget_data.csv", "r") as budget_data:
  # CSV reader specifies delimiter and variable that holds contents
    csvreader = csv.reader(budget_data, delimiter=',')
    header = next(csvreader)

    for row in csvreader: 
        total_months.append(row[0])
        total_profit.append(int(row[1]))

    for x in range(len(total_profit)-1):

        monthly_profit_change.append(total_profit[x+1]-total_profit[x])

Max_increas = max(monthly_profit_change)
Min_decrese = min(monthly_profit_change)

Increse_Month = monthly_profit_change.index(Max_increas)+1
Decrese_Month = monthly_profit_change.index(Max_increas)+1

print("Financial Analysis")
print("**********************")       
print(f"Total Months:{len(total_months)}")
print(f"Total:${sum(total_profit)}")
percent = round(sum(monthly_profit_change)/len(monthly_profit_change), 2)
Avarage_Change.append(percent)
print(f"Avarage Change :{Avarage_Change}%")
print(f"Greatest Increase in Profits :{total_months[Increse_Month]} (${(str(Max_increas))})")
print(f"Greatest Decrese in Profits :{total_months[Decrese_Month]} (${(str(Min_decrese))}")
 #-------------------output------------------------
output_file = os.path.join("budget_data.csv")
with open(output_file, "w", newline="") as datafile:
    writer = csv.writer(datafile)
datafile.write("Financial Analysis")
datafile.write("\n")
datafile.write("**********************")
datafile.write("\n")
datafile.write(f"Total Months: {len(total_months)}")
datafile.write("\n")
datafile.write(f"Total: ${sum(total_profit)}")
datafile.write("\n")
datafile.write(f"Average Change:{Avarage_Change}% ")
datafile.write("\n")
datafile.write(f"Greatest Increase in Profits:{total_months[Increse_Month]} (${(str(Max_increas))})")
datafile.write("\n")
datafile.write(f"Greatest Decrease in Profits:{total_months[Decrese_Month]} (${(str(Min_decrese))})")
