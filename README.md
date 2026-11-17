# Secure Notes — Frontend

A responsive web interface for creating and managing personal notes. It connects to the Secure Notes REST API and provides separate User and Admin experiences.

## All Project Links

| Resource | Link |
|---|---|
| **Live application** | https://cerulean-starburst-490a40.netlify.app/ |
| Frontend GitHub repository | https://github.com/2021331100/secure-notes-frontend |
| Backend GitHub repository | https://github.com/2021331100/Assignment-Noteapp |
| Live backend API | https://secure-notes-api-u0nq.onrender.com |
| API health check | https://secure-notes-api-u0nq.onrender.com/health |
| Backend documentation | https://github.com/2021331100/Assignment-Noteapp/blob/production-hardening/README.md |
| Frontend documentation | https://github.com/2021331100/secure-notes-frontend/blob/main/README.md |

## Application Overview

The application has two account roles.

### User
- Register with a name, email, and password.
- Sign in and sign out.
- Create personal notes.
- View a list of personal notes.
- Open, edit, and delete personal notes.
- Access only notes owned by the signed-in account.

### Admin
- Sign in with a separately created Admin account.
- View the registered users.
- Create, view, update, and delete user accounts.
- View notes from all users.
- Group users by their interests.

A regular account created through the Register page is a User account. The public registration form cannot create an Admin account.

## How to Use the Live Site

1. Open the [Secure Notes application](https://cerulean-starburst-490a40.netlify.app/).
2. Select **Register** and create a regular account.
3. Return to the sign-in page and log in.
4. Use the notes dashboard to create, view, edit, or delete your notes.
5. To use the Admin area, sign in with an Admin account created by the project owner.

For details about creating an Admin account, see [Administrator Account Setup in the backend README](https://github.com/2021331100/Assignment-Noteapp/blob/production-hardening/README.md#administrator-account-setup).

## How the Frontend Connects to the Backend

The frontend sends HTTP requests to the deployed API:

```
https://secure-notes-api-u0nq.onrender.com
```

The backend handles account authentication, permission checks, validation, and database operations. Private requests include the access token in the Authorization header:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

The frontend does not contain database credentials, administrator passwords, or the JWT signing secret.

## API Routes Used

### Authentication

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/auth/register` | Register a User |
| POST | `/api/auth/login` | Sign in |
| GET | `/api/auth/me` | Load the current account |

### Notes

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/notes` | Create a note |
| GET | `/api/notes` | List personal notes |
| GET | `/api/notes/:id` | View a note |
| PUT | `/api/notes/:id` | Update a note |
| DELETE | `/api/notes/:id` | Delete a note |

### Admin

These routes require an Admin account.

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/admin/users` | Create a user |
| GET | `/api/admin/users` | List all users |
| GET | `/api/admin/users/:id` | View a user |
| PUT | `/api/admin/users/:id` | Update a user |
| DELETE | `/api/admin/users/:id` | Delete a user |
| GET | `/api/admin/notes` | View all notes |
| GET | `/api/admin/users/group-by-interests` | Group users by interests |

The backend README contains the complete API and setup guide.

## Run the Frontend Locally

### Requirements
- A modern web browser
- Python 3 (for the simple local static server)

### Download the project

```bash
git clone https://github.com/2021331100/secure-notes-frontend.git
cd secure-notes-frontend
```

### Start a local server

```bash
python3 -m http.server 5500
```

Open this address in your browser:

```
http://localhost:5500
```

The frontend is a static site, so it does not need a separate frontend build step for this setup.

## Deployment

The live frontend is deployed on Netlify.

- Site: https://cerulean-starburst-490a40.netlify.app/
- Publish directory: repository root
- Build command: not required for the current static frontend

The backend is deployed separately on Render. Its `CORS_ORIGIN` environment variable must contain the exact frontend origin:

```
https://cerulean-starburst-490a40.netlify.app
```

If the frontend domain changes, update `CORS_ORIGIN` in the Render backend environment and redeploy the backend.

## Troubleshooting

**Cannot connect to API**
1. Open the [backend health check](https://secure-notes-api-u0nq.onrender.com/health).
2. Confirm that the API reports a connected database.
3. If the service is unavailable, check the backend deployment on Render.

**CORS error in the browser**
1. Confirm that the frontend URL matches the Render `CORS_ORIGIN` value exactly.
2. The value must not include a trailing slash or `/api`.
3. Save the Render environment change and wait for deployment to finish.

**Admin page is not accessible**
- A normal registered account has the User role.
- Sign in with a separately created Admin account. See the [backend Admin setup guide](https://github.com/2021331100/Assignment-Noteapp/blob/production-hardening/README.md#administrator-account-setup).

**First request is slow**
- The hosted backend may take some time to start after a period without activity.

## Security Reminders

- Do not store real passwords, database URLs, JWT secrets, or access tokens in frontend files.
- Do not publish Admin credentials in GitHub.
- Use only your own account and test data.
- The backend is responsible for enforcing permissions; frontend navigation alone is not an access-control system.

## Related Documentation

- [Backend README and complete API guide](https://github.com/2021331100/Assignment-Noteapp/blob/production-hardening/README.md)
- [Live application](https://cerulean-starburst-490a40.netlify.app/)
- [Live API health check](https://secure-notes-api-u0nq.onrender.com/health)
