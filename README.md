# OpenCart 3 REST API Automation Testing

This repository contains a fully automated Postman collection for testing the core shopping cart functionalities of the OpenCart 3 REST API. The project is designed to be executed via Newman (Postman's command-line companion) and is fully integrated with Jenkins for CI/CD pipeline automation.

## 🚀 Features

*   **End-to-End Cart Flow:** Automates the complete user journey from API authentication to modifying a shopping cart.
*   **Dynamic Variable Chaining:** Automatically extracts the `api_token` from the login session and passes it to subsequent requests.
*   **CI/CD Ready:** Configured for headless execution via Newman with Jenkins integration.
*   **Automated Reporting:** Generates detailed HTML reports for every test run.

## 📦 API Endpoints Tested

This collection contains 5 sequential requests that validate the OpenCart Cart Module:

1.  **Create Session** (`POST api/login`) - Authenticates the API user and extracts the session token.
2.  **Add Product to Cart** (`POST api/cart/add`) - Adds a specific product (e.g., iPhone) to the active cart session.
3.  **Get Content** (`GET api/cart/products`) - Retrieves and validates the current items inside the cart.
4.  **Edit Cart Quantity** (`POST api/cart/edit`) - Modifies the quantity of an existing item in the cart.
5.  **Remove Product** (`POST api/cart/remove`) - Deletes the item from the cart and validates the removal.

## 🛠️ Prerequisites

To run these tests locally or on a server, you will need:
*   [Node.js](https://nodejs.org/) installed.
*   [Newman](https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/) installed globally (`npm install -g newman`).
*   Newman HTML Reporter installed globally (`npm install -g newman-reporter-html`).
*   A running instance of OpenCart 3.0.3.8 (configured for API access).

## 💻 Running the Tests Locally

1. Clone this repository:
   ```bash
   git clone https://github.com/YourUsername/PostmanAPI_Opencart.git
   ```
2. Navigate to the directory:
   ```bash
   cd PostmanAPI_Opencart
   ```
3. Run the collection using Newman:
   ```bash
   newman run Opencart_RestAPI_CartModule.postman_collection.json -r cli,html
   ```
   *The HTML report will be automatically generated inside a new `newman` folder.*

## ⚙️ Jenkins CI/CD Integration

This project is configured to run automatically via Jenkins. 

**Build Command:**
```batch
newman run Opencart_RestAPI_CartModule.postman_collection.json -r cli,html
```

**Post-Build Action:**
To save and view the HTML reports directly in the Jenkins dashboard, configure the **Archive the artifacts** step with the following path:
```text
newman/*.html
```

## ⚠️ Important OpenCart Configuration Notes

If you are running this against a local OpenCart server (e.g., XAMPP), ensure the following configurations are set in your OpenCart Admin Panel to prevent `403 Forbidden` and `JSONError` failures:
*   **IP Whitelist:** Navigate to *System > Users > API* and ensure your testing IPs (`127.0.0.1` and `::1`) are added to the IP Addresses tab.
*   **Error Reporting:** Ensure PHP `display_errors` is turned `Off` in your `php.ini` to prevent PHP warnings from corrupting the JSON API responses.