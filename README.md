# Student Management System

A full-stack student records dashboard for managing student information through a responsive React interface and a real Django REST Framework API backed by SQLite.

## Features

- Dashboard with live student totals, department distribution, year distribution, and recent students
- Create, view, edit, and delete student records
- Search by student name or email
- Filter by department, year, and gender
- Frontend and backend validation
- Unique email enforcement with clear error feedback
- Loading, empty, success, error, and delete-confirmation states
- SQLite persistence through Django ORM
- REST API with JSON responses
- Responsive layout for desktop and mobile

## Tech stack

- Frontend: React, TypeScript/JSX, Vite, Tailwind CSS, TanStack Query
- Backend: Python, Django, Django REST Framework, django-cors-headers
- Database: SQLite
- Communication: JSON REST API with generated React Query hooks

## Setup

### Backend

From the project root:

```bash
python3 -m pip install -r backend/requirements.txt
python3 backend/manage.py migrate
python3 backend/manage.py runserver 0.0.0.0:8080
```

The API is available at `http://localhost:8080/api/`.

### Frontend

Install the JavaScript workspace dependencies and start the dashboard:

```bash
pnpm install
pnpm --filter @workspace/student-management run dev
```

The frontend uses the Replit preview routing and calls the API through `/api`.

### Replit

The project includes managed workflows for the web dashboard and API service. Start the workflows from the Replit Run panel. The API service runs Django on the configured API port and the frontend runs Vite on the configured web port.

## API documentation

Base URL: `/api`

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/healthz` | API health check |
| GET | `/students/` | List students; accepts `search`, `department`, `year`, and `gender` query parameters |
| POST | `/students/` | Create a student |
| GET | `/students/summary/` | Dashboard totals and grouped counts |
| GET | `/students/{id}/` | Retrieve one student |
| PUT | `/students/{id}/` | Replace a student |
| PATCH | `/students/{id}/` | Partially update a student |
| DELETE | `/students/{id}/` | Delete a student |

Example create request:

```json
{
  "name": "Aarav Menon",
  "email": "aarav.menon@example.com",
  "phone": "+91 98765 43210",
  "department": "Computer Science",
  "year": 2,
  "gender": "Male",
  "date_of_birth": "2005-08-12",
  "address": "Bengaluru, Karnataka"
}
```

Email addresses are normalized to lowercase and must be unique. Validation errors return HTTP 400 with a `detail` message and an `errors` object keyed by field.

## Testing instructions

Run the Django checks and migrations:

```bash
python3 backend/manage.py check
python3 backend/manage.py makemigrations --check
python3 backend/manage.py migrate
```

Run the workspace typecheck and build:

```bash
pnpm run typecheck
pnpm --filter @workspace/student-management run build
```

To manually verify CRUD behavior, create a student in the dashboard, refresh the page, search for the record, edit it, delete it with confirmation, and confirm it no longer appears. API calls can also be tested with `curl` against `/api/students/`.

## GitHub instructions

1. Create a new GitHub repository.
2. Add the repository as a remote:

   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   ```

3. Review the files and commit:

   ```bash
   git add .
   git commit -m "Build student management system"
   ```

4. Push the default branch:

   ```bash
   git branch -M main
   git push -u origin main
   ```

Do not commit `backend/db.sqlite3`, Python caches, virtual environments, or environment files.