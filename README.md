#  Amazon Price Tracker with Python

This project is a Python-based web scraping tool designed to track the price of an Amazon product over time. The script collects product details (title, price, and date), stores them in a CSV file, and can send an email notification when the price drops below a specified threshold.

## Features

## Web Scraping:

- Extracts product title and price from the Amazon product page.

- Uses the BeautifulSoup library for HTML parsing.

## Data Storage:

- Saves product details (title, price, and date) into a CSV file.

- Appends new data to the file daily.

## Price Monitoring:

- Runs periodically (every 24 hours) to check for price changes.

- Sends an email notification when the price drops below a specified level.

## Email Notification:

Sends an email alert with product details and a link to the product when the price condition is met.

# Prerequisites

Before running the script, ensure you have the following installed:

Python 3.x

# Required Python libraries:

pip install requests beautifulsoup4 pandas

## How to Use

## Clone the Repository:

git clone https://github.com/your-username/amazon-price-tracker.git
cd amazon-price-tracker

## Update the Script:

Replace the URL variable with the URL of the Amazon product you want to track.

Update the email credentials in the send_mail() function.

server.login('your-email@gmail.com', 'your-email-password')

## Run the Script:
## Execute the script to start tracking:

python amazon_price_tracker.py

## Email Alerts:
If the price drops below a set threshold (defined in the send_mail function), you will receive an email notification.

# File Structure

- amazon_price_tracker.py: Main script for scraping, data storage, and email alerts.

- AmazonWebScraperDataset.csv: CSV file storing product details (created automatically).

README.md: Project documentation.

## Code Breakdown

1. Web Scraping

Uses requests to fetch the HTML content of the product page and BeautifulSoup to extract the product title and price:

page = requests.get(URL, headers=headers)
soup = BeautifulSoup(page.content, "html.parser")
title = soup.find(id='productTitle').get_text().strip()
price = soup.find(id='priceblock_ourprice').get_text().strip()[1:]

2. Data Storage

Writes product details into a CSV file:

header = ['Title', 'Price', 'Date']
data = [title, price, today]
with open('AmazonWebScraperDataset.csv', 'a+', newline='', encoding='UTF8') as f:
    writer = csv.writer(f)
    writer.writerow(data)

3. Email Notification

Sends an email if the price drops below the specified threshold:

def send_mail():
    server = smtplib.SMTP_SSL('smtp.gmail.com', 465)
    server.login('your-email@gmail.com', 'your-password')
    subject = "The product is now affordable!"
    body = "Check the link: " + URL
    msg = f"Subject: {subject}\n\n{body}"
    server.sendmail('your-email@gmail.com', 'recipient-email@gmail.com', msg)
    server.quit()

4. Automation

Runs the price-checking function daily:

while True:
    check_price()
    time.sleep(86400)  # Wait for 24 hours

# Notes

Amazon's Terms of Service: Scraping Amazon may violate their terms of service. Use this script responsibly.

User-Agent Header: Ensure the headers dictionary includes an appropriate User-Agent string to avoid being blocked.

Email Security: Use app-specific passwords or environment variables for secure email authentication.

# Future Improvements

- Add support for multiple product tracking.

- Implement a graphical user interface (GUI).

- Use a database instead of a CSV file for better scalability.

- Integrate notification services like SMS or push notifications.

- Feel free to customize and enhance the project as per your requirements!

