# codesoft_weatherforcast_2
import tkinter as tk
import requests

def get_weather():
    api_key = "4ae5cbb67c4b12540b102a32327ea7b9"
    city = city_entry.get()
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

    response = requests.get(url)
    data = response.json()

    if data["cod"] == 200:
        temperature = data["main"]["temp"]
        humidity = data["main"]["humidity"]
        description = data["weather"][0]["description"]

        result_label.config(
            text=f"Weather in {city}: \nTemperature: {temperature}°C\nHumidity: {humidity}%\nDescription: {description.capitalize()}"
        )
    else:
        result_label.config(text="City not found")

# Create the main window
root = tk.Tk()
root.title("Weather Forecast")

# Entry for city or zip code
city_label = tk.Label(root, text="Enter City:")
city_label.pack()

city_entry = tk.Entry(root)
city_entry.pack()

# Get Weather Button
get_weather_button = tk.Button(root, text="Get Weather", command=get_weather)
get_weather_button.pack()

# Label to display weather information
result_label = tk.Label(root, text="", wraplength=300)
result_label.pack()

# Run the Tkinter main loop
root.mainloop()
