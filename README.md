# insights-from-a-real-air-bnb-data-set-Hong-Kong
python code for insights on airbwb booking of Hong-Kong we are using calendar add listing csv files
Please find the link for downloading
https://data.insideairbnb.com/china/hk/hong-kong/2024-09-20/data/calendar.csv.gz


```diff
import pandas as pd
calendar=pd.read_csv("calendar.csv")
```

# ✅ Questions that you might want to address about the given data
Let`s dive into exciting insights!
# 1 Want to know the number of available and unavailable rooms
```python
calendar.available.value_counts()
```
<img width="305" alt="Screenshot 1446-07-28 at 9 45 32 am" src="https://github.com/user-attachments/assets/aea50956-3f08-444b-ad63-3cf44c5fd3b1" />

f (false) means not available, t(true) means available.
# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
Explanation:
value_counts(normalize=True) gives proportions.
Multiplying by 100 converts the proportions into percentages
```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```

# 3 Let`s Count the busiest day! 🚩
Hint: We will be counting the most unavailable days (given by f)
```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
# 4 Plot a bar graph to show availability percentage
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['blue', 'pink'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img width="634" alt="Screenshot 1446-07-28 at 9 49 34 am" src="https://github.com/user-attachments/assets/61b99e43-4604-4038-995e-a87111c9b250" />
# 5 Plot the busiest day
```python
busiest_dates.head(10).plot(kind='bar', color='green')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```

<img width="732" alt="Screenshot 1446-07-28 at 9 54 25 am" src="https://github.com/user-attachments/assets/8eacc9f4-ad54-4a09-a838-940ff7d59c3c" />

# 📄 Download listings dataset of Hong-Kong from https://data.insideairbnb.com/china/hk/hong-kong/2024-09-20/visualisations/listings.csv


