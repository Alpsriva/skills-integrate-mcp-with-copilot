# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure teacher credentials in the server environment:

   ```
   export TEACHER_USERNAME=teacher
   export TEACHER_PASSWORD='choose-a-strong-password'
   ```

   Set `COOKIE_SECURE=true` when serving the application over HTTPS. The default
   is suitable only for local HTTP development.

3. Run the application:

   ```
   uvicorn app:app --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

Students can view activity rosters without logging in. A teacher login is
required to register or remove students. Teacher credentials are read from
environment variables and must not be committed to the repository. Sessions
are held in memory and expire after eight hours or when the server restarts.

## API Endpoints

| Method | Endpoint                                                               | Description                                                         |
| ------ | ---------------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                          | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                          | Start a teacher session                                             |
| GET    | `/auth/session`                                                        | Check the current teacher session                                   |
| POST   | `/auth/logout`                                                         | End the current teacher session                                     |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu`      | Register a student (teacher session required)                       |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Remove a student (teacher session required)                         |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
