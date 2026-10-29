# PeopleFlow — Human Resource Management

PeopleFlow is a responsive HR workspace for employees, managers, and HR teams. It includes secure account access, employee records, attendance check-in/out, leave requests and approvals, company announcements, and learning programs.

## Get started

Requirements: Node.js 18+ and MongoDB (local or hosted).

1. Install dependencies: `npm install`
2. Copy `.env.example` to `.env` and set `MONGODB_URI` and a long, random `JWT_SECRET`.
3. Start the API and web app: `npm run dev`
4. Open `http://localhost:5173` and create an account. The first account in a new database is the HR administrator; later self-registrations are employees.

The API runs on port 5000 by default. Vite forwards `/api` requests to it. For production, build the frontend with `npm run build` and run the API with `npm start`; serve the generated `dist` directory from your web host or reverse proxy.

## Roles and features

- **Employee:** update profile, check in and out, submit leave requests, view announcements, and enroll in training.
- **Manager:** view assigned direct reports, review their leave requests, and create training programs.
- **HR:** manage employee records, review leave requests, post announcements, and view organization attendance.

Managers see the employees assigned to them. HR can assign an employee's manager when creating that employee through the API (`manager` is the manager user's MongoDB ID). Manager accounts and employee account creation are available to HR in the Team area.

## API overview

All routes except `/api/health` and `/api/auth/login` and `/api/auth/register` require a bearer JWT.

| Area | Routes |
| --- | --- |
| Account | `POST /api/auth/register`, `POST /api/auth/login`, `GET/PATCH /api/auth/me` |
| Dashboard | `GET /api/dashboard` |
| Team | `GET/POST /api/employees` |
| Attendance | `GET /api/attendance`, `POST /api/attendance/check-in`, `POST /api/attendance/check-out` |
| Time off | `GET/POST /api/leaves`, `PATCH /api/leaves/:id` |
| Announcements | `GET/POST /api/announcements` |
| Learning | `GET/POST /api/trainings`, `POST /api/trainings/:id/enroll` |

## Security notes

Passwords are hashed with bcryptjs. JWTs expire after seven days. Role checks protect HR and manager operations, and request bodies are validated for required fields. Configure a unique `JWT_SECRET`, use HTTPS, and set `CLIENT_URL` to the production frontend origin before deployment.

## Current scope

The project provides the core workflows and responsive dashboards. Some dashboard summary values and calendar events are presentation placeholders; production payroll, notifications, audit logging, reporting, and comprehensive automated test coverage can be added as follow-on modules.
