# API Model Hosting with Flask

## Overview

This project implements a simple API for hosting machine learning models using Flask, a popular web framework in Python. The primary purpose is to showcase how to create an API endpoint for making predictions based on a trained machine learning model. In this example, we've used a Polynomial Regression model for demonstration purposes.

[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![Flask](https://img.shields.io/badge/flask-2.0.1-blue.svg)](https://pypi.org/project/Flask/)
[![NumPy](https://img.shields.io/badge/numpy-1.21.0-blue.svg)](https://pypi.org/project/numpy/)
[![Pandas](https://img.shields.io/badge/pandas-1.3.0-blue.svg)](https://pypi.org/project/pandas/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-0.24.2-blue.svg)](https://pypi.org/project/scikit-learn/)
[![Requests](https://img.shields.io/badge/requests-2.26.0-blue.svg)](https://pypi.org/project/requests/)
[![Waitress](https://img.shields.io/badge/waitress-2.1.0-blue.svg)](https://pypi.org/project/waitress/)


## Project Structure

### Code

The main code is split into two parts: the API implementation and a client script for making predictions.

#### API Implementation (`app.py`)

- The `app.py` file contains the Flask application that serves as the API.
- The Polynomial Regression model is trained on a provided dataset (`Position_Salaries.csv`).
- The `/predict` endpoint is created to accept HTTP GET requests with an employee's level as a query parameter and returns the predicted salary based on the trained model.

#### Running the API (`python -m waitress --listen=0.0.0.0:8000 app:app`)

- The `waitress` server is used to serve the Flask application. It is set to listen on `0.0.0.0:8000`.

### Dataset (`Position_Salaries.csv`)

- This CSV file contains a sample dataset with columns: `Position`, `Level`, and `Salary`.
- The dataset is used to train the Polynomial Regression model.

### Client Script (`predict_salary.py`)

- A simple Python script (`predict_salary.py`) demonstrates how to make requests to the API endpoint for salary predictions based on an employee's level.
- It uses the `requests` library to send a GET request to the API and prints the predicted salary.

### Configuration (`gunicorn.conf.py`)

- Gunicorn configuration file (`gunicorn.conf.py`) sets the number of worker processes to utilize for handling incoming requests.

## Setup and Usage

1. Ensure you have the required Python libraries installed (`Flask`, `numpy`, `pandas`, `scikit-learn`, `requests`).
2. Run the API using the provided command: `python -m waitress --listen=0.0.0.0:8000 app:app`.
3. Use the provided client script (`predict_salary.py`) or integrate the API endpoint into your application for making predictions.

## API Endpoint

### Predict Salary Endpoint

- **Endpoint:** `/predict`
- **Method:** `GET`
- **Query Parameter:**
  - `level`: Employee level for prediction (float)

### Example Request

```python
import requests

url = 'http://localhost:8000/predict'
params = {'level': 3.1}
response = requests.get(url, params=params)

if response.status_code == 200:
    result = response.json()
    predicted_salary = result['predicted_salary']
    print(f"Predicted Salary: {predicted_salary}")
else:
    print("Error occurred during the request")
