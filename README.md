Here’s a comprehensive README for your project, covering installation, setup, usage, and troubleshooting:

---

# Product Price Tracking Application

This application tracks the price of a specified product on Amazon and sends an email notification to the user if the price drops below the target price within a specified time limit.

## Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Troubleshooting](#troubleshooting)

---

### Features

- Track a product’s price by providing its Amazon URL.
- Set a target price, and receive email notifications when the price drops below it.
- Specify a time limit for tracking, after which you’ll receive a notification if no price drop occurs.
- Retrieve the current tracking status through a status endpoint.

### Requirements

1. **Python 3.x**
2. **Packages**: Install the following Python packages
   - Flask
   - requests
   - BeautifulSoup (bs4)
   - smtplib (comes with Python's `smtplib` library)
   - re (Regular Expressions)
   - datetime
3. **Other Setup**
   - **Email Setup**: Use a Gmail account and enable "App Passwords" if two-factor authentication (2FA) is enabled on the account.

### Setup and Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/Product-Price-Tracking.git
   cd Product-Price-Tracking
   ```

2. **Install Dependencies**

   Run the following command to install the required Python packages:

   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Email in Code**

   - Open `app.py`.
   - Find the `gmail_user` and `gmail_password` variables in the `send_email()` function.
   - Replace `gmail_user` with your Gmail address and `gmail_password` with your App Password (if 2FA is enabled).
   
   **Note:** For security, avoid hardcoding passwords. Use environment variables or a `.env` file to manage sensitive information in production environments.

4. **Run the Application**

   In your terminal, navigate to the project directory and start the Flask application:

   ```bash
   python app.py
   ```

   The app will start at `http://127.0.0.1:5000/`.

### Usage

1. **Track a Product**

   - Open Postman or any other API client.
   - Make a `POST` request to `http://127.0.0.1:5000/track` with a JSON payload containing:
     - `url`: URL of the Amazon product.
     - `target_price`: The price you want to be notified about.
     - `max_time`: Maximum tracking time in minutes.
     - `email`: Your email address to receive notifications.

   **Example JSON Payload:**
   ```json
   {
     "url": "https://www.amazon.in/dp/B0934DRG8F",
     "target_price": 500,
     "max_time": 60,
     "email": "your-email@example.com"
   }
   ```

2. **Check Tracking Status**

   - To check the current tracking status, make a `POST` request to `http://127.0.0.1:5000/status` with a JSON payload containing:
     - `url`: The URL of the Amazon product you’re tracking.

   **Example JSON Payload:**
   ```json
   {
     "url": "https://www.amazon.in/dp/B0934DRG8F"
   }
   ```

### API Endpoints

1. **`POST /track`**
   - Starts tracking the specified product price.

   **Request Body:**
   ```json
   {
     "url": "string",
     "target_price": "float",
     "max_time": "integer",
     "email": "string"
   }
   ```

   **Response:**
   - Returns a JSON message indicating tracking has started.

2. **`POST /status`**
   - Retrieves the tracking status for the specified product.

   **Request Body:**
   ```json
   {
     "url": "string"
   }
   ```

   **Response:**
   - Returns the current status message for the product being tracked.

### Troubleshooting

1. **Common Issues:**
   - **Email Sending Error**: Ensure that the email and App Password are correctly configured.
   - **TypeError: Object of type timedelta is not JSON serializable**: If this error appears, confirm that any `timedelta` object is converted to a string in the `status` endpoint.
   
2. **Check Logs**:
   - Monitor the console output for detailed error messages during tracking.

3. **Testing and Modifications**:
   - Adjust the Amazon page selectors (`.a-price-whole`) if they change in Amazon's HTML structure.
   - To test locally, use smaller `max_time` values to avoid long wait times.

### Additional Notes

- **Automating Execution**: You may want to host this app on a server and use tools like Gunicorn for production-ready deployments.
- **Monitoring Multiple Products**: Use different URLs for each product to track multiple items concurrently.

--- 

Feel free to reach out for any issues you may encounter or if you’d like additional functionality added!
