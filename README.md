# HERE complete Python CODE FOR DATA SCRAPPING FORMATTING ALSO CLEAING ALL INCLUDED

import requests
from bs4 import BeautifulSoup
import pandas as pd

# Fetch and parse the HTML
url = 'https://example.com/directory'
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Lists to store the extracted data
names = []
emails = []

# Extract data
for item in soup.find_all('div', class_='contact'):
    name = item.find('span', class_='name').text.strip()
    email = item.find('a', class_='email').text.strip()
    
    names.append(name)
    emails.append(email)

# Create a DataFrame
df = pd.DataFrame({
    'Name': names,
    'Email': emails
})

# Data cleaning
df.drop_duplicates(inplace=True)
df['Email'] = df['Email'].str.lower()

# Save to CSV
df.to_csv('contacts.csv', index=False)

print('Data extracted and saved to contacts.csv')
