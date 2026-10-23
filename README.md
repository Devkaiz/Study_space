# StudySpace

StudySpace is a full-stack collaborative study material and productivity platform for B.Tech Software Engineering demonstrations. It is intentionally built with approachable technologies: vanilla HTML/CSS/JavaScript, Express, and SQLite.

## Features

- JWT + bcrypt registration, login, demo login, profile editing, and password changes
- Database-backed dashboard with live task, session, group, material, and notification data
- Material upload (10 MB limit; PDF/DOC/DOCX/PPT/PPTX/TXT), external links, search/filter, view/download/delete
- Study groups, membership, member lists, and database-backed discussions
- Tasks with deadlines, priority, complete/undo, editing, deleting, calendar display, and overdue status
- Pomodoro timer plus an explicit **Demo Complete Session** action that records a real 25-minute session
- Progress analytics, weekly activity, read/unread notifications, responsive navigation

## Stack and architecture

`Vanilla JS frontend → fetch REST API → Node.js + Express → SQLite`

All dashboard/progress data is calculated from SQLite; the frontend does not hardcode project statistics.

## Run locally

1. Install [Node.js](https://nodejs.org/) 18+.
2. In this project folder, run `npm install`.
3. Run `npm start`.
4. Open `http://localhost:3000`.

The database (`studyspace.db`) and sample data are initialized automatically on first start. Uploaded material files are stored in `uploads/`.

## Demo account

- Email: `demo@studyspace.com`
- Password: `Demo@123`

Click **Continue as Demo User** on the opening login page.

## API endpoints

| Area | Endpoints |
|---|---|
| Auth | `POST /api/auth/register`, `POST /api/auth/login`, `GET/PATCH /api/me`, `POST /api/auth/change-password` |
| Dashboard | `GET /api/dashboard` |
| Materials | `GET/POST /api/materials`, `DELETE /api/materials/:id` |
| Groups | `GET/POST /api/groups`, `GET /api/groups/:id`, `POST /api/groups/:id/join`, `/leave`, `GET/POST /api/groups/:id/comments` |
| Tasks | `GET/POST /api/tasks`, `PATCH/DELETE /api/tasks/:id` |
| Calendar | `GET /api/calendar` |
| Focus sessions | `GET/POST /api/sessions` |
| Progress | `GET /api/progress` |
| Notifications | `GET /api/notifications`, `PATCH /api/notifications/:id/read`, `PATCH /api/notifications/read-all` |

## Database schema

SQLite tables: `Users`, `StudyMaterials`, `StudyGroups`, `GroupMembers`, `GroupComments`, `Tasks`, `StudySessions`, and `Notifications`. Foreign keys are enabled and relationships are enforced. Password hashes are never returned from APIs.

## Project layout

```
StudySpace/
├── server.js          # Express API and authorization
├── database.js        # SQLite schema + automatic realistic demo seed
├── package.json
├── studyspace.db      # created on first run
├── uploads/
└── public/
    ├── index.html     # login/register and responsive SPA shell
    ├── css/style.css
    └── js/app.js
```

## Suggested demonstration

1. Open the login page and choose the demo user.
2. Dashboard: explain live statistics and quick actions.
3. Materials: search `DBMS`, open a resource, then upload a supported file or add a URL.
4. Groups: open Big Data Squad and post a discussion message.
5. Tasks: create **Complete Software Engineering Report** with deadline/priority/subject, then open Calendar.
6. Pomodoro: start normally or use **Demo Complete Session**; it writes to SQLite and makes a notification.
7. Progress and Notifications: show updated session metrics and mark notification read.
8. Profile and logout.

## Testing

Start the server, use the demo flow above, and use browser DevTools Network/Console to observe API calls. The backend validates authorization, task/material ownership, group membership, malformed values, duplicate emails, and upload size/type.

## Future enhancements

- AI study assistant and AI-generated quizzes
- Automatic material summarization
- Cloud storage
- Real-time group chat
- Mobile application
- Advanced analytics
- Calendar synchronization
