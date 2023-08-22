# tests

import requests

def get_hotel_names(api_key, location, keyword):
    base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"
    params = {
        "key": api_key,
        "location": location,  # Format: "latitude,longitude"
        "radius": 2000,  # Search radius in meters
        "keyword": keyword
    }

    response = requests.get(base_url, params=params)
    data = response.json()

    if data.get("status") == "OK":
        hotel_names = [result["name"] for result in data.get("results")]
        return hotel_names
    else:
        print("Error:", data.get("status"))
        return []

if __name__ == "__main__":
    api_key = "YOUR_API_KEY"
    location = "52.3676,4.9041"  # Amsterdam's latitude and longitude
    keyword = "hotel"

    hotel_names = get_hotel_names(api_key, location, keyword)
    if hotel_names:
        print("Hotel Names in Amsterdam:")
        for index, name in enumerate(hotel_names, start=1):
            print(f"{index}. {name}")
    else:
        print("No hotels found.")
