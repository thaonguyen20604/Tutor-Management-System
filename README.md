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
flowchart LR
  Client --> API[FastAPI Backend]
  API --> DB[(MySQL Database)]
  API --> FS[File Storage]
  API --> Auth[JWT Security Layer]

# API Endpoints (Summary)
Authentication
| Method | Endpoint         | Description                     |
| ------ | ---------------- | ------------------------------- |
| POST   | `/auth/login`    | User login                      |
| POST   | `/auth/register` | Create new user (Tutor/Student) |

  

Tutors
| Method | Endpoint               | Description                              |
| ------ | ---------------------- | ---------------------------------------- |
| GET    | `/tutors/{id}`         | Get tutor details                        |
| POST   | `/tutors/`             | Create tutor profile                     |
| PUT    | `/tutors/{id}`         | Update tutor profile                     |
| GET    | `/tutors/pending`      | Get list of tutors awaiting verification |
| POST   | `/tutors/{id}/approve` | Approve tutor                            |
| POST   | `/tutors/{id}/reject`  | Reject tutor                             |

Documents
| Method | Endpoint                     | Description                             |
| ------ | ---------------------------- | --------------------------------------- |
| POST   | `/documents/upload`          | Upload document (ID, certificate, etc.) |
| GET    | `/documents/tutor/{id}`      | Get documents by tutor ID               |
| PATCH  | `/documents/{doc_id}/status` | Update document status                  |

Sessions
| Method | Endpoint                 | Description                                |
| ------ | ------------------------ | ------------------------------------------ |
| POST   | `/sessions/`             | Create a new session request               |
| GET    | `/sessions/tutor/{id}`   | Get sessions belonging to a tutor          |
| GET    | `/sessions/student/{id}` | Get sessions belonging to a student        |
| PATCH  | `/sessions/{id}/status`  | Update session status (accept/reject/etc.) |


# Sample Request
## Create Tutor
POST /tutors

{

  "name": "Nguyen Van A",
  
  "email": "tutor@example.com",
  
  "subjects": ["Math", "Physics"]
  
}

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
