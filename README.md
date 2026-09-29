# Step-by-Step Introduction to the React Framework

📖 **Read the tutorial: [https://stahe.github.io/en-react-etape-par-etape-sept-2026/](https://stahe.github.io/en-react-etape-par-etape-sept-2026/)**

This course teaches you how to build a web application using the [React](https://react.dev) 19.3 library: a **single-page application** (SPA), where pages are rendered **in the browser** using JSON data from a server.

It follows up on the course [Step-by-Step Introduction to the NestJS Web Framework](https://stahe.github.io/nestjs-html-sept-2026/), offering a different perspective, and follows the outline of the course [Step-by-Step Introduction to the Vue.js Framework](https://stahe.github.io/ en-vuejs-step-by-step-sept-2026/) and [Step-by-Step Introduction to the Angular Framework](https://stahe.github.io/en-angular-etape-par-etape-sept-2026/): same server, same pages, written in the React style.

| NestJS Course | React Course |
|---|---|
| the server generates HTML pages (Handlebars) | the browser generates pages (React) |
| the browser displays what it receives | the server only returns JSON |
| controllers, views, `res.render` | components, router, hooks |
| guards `JwtAuthGuard`, `RolesGuard` | router guards (React Router middleware); the server maintains its own |
| dictionaries read by the server | dictionaries on the client (i18next); the server returns only keys |
| flash message in a cookie | flash message in a state store |

The pages themselves remain unchanged: they are those from the **RdvMedecins** application already presented with the other frameworks.

## The Approach: Many Short Examples, Then a Case Study

The course is structured around **25 short examples**, each focused on a single concept. They form a single Vite project: a single `npm install` command, followed by `npm start <example>` to run one.

| Chapter | Content | Examples |
|---|---|---|
| Getting Started | a Vite project, function components, JSX, state (`useState`, `useReducer`), events, controlled fields, validation, React Hook Form, formatting (`Intl`) | 01–09 |
| Components | props, function props, `children`, lifecycle (`useEffect`, `useEffectEvent`), contexts, custom hooks, confirmation dialog (`createPortal`) | 10–16 |
| Routing | React Router 8: routes, parameters, query, lazy loading, `<title>`, middleware | 17–18 |
| Asynchronous Operations and Shared State | timers, anti-bounce, expired responses, `use()` + `<Suspense>`, Zustand, `localStorage`, `<Activity>` | 19–20 |
| Internationalization | i18next / react-i18next: parameters, plurals, dates, amounts | 21 |
| The Server: A Black Box | setting up the JSON server, its API, 48 `curl` examples | – |
| Communicating with the Server | `fetch`, Vite proxy, `httpOnly` cookies, `useActionState`, API access layer, TanStack Query, server errors attached to fields | 22–25 |

Each example is presented with its complete code, commented line by line, and a screenshot of its execution.

## The Server: A Black Box

The server is the NestJS server from the previous lesson, whose controllers return **JSON**—the same as for the Vue.js and Angular clients. This lesson treats it as a **black box**: we install it, study its API, and query it with `curl`—but we don’t need to read its code (which is provided and commented for the curious).

- All errors have the same format: `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — **keys** for translation, never plain text;
- Authentication via a JWT token in an `httpOnly` / `sameSite=strict` cookie: the client-side JavaScript code never sees the token;
- CSRF protection: `sameSite` cookie, and all POST requests must be in JSON;
- A “test mode” for the CAPTCHA so you can query the API with `curl`.

## The Case Study: The RdvMedecins React Client

A complete application for **booking appointments at a doctor’s office**, with **all** of its files (about forty) listed and commented.

- **Modern React**: function components and hooks, form actions, `<title>` in components, React Router 8 in “data” mode (middleware, on-demand page loading), TanStack Query for server data, Zustand for shared state.
- **Three roles**: `ADMIN` (manages doctors and clients), `DOCTOR` (schedules and cancels appointments), `USER` (the patient: books appointments for themselves, manages their account).
- **Privacy**: a patient never receives the names of other patients—the server does not send them.
- **The entire page state in the URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` reopens the booking window after pressing F5; the Previous/Next buttons work.
- **Server-side validation**: Forms display errors returned by the API below each field; optimistic locking, duplicate names, username already in use, etc.
- **Session**: Restored after pressing F5 (`GET /api/auth/moi`), expiration managed in a single location (the function common to all requests, 401 response).
- **French / English**, translated tab titles, keyboard-accessible confirmation window, Bootstrap 5.
- **Deployment**: the compiled client is served by the JSON server itself (same origin, no CORS).

## Repository contents

```
exemples-react/            the 25 short examples (a single Vite project)
rdvmedecins-nestjs-json/   the RdvMedecins JSON server (the “black box”)
rdvmedecins-react/         the React client from the case study
```

## Technologies

React 19.3 · TypeScript 6.0 · Vite 8 · React Router 8.4 · TanStack Query 5 · Zustand 5 · i18next 26 / react-i18next 17 · React Hook Form 7 (example 08) · Bootstrap 5.3 · server-side: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Prerequisites

- A basic understanding of JavaScript (or TypeScript), HTML, and the HTTP protocol.
- Node.js 24 (or at least 22.22), Visual Studio Code, the React Developer Tools browser extension, and a MySQL server (e.g., Laragon on Windows) for the JSON server. Installation instructions are provided in the course appendices.

## Author

This course, its examples, the JSON server, and the case study were written by **Claude**, the AI from [Anthropic](https://www.anthropic.com) (September 2026), at the request of **Serge Tahé**.
