# Tutor Management System
A backend platform built with FastAPI to manage tutors, students, document verification, and scheduling.
The system exposes a clean and scalable RESTful API for frontend and mobile applications.


# Overview
* The Tutor Management System supports the full workflow of a private tutoring service, including:

* Tutor onboarding & document verification

* Student registration & profile management

* Session booking and scheduling

* Admin approval workflows

* Secure authentication with JWT

* Role-based access control (Admin, Tutor, Student)

# Features
## Tutor Management
* Create, update, and manage tutor profiles

* Upload verification documents (ID card, certificates, CV…)

* Admin review and approval process

## Student Management
* Create student accounts

* Browse tutors and request sessions

## Scheduling
* Students request tutoring sessions

* Tutors accept or reject bookings

* Admin override capabilities

## Security
* JWT-based authentication

* Role-based endpoint protection

## Document Handling
* Upload files via multipart/form-data

* Track document status (pending, approved, rejected)

# Architecture

  Client --> API[FastAPI Backend]
  
  API --> DB[(MySQL Database)]
  
  API --> FS[File Storage]
  
  API --> Auth[JWT Security Layer]
  

# API Endpoints (Summary)
Authentication
| Method | Endpoint                            | Description                                             |
| ------ | ----------------------------------- | ------------------------------------------------------- |
| POST   | `/auth/login`                       | Login with username & password                          |
| POST   | `/auth/signup`                      | Create new account (username, email, password, role, …) |
| PATCH  | `/auth/password`                    | Change password                                         |
| POST   | `/auth/forgot-password/request-otp` | Request OTP for password reset                          |
| POST   | `/auth/forgot-password/reset`       | Reset password using OTP                                |
| GET    | `/auth/verify`                      | Verify OTP & update new password                        |
| PATCH  | `/auth/update-role`                 | Internal API — update user role                         |
| GET    | `/`                                 | Root check                                              |
  

Users
| Method | Endpoint                       | Description                                      |
| ------ | ------------------------------ | ------------------------------------------------ |
| POST   | `/user/create`                 | Create a new user (username, email, name, phone) |
| GET    | `/user/by-email/{email}`       | Get user info by email                           |
| GET    | `/user/me`                     | Get current authenticated user                   |
| GET    | `/user/by-id/{user_id}`        | Get user info by ID                              |
| GET    | `/user/by-username/{username}` | Get user info by username                        |
| POST   | `/user/{user_id}/debit`        | Deduct money from user balance                   |
| POST   | `/user/{user_id}/deposit`      | Add money to user balance                        |
| PATCH  | `/user/{user_id}/update`       | Update user data                                 |
| GET    | `/`                            | Root endpoint                                    |


Documents
| Method | Endpoint                                | Description                                     |
| ------ | --------------------------------------- | ----------------------------------------------- |
| GET    | `/academic/tutor-profiles`              | List tutor profiles (filter by user_id, status) |
| POST   | `/academic/tutor-profiles`              | **Upload tutor CV** (multipart/form-data)       |
| GET    | `/academic/tutor-profiles/{profile_id}` | Get tutor profile details                       |
| PATCH  | `/academic/tutor-profiles/{profile_id}` | Update tutor profile (status, bio, etc.)        |
| DELETE | `/academic/tutor-profiles/{profile_id}` | Delete tutor profile                            |


Sessions
| Method | Endpoint                                           | Description                                    |
| ------ | -------------------------------------------------- | ---------------------------------------------- |
| GET    | `/academic/class-sessions`                         | List sessions (filter by class_id, status)     |
| GET    | `/academic/class-sessions/{session_id}`            | Get session details                            |
| PATCH  | `/academic/class-sessions/{session_id}`            | Update session (start_time, end_time, status…) |
| DELETE | `/academic/class-sessions/{session_id}`            | Delete a session                               |
| POST   | `/academic/class-sessions`                         | Create new session                             |
| PATCH  | `/academic/class-sessions/{session_id}/complete`   | Mark session as completed (tutor)              |
| PATCH  | `/academic/class-sessions/{session_id}/processing` | Mark session as processing (tutor)             |

# Installation
pip install -r requirements.txt
uvicorn main:app --reload
## Access API docs:
http://localhost:8000/docs

# Future Enhancements
* AI-based tutor recommendation

* Google Calendar sync

* Payment gateway integration

* WebSocket notifications

* Admin analytics dashboard
