## API Endpoint: `/search_anime`

### Description
This API allows users to search for anime by providing a search query. It scrapes an external website to retrieve anime information based on the search query and returns a list of anime results.

### Request

- **Method:** `GET`
- **Endpoint:** `/search_anime`

#### Query Parameters

| Parameter | Type   | Description                               |
|-----------|--------|-------------------------------------------|
| `search`  | String | The search query for anime titles.       |

### Response

#### Success Response

- **Status Code:** `200 OK`

```json
Anime Search Results for "Example":
Name: Example
Image URL: example.jpg
hoveredUlInfo: example

```

- `anime_list` (array): A list of anime entries matching the search query.
  - `Name` (string): The name of the anime.
  - `Image URL` (string): The URL of an image representing the anime.
  - `hoveredUlInfo` (string): Additional information about the anime.

#### Error Response

- **Status Code:** `HTTP 4xx` or `HTTP 5xx` (e.g., `400 Bad Request`, `500 Internal Server Error`)

```json
{
    "error": "Error message describing the issue."
}
```

### Example

**Request:**

```python
import requests

# Define the API endpoint URL
api_url = 'https://animeapi-1.u1u1u1u1u1u1u1.repl.co/search_anime'

# Define the search query
search_query = 'Vinland'  # Replace with your desired search query

# Define the parameters for the GET request
params = {'search': search_query}

# Send a GET request to the API
response = requests.get(api_url, params=params)

# Check the response status code
if response.status_code == 200:
    # Parse the JSON response
    data = response.json()
    anime_list = data.get('anime_list', [])

    if anime_list:
        print(f'Anime Search Results for "{search_query}":')
        for anime in anime_list:
            print(f"Name: {anime['Name']}")
            print(f"Image URL: {anime['Image URL']}")
            print(f"hoveredUlInfo: {anime['hoveredUlInfo']}")
            print()
    else:
        print(f'No anime found for "{search_query}".')

else:
    print(f'Error: {response.status_code} - {response.json().get("error", "Unknown Error")}')


```

**Response (200 OK):**

```json
Anime Search Results for "Vinland":
Name: Vinland Saga Season 2
Image URL: https://v.xsanime.com/wp-content/uploads/2023/01/Vinland-Saga-Season-2-XSAnime.jpg
hoveredUlInfo: تصنيف : سينين
موسم : شتاء 2023
"Vinland Saga" هو مسلسل أنمي ياباني تاريخي يعتمد على المانجا التي تحمل نفس الاسم من ...

Name: Vinland Saga
Image URL: https://www.xsanime.com/wp-content/uploads/2019/11/102249l.jpg
hoveredUlInfo: تصنيف : سينين
موسم : صيف 2019
قصة أنمي Vinland Saga تدور حول ثورفين الذي نشأ وهو يستمع إلى قصص البحارة القدامى ...

```

**Response (Error 400 Bad Request):**

```json
{
    "error": "Search query is missing."
}
```

### Notes

- This API scrapes an external website to retrieve anime information. Ensure that the external website is accessible and responds correctly to avoid errors.
- The quality and availability of data may vary depending on the external website's structure and content.
- Proper error handling should be implemented to deal with potential issues, such as network errors or changes in the external website's structure.
- It is essential to follow web scraping best practices and respect the terms of service of the external website you are scraping.
