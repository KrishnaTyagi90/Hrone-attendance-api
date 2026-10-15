# Employee Attendance & Analytics API

## Project Overview
A REST API built using Python, FastAPI, and MongoDB to manage employee attendance records.

## Technologies Used
- Python
- FastAPI
- MongoDB
- Pydantic

## Features
- Employee records management
- Employee attendance listing
- Employee punch-in and punch-out
- Attendance filtering by employee code, date range, and status
- Pagination for attendance records
- Health check endpoint

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/KrishnaTyagi90/Hrone-attendance-api.git
   cd Hrone-attendance-api
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   ```

   On Windows:
   ```bash
   .venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure the MongoDB connection using environment variables. Do not commit credentials or the `.env` file.

5. Start the API:
   ```bash
   uvicorn app.main:app --port 8000 --reload
   ```

6. Open the API documentation:
   http://127.0.0.1:8000/docs

## API Endpoints
- `GET /health` — Check application and database status
- `POST /employees` — Create an employee
- `GET /employees` — List employees
- `POST /attendance/punch-in` — Record punch-in
- `POST /attendance/punch-out` — Record punch-out
- `GET /attendance` — List and filter attendance records

Refer to the API documentation for request schemas and available parameters.

## Project Documents
- `REVIEW.md` — Code review notes
- `DECISIONS.md` — Design decisions
- `DATA_MODEL.md` — Database model information

## Security
Never commit database credentials, API keys, or other secrets.
