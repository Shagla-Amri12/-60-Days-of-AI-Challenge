# Day 53 – Project Setup & Foundation

## Objective
Set up the PaperMind AI full-stack development environment and verify frontend-backend communication.

## Tasks Completed
- Continued the capstone project setup.
- Configured Python virtual environment.
- Installed FastAPI, Uvicorn, PyPDF, python-dotenv, and Gemini SDK.
- Generated requirements.txt.
- Created FastAPI application with a /health endpoint.
- Configured CORS for local React development.
- Generated and secured environment variables using .env and .env.example.
- Started the React (Vite) frontend.
- Created an API client using fetch().
- Connected the React frontend to the FastAPI backend.
- Verified successful communication using the /health endpoint.

## Challenge Faced
- Encountered a CORS issue because Vite started on port 5174 instead of 5173.
- Updated the backend CORS configuration to allow both ports.

## Result
✅ Backend running successfully.

✅ Frontend running successfully.

✅ Backend status displayed as **ok**.

✅ Full-stack communication verified.

## Key Learnings
- How FastAPI and React communicate using REST APIs.
- Importance of CORS configuration.
- Managing environment variables securely.
- Creating an API client in React.
- Using health endpoints for backend verification.

## Technologies Used
- Python
- FastAPI
- Uvicorn
- React
- Vite
- JavaScript
- Git & GitHub
- Google Gemini SDK

# SCREENSHOTS

[Backend Running](backend-running.png)

[Backend Status OK](backend-status-ok.png)

[Frontend Running](frontend-running.png)
