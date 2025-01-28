# Analysis based on real Airbnb data
* We are dealing with Paris's calendar file in this dataset.
* :memo: You can find this dataset from https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz
* ![image](https://github.com/user-attachments/assets/06946a63-57fb-4ab2-a3f3-84dbb6466b4a)

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








