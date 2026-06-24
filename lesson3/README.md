# Introduction to APIs

## Lesson Overview

This lesson introduces the basic idea of using APIs in Python. An API allows one program to request data from another application, website, or service. In Python, we can use the `requests` library to send a request to an API and then use the response in our code.

In this lesson, I practiced pulling data from different APIs and JSON files, including a cat facts API, a World Cup API, my own GitHub JSON file, and a weather API.

## What I Learned

* How to use the `requests` library in Python
* How to send a GET request to an API
* How to convert an API response into JSON
* How to access values inside dictionaries and lists
* How to work with nested JSON data
* How to calculate basic statistics from API data

## Required Library

This lesson uses the `requests` library.

```python
import requests
```

## Cat Fact API

The first API used in this lesson was a cat fact API.

```python
import requests

response = requests.get("https://catfact.ninja/fact")
data = response.json()
```

The line below converts the API response into a Python dictionary:

```python
data = response.json()
```

Then I checked the type of the data:

```python
type(data)
```

To pull out the actual cat fact, I used the key `"fact"`:

```python
data["fact"]
```

This shows how API data can be accessed using dictionary keys.

## World Cup API

The next example used World Cup data from GitHub.

```python
url = "https://raw.githubusercontent.com/openfootball/worldcup.json/master/2026/worldcup.json"
response = requests.get(url)
data = response.json()
```

After converting the response into JSON, I checked what keys were available:

```python
data.keys()
```

Then I accessed the matches:

```python
data["matches"]
```

I also pulled out a specific match from the list:

```python
first_match = data["matches"][0]
five_five_match = data["matches"][55]
```

To access the full-time score from that match, I used:

```python
five_five_match["score"]["ft"][0]
```

This part showed how JSON data can have lists inside dictionaries and dictionaries inside lists.

## Using My GitHub as an API

I also used a raw JSON file from my own GitHub repository like an API.

```python
import requests

url = "https://raw.githubusercontent.com/harveygc2-png/INFO450/main/parts.json"
response = requests.get(url)
data = response.json()
```

Then I accessed a specific part name:

```python
data["parts"][1]["name"]
```

This shows that GitHub can be used to store JSON files and Python can request that data using a raw GitHub URL.

## Weather API

The last example used the Open-Meteo historical weather API.

```python
import requests

url = "https://historical-forecast-api.open-meteo.com/v1/forecast"

params = {
    "latitude": 40.7128,
    "longitude": -74.0060,
    "start_date": "2025-06-20",
    "end_date": "2025-06-26",
    "daily": "temperature_2m_max",
    "timezone": "auto"
}

response = requests.get(url, params=params)
data = response.json()
```

This API request used parameters to tell the API what data I wanted. The parameters included the latitude, longitude, start date, end date, and daily weather variable.

I accessed the daily maximum temperatures with:

```python
temperatures = data["daily"]["temperature_2m_max"]
```

Then I calculated summary statistics:

```python
mean_temp = sum(temperatures) / len(temperatures)
max_temp = max(temperatures)
min_temp = min(temperatures)
range_temp = max(temperatures) - min(temperatures)
```

Finally, I stored the results in a dictionary:

```python
temp_dict = {
    "mean": mean_temp,
    "max": max_temp,
    "min": min_temp,
    "range": range_temp
}
```

## Important Notes

One issue I ran into was accidentally using `min` as a variable name. Since `min()` is already a built-in Python function, it is better not to use `min` as a variable name.

For example, this is better:

```python
min_temp = min(temperatures)
```

Instead of:

```python
min = min(temperatures)
```

Using clear variable names helps avoid errors later in the code.

## Key Takeaways

APIs are useful because they let Python pull data from outside sources. After the data is requested, it can usually be converted into JSON and used like regular Python dictionaries and lists. This lesson helped me understand how to request data, explore the structure of the data, and pull out specific values from an API response.

