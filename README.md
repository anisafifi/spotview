# Spotify View

> A web application for visualizing your personalized Spotify listening data.

Spotify View connects to your Spotify account and presents insights such as top tracks, artists, and listening habits using the Spotify Web API.

---

## Tech Stack

The project is built using the following core technologies:

* **Spotify Web API** – OAuth authentication and user listening data
* **React** – Frontend UI (Create React App–based)
* **Node.js + Express** – Backend API for Spotify auth and data proxying
* **Reach Router** – Client-side routing
* **Styled Components** – Component-scoped styling
* **Vercel** – Hosting and serverless deployment

---

## Local Development Setup

### 1. Register a Spotify Application

1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/applications)
2. Create a new app
3. Add the following **Redirect URI**:

   ```
   http://localhost:8888/callback
   ```
4. Save the **Client ID** and **Client Secret**

---

### 2. Environment Configuration

Create an `.env` file in the project root using `.env.example` as a reference.

Example:

```env
CLIENT_ID=your_spotify_client_id
CLIENT_SECRET=your_spotify_client_secret
REDIRECT_URI=http://localhost:8888/callback
FRONTEND_URI=http://localhost:3000
```

---

### 3. Install Dependencies

```bash
nvm use
yarn
yarn client:install
```

---

### 4. Run the App Locally

```bash
yarn dev
```

* Backend: `http://localhost:8888`
* Frontend: `http://localhost:3000`
* Login endpoint: `http://localhost:8888/login`

---

## Deploying to Vercel

This project is deployed using **Vercel**, with the Express backend exposed as serverless functions.

---

### 1. Prepare the Project for Vercel

* Ensure backend routes are compatible with Vercel’s Serverless Functions (e.g. under `/api`)
* Add a `vercel.json` if routing or rewrites are required

Example:

```json
{
  "rewrites": [
    { "source": "/api/(.*)", "destination": "/api/$1" }
  ]
}
```

---

### 2. Deploy to Vercel

From the project root:

```bash
npx vercel
```

Follow the prompts to create and link a Vercel project.

---

### 3. Configure Environment Variables on Vercel

In the **Vercel Dashboard → Project → Settings → Environment Variables**, add:

| Key           | Value                                  |
| ------------- | -------------------------------------- |
| CLIENT_ID     | Your Spotify Client ID                 |
| CLIENT_SECRET | Your Spotify Client Secret             |
| REDIRECT_URI  | `https://your-app.vercel.app/callback` |
| FRONTEND_URI  | `https://your-app.vercel.app`          |

Make sure variables are enabled for **Production**.

---

### 4. Update Spotify Redirect URI

In the Spotify Developer Dashboard, add:

```
https://your-app.vercel.app/callback
```

---

### 5. Access the Live App

Once deployed:

* Login URL:

  ```
  https://your-app.vercel.app/login
  ```
* This behaves the same as:

  ```
  http://localhost:8888/login
  ```

---

## Notes

* Spotify access tokens expire; refresh tokens are handled server-side
* Only Spotify accounts with granted permissions can access user data
* Vercel Serverless Functions have execution limits—avoid long-running requests
