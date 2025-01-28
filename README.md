# insights-from-a-real-air-bnb-data-set-Hong-Kong
python code for insights on airbwb booking of Hong-Kong we are using calendar add listing csv files
Please find the link for downloading
https://data.insideairbnb.com/china/hk/hong-kong/2024-09-20/data/calendar.csv.gz

<img width="1114" alt="Screenshot 1446-07-28 at 10 25 26 am" src="https://github.com/user-attachments/assets/877901ec-3803-423f-b06d-a029e1f07b2d" />



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

```python
import pandas as pd
listings = pd.read_csv('/Users/reemsaad/Desktop/listings.csv')
listings.head(2)
```

<img width="859" alt="Screenshot 1446-07-28 at 10 01 14 am" src="https://github.com/user-attachments/assets/34ba72f0-6d6d-47d5-832a-a4cdf3e98877" />

```python
listings.columns
```

<img width="575" alt="Screenshot 1446-07-28 at 10 02 20 am" src="https://github.com/user-attachments/assets/9926c894-a808-4b4d-8d9e-18cca5ce046e" />

# ✅ Room type and price is given seperately

Let`s Combine and visualize them

```python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='pink')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```

<img width="746" alt="Screenshot 1446-07-28 at 10 04 19 am" src="https://github.com/user-attachments/assets/b2e073d9-1a67-4a52-a069-33b57d9a0174" />

# ✅ Which are the top 10 neighborhoods with the most listings?

```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```

<img width="708" alt="Screenshot 1446-07-28 at 10 06 09 am" src="https://github.com/user-attachments/assets/4105ba63-b19a-49a3-95b6-8ecec184b9ee" />

# ✅ Geographical Distribution of Listings (Price Colored)

```python
import matplotlib.pyplot as plt
import seaborn as sns
```

```python
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```

<img width="971" alt="Screenshot 1446-07-28 at 10 09 20 am" src="https://github.com/user-attachments/assets/b8317edc-e45f-4e28-b88b-85302e70fd51" />

# This analysis explores Airbnb availability and the busiest days in Hong Kong

The Busiest Days When Rooms Are Not Available

```python
# Find the busiest days when rooms are not available
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()

# Display the busiest day
most_busy_day = busiest_dates.idxmax()
print(f"The busiest day with no availability is: {most_busy_day}")
```
<img width="456" alt="Screenshot 1446-07-28 at 11 06 37 am" src="https://github.com/user-attachments/assets/2bb28ea3-c9b1-4899-a36b-da5914d95add" />

The Most Crowded Neighbourhoods Based on Listings

```python
# Find the most crowded neighbourhoods based on the number of listings
most_crowded_neighbourhood = listings['neighbourhood'].value_counts().idxmax()

print(f"The most crowded neighbourhood is: {most_crowded_neighbourhood}")
```

<img width="411" alt="Screenshot 1446-07-28 at 11 07 13 am" src="https://github.com/user-attachments/assets/4c890740-ec37-4768-9048-ed4c60e2be0c" />



# Let us see the listings on a real map

Hotter Areas (Red/Yellow):

High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas.
Popular Locations: These regions might be more popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in Hong Kong where people tend to stay more often.
Colder Areas (Green/Blue):

Low Density: Areas with blue or green (the "cold" colors) indicate a lower concentration of listings. These regions have fewer listings available.
Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic.
Density Patterns:

Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like resorts, beaches, or urban centers.
Spread-Out Listings: If the heatmap shows a more uniform distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of Hong Kong.

```python
import folium
from folium.plugins import HeatMap
import pandas as pd

# Select relevant columns
hong_kong_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hong Kong
m = folium.Map(location=[22.3193, 114.1694], zoom_start=11)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in hong_kong_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('hong_kong_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```

<img width="1084" alt="Screenshot 1446-07-28 at 10 17 16 am" src="https://github.com/user-attachments/assets/5eb150f8-aa60-47f0-85e9-b8d200dd7f94" />

# 🚨 How do I find location for my city?

Type your city name on google maps
Click on What`s here

<img width="1335" alt="Screenshot 1446-07-28 at 10 22 38 am" src="https://github.com/user-attachments/assets/de7cf54f-2795-47aa-ac79-17f2616d6f37" />

You will find latitude and longitude at the bottom of screen

<img width="374" alt="Screenshot 1446-07-28 at 10 23 59 am" src="https://github.com/user-attachments/assets/28ea12bc-e1df-4792-9f5c-c2cbbe21c430" />


