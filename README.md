# EatIQ: Intelligent Food Tracking & Comparison

## README.md is a work in progress

## Table of Contents

* [About The Project](#about-the-project)
    * [Problem Statement](#problem-statement)
    * [Solution: EatIQ](#solution-eatiq)
    * [Key Features](#key-features)
* [Technologies Used](#technologies-used)
* [Architecture](#architecture)
* [Getting Started](#getting-started)
    * [Prerequisites](#prerequisites)
    * [Installation](#installation)
    * [Configuration](#configuration)
    * [Running the Application](#running-the-application)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)

## About The Project

In today's fast-paced world, making informed decisions about food purchases can be challenging. Consumers often struggle to compare prices, understand nutritional values, and identify the best deals across various grocery stores. This leads to inefficient shopping, potentially higher costs, and less healthy choices.

### Problem Statement

* Lack of centralized, real-time price and nutritional data from multiple grocery retailers.
* Difficulty in comparing "price per kilogram" or "price per unit" for different package sizes.
* Time-consuming manual comparison of products across various store websites or physical visits.
* Limited transparency regarding the true cost and nutritional impact of food items.

### Solution: EatIQ

EatIQ is a comprehensive food tracking and comparison application designed to empower consumers with transparent, actionable insights into grocery products. By fetching detailed data from popular online grocery stores like Špar and Mercator's APIs, EatIQ centralizes product information, allowing users to effortlessly search, compare, and analyze food items based on price, nutritional value, package size, and more.

Our goal is to simplify the grocery shopping experience, help users save money, and encourage healthier eating habits by providing all the necessary information at their fingertips.

### Key Features

* **Automated Data Fetching:** Regularly collects product information (price, price per kilogram, nutritional values, package size, etc.) from Špar and Mercator online store APIs.
* **Dual Database Storage:**
    * **Notion Database:** For flexible, human-readable data management, easy categorization, and collaborative oversight.
    * **PostgreSQL Database:** A robust backend for the web application, optimized for querying, filtering, and high-performance data retrieval.
* **Intuitive Web Frontend:**
    * **Product Search:** Quickly find specific food items.
    * **Detailed Product Pages:** View comprehensive information for each product.
    * **Comparison Tools:** Directly compare items side-by-side based on various criteria.
    * **Nutritional Analysis:** Break down nutritional content to make healthier choices.
    * **Price History & Trends:** (Future feature) Track price changes over time.
* **Transparent Pricing:** Easily compare "price per kilogram" or other unit prices to identify the best value.

## Technologies Used

EatIQ leverages a powerful stack of modern technologies to ensure efficient data collection, robust storage, and a user-friendly experience.

* **Data Fetching/Scraping:**
    * Node.js
    * [Axios](https://axios-http.com/) (for making HTTP requests to APIs)
* **Databases:**
    * [PostgreSQL](https://www.postgresql.org/) (Primary backend database)
    * [Notion API](https://developers.notion.com/) (For Notion integration)
* **Backend (API for Frontend):**
    * Python (e.g., [FastAPI](https://fastapi.tiangolo.com/) or [Flask](https://flask.palletsprojects.com/))
* **Frontend:**
    * [React](https://react.dev/) / [Next.js](https://nextjs.org/) (For building the user interface and server-side rendering)
    * [Tailwind CSS](https://tailwindcss.com/) (For rapid and responsive UI development)
    * [Chart.js](https://www.chartjs.org/) (For data visualization, e.g., price trends)

## Architecture

EatIQ follows a modular architecture to ensure scalability and maintainability.

```
graph TD
A\[Špar Online Store API\] --> B(Data Fetcher - Node.js);
C\[Mercator Online Store API\] --> B;
B --> D{Data Processing & Cleaning};
D --> E\[PostgreSQL Database\];
D --> F\[Notion Database\];
E --> G\[Backend API - Python\];
G --> H\[Frontend Web Application - React/Next.js\];
H --> I\[User\];
```

1.  **Data Fetchers:** Node.js scripts periodically make requests to Špar and Mercator online store APIs, extracting raw product data.
2.  **Data Processing:** Extracted data is cleaned, standardized, and enriched (e.g., calculating price per kilogram).
3.  **Database Storage:** Processed data is simultaneously stored in a PostgreSQL database (for the web app backend) and a Notion database (for manual review and flexible management).
4.  **Backend API:** A Python-based API serves as an intermediary, providing structured data endpoints for the frontend. It queries the PostgreSQL database.
5.  **Frontend Web Application:** A React/Next.js-based web interface consumes data from the Backend API, allowing users to search, compare, and visualize food product information.

## Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

* Node.js & npm (for data fetching/scraping and frontend)
* PostgreSQL installed and running
* A Notion account and an integration token (if you plan to use the Notion integration)

### Installation (WIP)

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/maticjesenicnik/eatiq.git](https://www.google.com/search?q=https://github.com/maticjesenicnik/eatiq.git)
    cd eatiq
    ```

2.  **Set up Node.js environment (Data Fetcher & Frontend):**
    ```bash
    npm install # In the root for data fetcher, and in 'frontend' directory for frontend
    ```

### Configuration

1.  **Database Setup:**
    * Create a PostgreSQL database for EatIQ.
    * Update the database connection string in your backend configuration (e.g., `config.py` or environment variables).
    * Run database migrations (you'll need to define these, e.g., using `SQLAlchemy` or raw SQL scripts).

2.  **Notion Integration (Optional):**
    * Create a Notion database for your food products.
    * Create a Notion integration and obtain an API token.
    * Share your Notion database with the integration.
    * Set your Notion API token and database ID as environment variables or in a configuration file.

3.  **Environment Variables:**
    Create a `.env` file in the root of your project (and in the `frontend` directory if needed) with the following (example) variables:

    ```conf
    DATABASE_URL="postgresql://user:password@host:port/database_name"
    NOTION_API_KEY="secret_notion_token"
    NOTION_DATABASE_ID="your_notion_db_id"
    ```

    ```conf
    NEXT_PUBLIC_BACKEND_API_URL="http://localhost:8000/api"
    ```

### Running the Application

1.  **Start the PostgreSQL database:** Ensure your PostgreSQL server is running.

2.  **Run the Data Fetcher (initial data population):**
    ```bash
    node scripts/fetch_spar.js # Or your main data fetching script
    node scripts/fetch_mercator.js
    ```

    *(You'll need to create these Node.js scripts)*

3.  **Start the Backend API:**
    ```bash
    cd backend
    source venv/bin/activate
    uvicorn main:app --reload --port 8000 # If using FastAPI, assuming main.py has `app`
    ```

4.  **Start the Frontend Development Server:**
    ```bash
    cd frontend
    npm run dev # For Next.js development server
    ```

    The frontend application should now be accessible in your browser, usually at `http://localhost:3000`.

## Usage

Once the application is running:

1.  Navigate to the frontend URL (`http://localhost:3000`).
2.  Use the search bar to find products by name or category.
3.  Click on a product to view its detailed information, including nutritional values, price per unit, and store availability.
4.  Utilize the comparison feature to analyze multiple products side-by-side.
5.  (Future) Explore price trends and historical data.

## Roadmap

EatIQ is under active development, and we have several exciting features planned:

* **User Accounts & Preferences:** Allow users to save favorite products, create shopping lists, and set dietary preferences.
* **Price Alerts:** Notify users when a product's price drops below a certain threshold.
* **Advanced Filtering & Sorting:** More robust options for refining search results.
* **Historical Price Data & Trends:** Visualizations of how product prices have changed over time.
* **Mobile Application:** Native iOS/Android app for on-the-go access.
* **More Retailers:** Expand data fetching to include other major grocery chains.
* **Recipe Integration:** Suggest recipes based on available ingredients or dietary goals.

## Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Your Name/Team Name - [your.email@example.com](mailto:your.email@example.com)

Project Link: [https://github.com/maticjesenicnik/eatiq](https://github.com/maticjesenicnik/eatiq) (Update this with your actual repo link)