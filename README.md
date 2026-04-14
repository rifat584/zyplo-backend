# Zyplo Backend

> Express.js backend for Zyplo, powering authentication, workspaces, projects, tasks, time tracking, billing, invitations, GitHub integration, and real-time dashboard updates.

## Description

- REST API and realtime backend for the Zyplo project management platform
- Built with Express, MongoDB, JWT auth, Socket.IO, Stripe, Nodemailer, and Groq
- Deployed with Vercel-compatible Node routing via [`vercel.json`](./vercel.json)

## Features

- Email/password registration and login with JWT-based protected routes
- OAuth user sync endpoint for frontend Google and GitHub sign-in flows
- Workspace, project, board, and task management APIs
- Time tracking, active timers, and reporting endpoints
- Workspace invitations with email delivery and accept/reject flows
- User profile and dashboard bootstrap endpoints
- Stripe subscription checkout, portal, status, and webhook handling
- GitHub App callback, installation status, disconnect flow, and webhook ingestion
- Task comments and task activity endpoints
- Newsletter subscriber endpoint
- Socket.IO rooms for live task and notification updates
- Groq-powered task helper flow inside task creation/update logic

## Tech Stack

### Core

- Node.js
- Express 5
- MongoDB Node Driver
- JWT (`jsonwebtoken`)
- Zod

### Integrations

- Socket.IO
- Stripe
- Nodemailer
- Groq SDK
- Vercel Node runtime

## Installation

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd zyplo-backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create your local environment file

```bash
cp .env.example .env
```

## Environment Variables

Create a local `.env` file with placeholder values like these:

```env
PORT=5000
NODE_ENV=development
DB_USER=your_mongodb_username
DB_PASS=your_mongodb_password
NEXTAUTH_SECRET=your_jwt_secret
FRONTEND_URL=http://localhost:3000
APP_URL=http://localhost:3000
USER_EMAIL=your_smtp_email
USER_PASS=your_smtp_app_password
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
STRIPE_PRICE_STARTER_MONTHLY=your_stripe_price_id
STRIPE_PRICE_STARTER_YEARLY=your_stripe_price_id
STRIPE_PRICE_TEAM_MONTHLY=your_stripe_price_id
STRIPE_PRICE_TEAM_YEARLY=your_stripe_price_id
GITHUB_WEBHOOK_SECRET=your_github_webhook_secret
GROQ_API_KEY=your_groq_api_key
```

Notes:

- `DB_USER` and `DB_PASS` are used to build the MongoDB Atlas connection string in `index.js`.
- `NEXTAUTH_SECRET` is also used by this backend to verify JWTs coming from the paired frontend.
- `FRONTEND_URL` is used for CORS, invite links, and GitHub callback redirects.
- `APP_URL` is used for Stripe redirect URLs and falls back to `FRONTEND_URL` in billing flows.

## Usage

### Start the server

```bash
npm start
```

The API runs on `http://localhost:5000` by default.

### Run tests

```bash
npm test
```

## API Overview

### Auth

- `POST /auth/register`
- `POST /auth/login`
- `POST /auth/oauth`

### Dashboard

- `GET /dashboard/bootstrap`
- `GET /dashboard/profile`
- `PATCH /dashboard/profile`
- `POST /dashboard/workspaces`
- `POST /dashboard/projects`
- `POST /dashboard/tasks`
- `PATCH /dashboard/tasks/:taskId`
- `DELETE /dashboard/tasks/:taskId`
- `GET /dashboard/boards/:projectId`

### Time Tracking and Reports

- `POST /dashboard/tasks/:taskId/time/start`
- `POST /dashboard/time/:logId/stop`
- `GET /dashboard/tasks/:taskId/time`
- `GET /dashboard/time/active`
- `GET /dashboard/reports/timesheet`
- `GET /dashboard/reports/project/:projectId`
- `GET /dashboard/reports/task/:taskId`
- `GET /dashboard/reports/workspace/:workspaceId`

### Invitations and Members

- `GET /invites/:token`
- `POST /invites/:choice`
- `GET /workspaces/:workspaceId/invites`
- `POST /workspaces/:workspaceId/invites`
- `DELETE /workspaces/:workspaceId/invites/:inviteId`
- Workspace member management routes under `/dashboard/workspaces/:workspaceId/members/...`

### Billing

- `GET /api/billing/subscription`
- `POST /api/billing/checkout-session`
- `POST /api/billing/portal-session`
- `POST /api/billing/webhook`

Detailed billing behavior is documented in [`README.billing.md`](./README.billing.md).

### GitHub and Comments

- `POST /github/webhook`
- `GET /github/callback`
- `GET /dashboard/github/status`
- `DELETE /dashboard/github/disconnect`
- `GET /dashboard/tasks/:taskId/activities`
- `POST /dashboard/:id/comments`
- `GET /dashboard/comments/:taskId`
- `PUT /dashboard/:taskId/comments/:commentId`
- `DELETE /dashboard/:taskId/comments/:commentId`

## Project Structure

```text
zyplo-backend/
├── index.js
├── package.json
├── vercel.json
├── README.billing.md
├── README.md
└── .env.example
```

## Deployment

- `vercel.json` is configured to route all HTTP methods to `index.js`
- The server starts on `PORT` locally and uses Vercel Node runtime config for deployment

## Project Context

- This backend is part of the Zyplo group project.
- It serves the paired frontend application and shared product features.

## Team

- [Md Mahmud Ullah Hasan](https://github.com/rifat584)
- [Israt Jahan](https://github.com/israt9528)
- [Arifun Nahar Lipi](https://github.com/arifunnahar)
- [Md Al Helal Mohammod Bayijid](https://github.com/Dsx7)
- [MD Ebrahim Ali](https://github.com/ebrahim2355)

## Author

- Md Mahmud Ullah Hasan
- LinkedIn: [https://www.linkedin.com/in/md-mahmud-ullah-hasan/](https://www.linkedin.com/in/md-mahmud-ullah-hasan/)
- Email: [contactwithrifat@gmail.com](mailto:contactwithrifat@gmail.com)
