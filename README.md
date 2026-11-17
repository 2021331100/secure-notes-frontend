# Secure Notes Frontend

A lightweight, responsive frontend for the Secure Notes REST API assignment.

## Live links
- Frontend: Deploy this repository to Netlify or Vercel.
- Backend API: https://secure-notes-api-u0nq.onrender.com
- Backend health: https://secure-notes-api-u0nq.onrender.com/health

## Features
- User registration and login (JWT bearer token)
- Create, list, edit and delete personal notes
- Admin dashboard: list, create, edit and delete users
- Admin view of all notes
- Group users by interests
- Pagination controls for list views
- Responsive layout

## Run locally
This is a static site. Open `index.html` with a local static server, for example:
```bash
python3 -m http.server 5500
```
Then open http://localhost:5500.

## Deploy
Import this repository into Netlify or Vercel as a static site. No build command is required; publish the repository root.

After deployment, add the exact frontend origin (for example, `https://your-site.netlify.app`) to the backend Render environment variable `CORS_ORIGIN`. If multiple origins are needed, separate them with commas. Redeploy/restart the backend after changing the variable.

## API integration
The default API base URL is set in `app.js` and can also be changed in the sign-in screen. The app expects the backend routes:
- `POST /api/auth/register`, `POST /api/auth/login`
- `GET /api/notes`, `POST /api/notes`, `PUT /api/notes/:id`, `DELETE /api/notes/:id`
- `GET/POST /api/admin/users`, `GET/PUT/DELETE /api/admin/users/:id`
- `GET /api/admin/notes`
- `GET /api/admin/users/group-by-interests`

The backend must remain the source of truth for authentication, authorization, validation and ownership checks. Never put admin credentials, JWT secrets, or database credentials in this frontend repository.
