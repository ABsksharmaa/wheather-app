# wheather-app
import requests  # Importing the requests library
import tkinter as tk
from PIL import Image, ImageTk  # Corrected import statement            

API_KEY = '0b43c06e6b94a16ad6ca4947a8392073'    #this is my key
BASE_URL = "http://api.openweathermap.org/data/2.5/weather?"  
country_names = {
    "AF": "Afghanistan",
    "AL": "Albania",
    "DZ": "Algeria",
    "AS": "American Samoa",
    "AD": "Andorra",
    "AO": "Angola",                             #these are all the name of the countries to print the full name of country
    "BI": "Burundi",
    "CV": "Cabo Verde",
    "IN": "India",
    "ID": "Indonesia",
    "IR": "Iran (Islamic Republic of)",
    "IQ": "Iraq",
    "IE": "Ireland",
    "IM": "Isle of Man",
    "IL": "Israel",
    "IT": "Italy",
    "AF": "Afghanistan",
    "AL": "Albania",
    "DZ": "Algeria",
    "AS": "American Samoa",
    "AD": "Andorra",
    "AO": "Angola",
    "AI": "Anguilla",
    "AQ": "Antarctica",
    "AG": "Antigua and Barbuda",
    "AR": "Argentina",
    "AM": "Armenia",
    "AW": "Aruba",
    "AU": "Australia",
    "AT": "Austria",
    "AZ": "Azerbaijan",
    "BS": "Bahamas",
    "BH": "Bahrain",
    "BD": "Bangladesh",
    "BB": "Barbados",
    "BY": "Belarus",
    "BE": "Belgium",
    "BZ": "Belize",
    "BJ": "Benin",
    "BM": "Bermuda",
    "BT": "Bhutan",
    "BO": "Bolivia",
    "BQ": "Bonaire, Sint Eustatius and Saba",
    "BA": "Bosnia and Herzegovina",
    "BW": "Botswana",
    "BV": "Bouvet Island",
    "BR": "Brazil",
    "IO": "British Indian Ocean Territory",
    "BN": "Brunei Darussalam",
    "BG": "Bulgaria",
    "BF": "Burkina Faso",
    "BI": "Burundi",
    "CV": "Cabo Verde",
    "KH": "Cambodia",
    "CM": "Cameroon",
    "CA": "Canada",
    "KY": "Cayman Islands",
    "CF": "Central African Republic",
    "TD": "Chad",
    "CL": "Chile",
    "CN": "China",
    "CX": "Christmas Island",
    "CC": "Cocos (Keeling) Islands",
    "CO": "Colombia",
    "KM": "Comoros",
    "CD": "Congo (Democratic Republic of the)",
    "CG": "Congo",
    "CK": "Cook Islands",
    "CR": "Costa Rica",
    "HR": "Croatia",
    "CU": "Cuba",
    "CW": "Curaçao",
    "CY": "Cyprus",
    "CZ": "Czech Republic",
    "DK": "Denmark",
    "DJ": "Djibouti",
    "DM": "Dominica",
    "DO": "Dominican Republic",
    "EC": "Ecuador",
    "EG": "Egypt",
    "SV": "El Salvador",
    "GQ": "Equatorial Guinea",
    "ER": "Eritrea",
    "EE": "Estonia",
    "SZ": "Eswatini",
    "ET": "Ethiopia",
    "FK": "Falkland Islands (Malvinas)",
    "FO": "Faroe Islands",
    "FJ": "Fiji",
    "FI": "Finland",
    "FR": "France",
    "GF": "French Guiana",
    "PF": "French Polynesia",
    "TF": "French Southern Territories",
    "GA": "Gabon",
    "GM": "Gambia",
    "GE": "Georgia",
    "DE": "Germany",
    "GH": "Ghana",
    "GI": "Gibraltar",
    "GR": "Greece",
    "GL": "Greenland",
    "GD": "Grenada",
    "GP": "Guadeloupe",
    "GU": "Guam",
    "GT": "Guatemala",
    "GG": "Guernsey",
    "GN": "Guinea",
    "GW": "Guinea-Bissau",
    "GY": "Guyana",
    "HT": "Haiti",
    "HM": "Heard Island and McDonald Islands",
    "VA": "Holy See",
    "HN": "Honduras",
    "HK": "Hong Kong",
    "HU": "Hungary",
    "IS": "Iceland",
    "IN": "India",
    "ID": "Indonesia",
    "IR": "Iran (Islamic Republic of)",
    "IQ": "Iraq",
    "IE": "Ireland",
    "IM": "Isle of Man",
    "IL": "Israel",
    "IT": "Italy",
    "JM": "Jamaica",
    "JE": "Jersey",
    "JP": "Japan",
    "JO": "Jordan",
    "KZ": "Kazakhstan",
    "KE": "Kenya",
    "KI": "Kiribati",
    "KP": "Korea (Democratic People's Republic of)",
    "KR": "Korea, Republic of",
    "KW": "Kuwait",
    "KG": "Kyrgyzstan",
    "LA": "Lao People's Democratic Republic",
    "LV": "Latvia",
    "LB": "Lebanon",
    "LS": "Lesotho",
    "LR": "Liberia",
    "LY": "Libya",
    "LI": "Liechtenstein",
    "LT": "Lithuania",
    "LU": "Luxembourg",
    "MO": "Macao",
    "MG": "Madagascar",
    "MW": "Malawi",
    "MY": "Malaysia",
    "MV": "Maldives",
    "ML": "Mali",
    "MT": "Malta",
    "MH": "Marshall Islands",
    "MQ": "Martinique",
    "MR": "Mauritania",
    "MU": "Mauritius",
    "YT": "Mayotte",
    "MX": "Mexico",
    "FM": "Micronesia (Federated States of)",
    "MD": "Moldova (Republic of)",
    "MC": "Monaco",
    "MN": "Mongolia",
    "ME": "Montenegro",
    "MS": "Montserrat",
    "MA": "Morocco",
    "MZ": "Mozambique",
    "MM": "Myanmar",
    "NA": "Namibia",
    "NR": "Nauru",
    "NP": "Nepal",
    "NL": "Netherlands",
    "NC": "New Caledonia",
    "NZ": "New Zealand",
    "NI": "Nicaragua",
    "NE": "Niger",
    "NG": "Nigeria",
    "NU": "Niue",
    "NF": "Norfolk Island",
    "MP": "Northern Mariana Islands",
    "NO": "Norway",
    "OM": "Oman",
    "PK": "Pakistan",
    "PW": "Palau",
    "PS": "Palestine, State of",
    "PA": "Panama",
    "PG": "Papua New Guinea",
    "PY": "Paraguay",
    "PE": "Peru",
    "PH": "Philippines",
    "PN": "Pitcairn",
    "PL": "Poland",
    "PT": "Portugal",
    "PR": "Puerto Rico",
    "QA": "Qatar",
    "RE": "Réunion",
    "RO": "Romania",
    "RU": "Russian Federation",
    "RW": "Rwanda",
    "BL": "Saint Barthélemy",
    "SH": "Saint Helena, Ascension and Tristan da Cunha",
    "KN": "Saint Kitts and Nevis",
    "LC": "Saint Lucia",
    "MF": "Saint Martin (French part)",
    "PM": "Saint Pierre and Miquelon",
    "VC": "Saint Vincent and the Grenadines",
    "WS": "Samoa",
    "SM": "San Marino",
    "ST": "Sao Tome and Principe",
    "SA": "Saudi Arabia",
    "SN": "Senegal",
    "RS": "Serbia",
    "SC": "Seychelles",
    "SL": "Sierra Leone",
    "SG": "Singapore",
    "SX": "Sint Maarten (Dutch part)",
    "SK": "Slovakia",
    "SI": "Slovenia",
    "SB": "Solomon Islands",
    "SO": "Somalia",
    "ZA": "South Africa",
    "GS": "South Georgia and the South Sandwich Islands",
    "SS": "South Sudan",
    "ES": "Spain"
}


