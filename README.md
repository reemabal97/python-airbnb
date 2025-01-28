# Analysis based on real Airbnb data
* We are dealing with Paris's calendar file in this dataset.
* :memo: You can find this dataset from https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz
![image](https://github.com/user-attachments/assets/06946a63-57fb-4ab2-a3f3-84dbb6466b4a)
# 🧑‍💻 Let`s import the calendar file
```python
import pandas as pd
calinder = pd.read_csv("/Users/reemabalharith/Desktop/MACHINE LEARNING/calendar.csv")
```
![image](https://github.com/user-attachments/assets/73d56ae0-4db6-4812-b338-5b89ff6e9207)

## ✅ Potential questions to explore in this dataset
## 1- Want to know the number of available and unavailable rooms

```python
calinder.available.value_counts()
````
![image](https://github.com/user-attachments/assets/1fef40d2-2b1b-462d-9576-3ec670fa700c)

f (false) means not available, t(true) means available.

## 2- Calculates the percentage of available (t) and unavailable (f) dates.
```python
availability_percentage = calinder['available'].value_counts(normalize=True) * 100
availability_percentage
````
![image](https://github.com/user-attachments/assets/9adb7f8f-9d8b-4b86-ae18-b2c945d44fb9)

## 3- Count the busiest day.
```python
busiest_dates = calinder[calinder['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
![image](https://github.com/user-attachments/assets/d5cd0cde-849f-4cad-aea5-16e97c12c141)

## 📈 4- Plot a bar graph to show availability percentage
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['pink', 'blue'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
````
<img src="https://github.com/user-attachments/assets/737901c6-16c9-42b8-aef9-d33e1ace25af" alt="Value Counts Output" width="600"/>

## 📈 5- Plot the busiest day
```python
busiest_dates.head(10).plot(kind='bar', color='pink')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
````
# 🧑‍💻 Let`s import the listings file
* 📝 You can find this dataset from https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/listings.csv.gz
```python
listings= pd.read_csv("/Users/reemabalharith/Desktop/MACHINE LEARNING/listings.csv")
listings
```
![image](https://github.com/user-attachments/assets/886bac3c-2107-4c9d-a09a-e7eb863664dc)

```python
listings.columns
```
![image](https://github.com/user-attachments/assets/e434ccd2-d81b-4b09-b085-b1451d9428f4)

## ✅ Room type and price is given seperately
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
<img src="https://github.com/user-attachments/assets/51ff6447-f3b3-4092-b849-4d432be0e55a" alt="Value Counts Output" width="600"/>


## 🚀 Top 10 neighborhoods with the most listings
```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightpink')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img src="https://github.com/user-attachments/assets/2b50a661-c376-49a6-9509-25e7be346524" alt="Value Counts Output" width="600"/>

## 💸 Geographical Distribution of Listings (Price Colored)
```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='coolwarm', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img src="https://github.com/user-attachments/assets/d6a30387-fb70-4d31-9227-eaf6007093ed" alt="Value Counts Output" width="600"/>

## 📌 Let us see the listings on a real map
##### Hotter Areas (Red/Yellow) in Paris:
* High Density:
The areas appearing in red or yellow (the "hot" colors) indicate a higher concentration of listings. This suggests that these neighborhoods have a significant number of available rentals.
* Popular Locations:
These regions are likely in high demand, possibly near iconic landmarks like the Eiffel Tower, the Louvre, or lively districts such as Le Marais and Saint-Germain-des-Prés. These are places where tourists and visitors frequently prefer to stay.
##### Colder Areas (Green/Blue) in Paris:
* Low Density:
The blue or green (the "cold" colors) indicate a lower concentration of listings, meaning fewer rental options are available in these parts of the city.
* Less Popular Locations:
These areas may be farther from central attractions or major tourist hubs, often found in quieter suburban neighborhoods. Lower density might also suggest less competition, potentially offering more affordable stays.
##### Density Patterns in Paris:
* Clustered Areas:
If you observe clusters of high-intensity colors, these hotspots likely correspond to areas with high visitor traffic, such as near Champs-Élysées, Montmartre, or the Latin Quarter.
* Spread-Out Listings:
A more even distribution of listings across the city may indicate a balanced demand, with people booking accommodations in various neighborhoods rather than just in central tourist zones.
```python
import folium
from folium.plugins import HeatMap
import pandas as pd

paris_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hawaii
m = folium.Map(location=[48.85611488592879, 2.3490920323011752], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in paris_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('paris_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
<img src="https://github.com/user-attachments/assets/411eebdd-31f4-4533-bf58-36c3379b2990" alt="Value Counts Output" width="600"/>

# 📌 How do I find location for my city?
* Type your city name on google maps
* Right click
* The firt button
<img src="https://github.com/user-attachments/assets/13f71a6b-3ead-473b-93fa-bd049f95f528" alt="Value Counts Output" width="600"/>


















