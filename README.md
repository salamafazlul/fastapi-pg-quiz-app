# FastAPI PostgreSQL Quiz Application

## Overview
This project is a lightweight, FastAPI-based quiz application integrated with PostgreSQL. It provides a RESTful API to create and retrieve quiz questions and their multiple-choice options. Built with FastAPI for rapid API development, SQLAlchemy for database management, Pydantic for robust data validation, and Psycopg2 for PostgreSQL connectivity, it offers a scalable backend for quiz systems.

## Features
- **Question Creation**: Add questions with multiple-choice options, including a flag for the correct choice.
- **Data Retrieval**: Fetch questions by ID or retrieve all choices for a specific question.
- **Persistent Storage**: Stores data in PostgreSQL with relationships managed via SQLAlchemy ORM.
- **Input Validation**: Ensures data integrity using Pydantic models.
- **Dependency Injection**: Efficiently manages database connections with FastAPI's dependency system.

## Tech Stack
- **FastAPI**: High-performance Python framework for building APIs.
- **PostgreSQL**: Robust, open-source relational database.
- **SQLAlchemy**: ORM for seamless database interactions.
- **Pydantic**: Data validation and settings management.
- **Uvicorn**: ASGI server for running the FastAPI application.

## Setup Instructions

### Prerequisites
- Python 3.8 or higher
- PostgreSQL installed and running
- pip for installing Python packages
- pgAdmin or similar tool (optional, for database management)

### Installation
1. **Clone the Repository** (if applicable):
   ```bash
   git clone <repository-url>
   cd fastapi-pg-quiz-app
   ```

2. **Create and Activate Virtual Environment**:
   ```bash
   python -m venv env
   # Windows
   .\env\Scripts\activate
   # Linux/Mac
   source env/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install fastapi uvicorn sqlalchemy psycopg2-binary pydantic
   ```

4. **Set Up PostgreSQL Database**:
   - Create a database.
   - Update the `DATABASE_URL` in `database.py` with your credentials:
     ```python
     DATABASE_URL = "postgresql://{username}:{password}@{host}:{port}/{database_name}"
     ```
5. **Run the Application**:
   ```bash
   uvicorn main:app --reload
   ```
   Access the API at `http://127.0.0.1:8000`.

### Interactive API Documentation
FastAPI provides built-in interactive documentation:
- **Swagger UI**: `http://127.0.0.1:8000/docs`
- **ReDoc**: `http://127.0.0.1:8000/redoc`

## API Endpoints
- **POST /questions**  
  Create a new question with associated choices.  
  **Request Body**:
  ```json
  {
    "question_text": "What is 2 + 2?",
    "choices": [
      {"choice_text": "3", "is_correct": false},
      {"choice_text": "4", "is_correct": true}
    ]
  }
  ```
  **Response**: 200 OK with `null` body on success.

- **GET /questions/{question_id}**  
  Retrieve a question by its ID.  
  **Response**:
  ```json
  {
    "id": 1,
    "question_text": "What is 2 + 2?"
  }
  ```
  **Error**: 404 if question not found.

- **GET /choices/{question_id}**  
  Retrieve all choices for a specific question.  
  **Response**:
  ```json
  [
    {"id": 1, "choice_text": "3", "is_correct": false, "question_id": 1},
    {"id": 2, "choice_text": "4", "is_correct": true, "question_id": 1}
  ]
  ```
  **Error**: 404 if no choices found.