def get_weather(city): #this function will return the data
    
    url = f"{BASE_URL}q={city}&appid={API_KEY}&units=metric"  #this url will come with their city and name
    
    
    response = requests.get(url)    #this is my get request for  api
    
    
    print(f"Request URL: {url}")  #here i am pring the url for varifying 
    
    
    # if response.status_code == 200:     # checking here about the code status
       
    #     data = response.json()  #jsonto convert response
        
        
    #     print("Raw data from API:", data)           #this is my row data uesd for debuging
        
        
    #     main = data['main']              # extract necessary information
    #     temperature = main['temp']
    #     feels_like = main['feels_like']
    #     humidity = main['humidity']
    #     pressure = main['pressure']
    #     weather_description = data['weather'][0]['description']
    #     country_code = data['sys']['country'] 

    #     print(f"Country Code: {country_code}")
    if response.status_code == 200:  # Checking status code
        data = response.json()  # Convert response to JSON
        
        main = data['main']  # Extract necessary information
        temperature = main['temp']
        feels_like = main['feels_like']
        humidity = main['humidity']
        pressure = main['pressure']
        weather_description = data['weather'][0]['description']
        country_code = data['sys']['country']
        
        
        country = country_names.get(country_code, "Unknown Country")     #geeiong the country name

        
        weather_info = (f"City: {city}, Country: {country}\n"
                        f"Temperature: {temperature}°C\n"
                        f"Feels like: {feels_like}°C\n"      #display wheather on gui
                        f"Humidity: {humidity}%\n"
                        f"Pressure: {pressure} hPa\n"
                        f"Weather Description: {weather_description.capitalize()}")
        
        output_label.config(text=weather_info)  # Update the output label
        
    else:
        # Display error message
        output_label.config(text="City not found, please try again.")


root = tk.Tk()
root.title("Weather App for desktop")        # create a basic Tkinter window
root.geometry("600x600")  # Window size

background_image = Image.open("C:/Users/Manoj kumar/Downloads/natureback.jpg")
# Change the path to your image
background_image = background_image.resize((600, 600), Image.LANCZOS)  # Resize image
bg_label = ImageTk.PhotoImage(background_image)

# Background label
background_label = tk.Label(root, image=bg_label)
background_label.place(x=0, y=0, relwidth=1, relheight=1) 

city_label = tk.Label(root, text="Enter city name:", bg='lightgray')         # create a label for the city entry
city_label.pack(pady=55)


city_entry = tk.Entry(root, width=30)            # create an entry field for city input
city_entry.pack(pady=54)


get_weather_button = tk.Button(root, text="Get Weather", command=lambda: get_weather(city_entry.get()))          # create a button to fetch weather
get_weather_button.pack(pady=40)


output_label = tk.Label(root, text="", justify="left")  # create a label for displaying output
output_label.pack(pady=40)


root.mainloop()       # run the Tkinter event loop
     




