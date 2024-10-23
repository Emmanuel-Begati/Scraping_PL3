# APIs and Web Scraping Peer Learning Activity - Group 3

## Group Members
- **Emmanuel**: Presented on Task 0
- **Esther**: Introduced the team and presented on the Amazon task
- **Charite**: Continued with the presentation on the Amazon task
- **Caroline**: Presented on scraping tabular data

## Summary
This repository focuses on tasks related to web scraping and the use of APIs. The project involves the following tasks:

### Tasks
1. **Task 0**
   - **Objective**: Retrieve a list of starships from the Star Wars API (SWAPI).
   
2. **Web Scraping**
   - **Objective**: Use the BeautifulSoup library in Python to perform the following tasks:
     - **Scrape Tabular Data**: Extract tabular data from the website and save it in CSV format.
     - **List Products from Amazon**: Scrape at least 5 products from different categories on Amazon.com, download and label the product images appropriately.

---

## Task 0: Retrieve Starships from SWAPI

### The Function
```python
def availableShips(passengerCount):
```

The `availableShips` function queries the SWAPI for starship data and filters the results based on the provided passenger count. It handles pagination to ensure all available data is retrieved and considers only ships with valid passenger capacities.

- **`passengerCount` (int)**: The minimum number of passengers a starship should be able to carry.


### Implementation
- The function makes a GET request to the SWAPI and processes each starship in the results.
- It checks for valid passenger data, excluding values such as "n/a", "unknown", "0", and "none".
- The passenger count is converted to an integer after removing commas.
- The function continues to fetch data until all pages are processed.
- Returns an empty list no ships meet the criteria
---
```python    
    while url:
        # Make a GET request to fetch starship data
        response = requests.get(url)
        print(f"Fetching data from: {url}")
        data = response.json()
        
        # Iterate over each starship in the results
        for ship in data["results"]:
            print(f"Processing ship: {ship['name']}")
            
            # Check if the passenger information is valid
            if (
                ship["passengers"] != "n/a"
                and ship["passengers"] != "unknown"
                and ship["passengers"] != "0"
                and ship["passengers"] != "none"
            ):
                # Remove commas from the passenger count and convert to an integer
                ship["passengers"] = ship["passengers"].replace(",", "")
                if int(ship["passengers"]) >= passengerCount:
                   
                    ships.append(ship["name"])
                    print(f"Ship added: {ship['name']}")
        
        url = data["next"]

```

## Web Scraping Tasks:

### Overview
This project demonstrates how to scrape tabular data using the BeautifulSoup library in Python. The goal is to extract the table data and save the data in CSV format.


#### IMPLEMENTATION:
   - We used the `requests` library to fetch the page content. 
   ```python
   data = requests.get(url)
   ```
   - Checked the response status to ensure successful data retrieval.
   ```python
   print (data.status_code)
   ```
   - Used BeautifulSoup to parse the HTML content.
   ```python
   soup = BeautifulSoup(data.text, 'html.parser')
   ```
   - Identified table headers and rows to structure the data.
   - Extracted table header:
     - Team Name
     - Year
     - Wins
     - Losses
     - Overtime Losses
     - Win Percentage
     - Goals For (GF)
     - Goals Against (GA)
     - Plus/Minus
   - Stored the data in df
   ```python
   df = pd.DataFrame(table_row, columns=table_columns)
   ```

   - Saved the extracted data into a CSV file named `scraped_data.csv`.
   ```python
   df.to_csv('scraped_data.csv', index=False)
   ```

   - Printed the length of the DataFrame to verify the amount of data scraped.
   ```python
   length = len(df)
   ```


```

## Amazon Tasks:


```