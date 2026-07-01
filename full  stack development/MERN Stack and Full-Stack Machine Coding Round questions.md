# MERN Stack & Full-Stack Machine Coding Round Questions

This list features frequently asked machine coding round questions for MERN/Full-Stack Developer roles (ranging from Junior to Senior levels). 

---

## 🛠️ Machine Coding Round Ground Rules
* **Time limit:** Usually 60 to 120 minutes.
* **Focus areas:** Separation of concerns, code readability, state management, modular design, error handling, performance optimization (re-renders, debounce), and a working UI-to-API connection.

---

## 🏎️ Frontend & Core JavaScript Problems

### 1. Advanced Search Component with Debounce & Throttle
* **Requirements:** Build a search input that fetches data from a mock/public API.
* **Key Tasks:** * Implement custom `useDebounce` or `useThrottle` hooks from scratch.
  * Show loading, error, and empty states.
  * Add a list cache to prevent redundant API calls for the same query.

### 2. Infinite Scroll vs. Pagination Component
* **Requirements:** Render a large dataset of products or posts.
* **Key Tasks:**
  * Build a pagination bar (Previous, Next, page numbers) with dynamically computed limits.
  * Alternatively, implement an Infinite Scroll layout using the `IntersectionObserver` API.

### 3. Interactive UI Components
* **Carousel / Slideshow:** Build a responsive image slider with Auto-play, Pause-on-hover, Next/Prev buttons, and indicator dots.
* **Custom Modal / Dialog:** Build an accessible modal with overlay clicking, a close button, and an overlay escape key exit.
* **Multi-Step Form Wizard:** Build a 3-step checkout or signup form with client-side validation per step, a summary page, and state retention when hitting "Back".

---

## 🌐 Full-Stack (React + Node + Express + MongoDB) Problems

### 1. Real-Time Collaborative To-Do App
* **Frontend:** A React app featuring task addition, toggling, filtering (All, Active, Completed), and categorization.
* **Backend:** Express API with endpoints to handle full CRUD operations (`GET`, `POST`, `PUT`, `DELETE`).
* **Database:** MongoDB schema handling separate `tasks` and `categories` collections.
* **Bonus:** Live syncing across open windows using WebSockets (`Socket.io`).

### 2. User Authentication System (JWT)
* **Frontend:** Login and Signup forms with standard validations (Email format, Password strength).
* **Backend:** Express app utilizing `bcryptjs` for password hashing and `jsonwebtoken` for issuing tokens.
* **Database:** Securely store user records.
* **Key Requirement:** Protect specific frontend routes and backend APIs using custom verification middleware.

### 3. File Upload & Media Gallery
* **Frontend:** Drag-and-drop file upload zone with upload progress indicators.
* **Backend:** Express route handling files via `multer` storing files locally or referencing Cloudinary/S3.
* **Database:** Track file metadata (filename, size, file path, upload date).

### 4. Custom URL Shortener
* **Frontend:** Simple form allowing a user to paste a long URL and view a generated shortened link.
* **Backend:** An API generating a unique hash code for incoming URLs. Create a fallback wildcard route (`/:code`) that finds the original address and issues a HTTP 302 redirect.
* **Database:** Schema tracking `{ shortCode, originalUrl, clickCount }`.

### 5. Simple E-Commerce Cart & Product Catalog
* **Frontend:** Grid layout listing items with dynamic search filters, category dropdowns, and an "Add to Cart" button.
* **Backend:** REST endpoints returning paginated product entries.
* **Key Tasks:** Sync the checkout cart persistently across local storage and the database.

---

## 🏗️ System Design & Backend-Heavy Coding

### 1. Rate Limiting Middleware
* **Requirements:** Write a custom custom Express middleware function implementing a sliding or fixed-window rate limiter without installing 3rd party packages.
* **Key Tasks:** Limit unique IP addresses to `X` requests per `Y` minutes. (Can use an in-memory object or Redis).

### 2. Role-Based Access Control (RBAC)
* **Requirements:** Extend an authentication setup to restrict API endpoints depending on user roles (`Admin`, `Editor`, `User`).
* **Key Tasks:** Build a reusable `checkRole(['Admin'])` middleware that halts unprivileged request lifecycles early with a `403 Forbidden` code.

---

## 💡 Practical Evaluation Metrics
When review boards inspect your code, they score heavily on:
1. **Directory Architecture:** Clean separation of components, hooks, controllers, models, and routes.
2. **Error Safety:** Proper `try/catch` wrappers, global Express error-handling middleware, and React Error Boundaries.
3. **Efficiency:** Avoiding needless component re-renders (via `useMemo`/`useCallback`) and query performance indexes in MongoDB.


## 🚀 Senior & Lead Level Advanced Scenarios

### 1. Job Queue / Task Processing System
* **Requirements:** Build an application where clients can submit heavy data-processing jobs (e.g., CSV parsing or PDF report generation) that shouldn't block the main Express server thread.
* **Key Tasks:** * Use a Redis-backed queue system like `BullMQ` or an in-memory queue to process tasks asynchronously.
  * Implement WebSockets to push live progress updates (e.g., "Parsing 45% complete") back to the React UI.

### 2. Live Chat Application with Persistence
* **Frontend:** A dashboard showing a list of conversations and an active chat window with typing indicators.
* **Backend:** Setup a raw Node.js HTTP server configured with `Socket.io` or native `ws`. 
* **Key Tasks:** * Write logic to fetch message history on-demand when clicking a user conversation (pagination/cursors).
  * Handle edge cases like connection drops, reconnection strategies, and marking messages as "read".

### 3. Distributed Tracing & Centralized Logging Middleware
* **Requirements:** Create a system to trace a single request's lifecycle across multiple internal modules.
* **Key Tasks:** * Write an Express middleware that checks for a `X-Correlation-ID` header, generates a new UUID if missing, and appends it to all subsequent logs and down-stream API requests.
  * Set up a global error interceptor that logs the full stack trace along with the exact query state that caused the failure.

---

## ⚡ Mock Coding Challenge: Build a Notification Center
*Try to complete this mini-project within 90 minutes.*

### The Goal
Create a notification dispatching and viewing service. 

### Specifications
1. **The API (`Node/Express`):**
   * `POST /api/notifications` - Dispatches a notification to specific users with a body payload (`{ userId, message, type: 'info' | 'alert' }`).
   * `GET /api/notifications/:userId` - Retrieves all notifications for a specific user.
   * `PATCH /api/notifications/:id/read` - Marks a single notification as read.
2. **The Database (`MongoDB`):**
   * Define a schema ensuring proper indices on `userId` and `createdAt` for rapid querying.
3. **The Interface (`React`):**
   * Design a bell icon in a navigation bar with a red badge indicating unread counts.
   * Clicking the bell opens a dropdown listing the notifications with distinct styling for read vs. unread states.
   * Use polling or WebSockets to instantly update the UI when a new notification is posted.

---

## 🛠️ Cheat Sheet: Ideal Boilerplate Architecture

When the timer starts, organizing your directory structure quickly gives you a massive advantage. Stick to a standard convention:

```text
my-mern-app/
├── backend/
│   ├── config/             # DB connections, environment variables
│   ├── controllers/        # Request handling logic
│   ├── models/             # Mongoose schemas
│   ├── routes/             # Express route definitions
│   ├── middleware/         # Auth, validation, error-handlers
│   └── server.js           # App entry point
└── frontend/
    ├── src/
    │   ├── components/     # Reusable UI elements (Button, Modal)
    │   ├── hooks/          # Custom React hooks (useAuth, useFetch)
    │   ├── context/        # Global state management (Theme, Auth)
    │   ├── App.jsx
    │   └── main.jsx



    ## 🧪 Testing & Edge Case Scenarios

### 1. Robust Component Testing (Frontend)
* **Requirements:** Write unit and integration tests for a complex component (e.g., the Cart or Multi-Step Form) using React Testing Library and Jest/Vitest.
* **Key Tasks:**
  * Mock API responses using `msw` (Mock Service Worker) to test loading and network error states.
  * Test user interactions: verify that typing into fields updates state, and clicking "Submit" fires the correct API payload.
  * Assert that validation error messages appear dynamically when invalid data is supplied.

### 2. Integration & API Testing (Backend)
* **Requirements:** Set up an isolated testing environment for your Express routes using `Supertest` and an in-memory MongoDB server (`mongodb-memory-server`).
* **Key Tasks:**
  * Write test suites for authentication pipelines (`POST /api/auth/register` and `/api/auth/login`).
  * Ensure database state resets between individual test runs to avoid cross-contamination.
  * Verify that edge cases—like submitting duplicate emails or malformed payloads—properly return `400 Bad Request` or `409 Conflict` statuses.

---

## 🔒 Security & Data Sanitization Guidelines

In advanced machine coding rounds, implement these security quick-wins to stand out:

* **XSS Protection:** Sanitize incoming user inputs on the backend using libraries like `dompurify` or `express-mongo-sanitize` to prevent script injection attacks.
* **Security Headers:** Drop in `helmet` middleware into your Express application instance to automatically assign secure HTTP response headers.
* **CORS Management:** Configure the `cors` middleware explicitly to white-list only the frontend port rather than utilizing the insecure wildcard `*`.
* **Data Masking:** Ensure your Mongoose schemas explicitly set `select: false` on sensitive properties (like fields holding hashed passwords) so they aren't accidentally exposed in general queries.

---

## 📈 Checklist Before You Hand Over Your Code

Before signaling to the reviewer that you have completed the assignment, double-check this list:

- [ ] **No Dead Code:** Removed all unused variables, empty functions, and messy `console.log` lines.
- [ ] **Environment Variables:** Confidential configurations (like Mongo URIs or JWT secrets) are safely isolated into a `.env.example` file instead of hardcoded.
- [ ] **Graceful Degradation:** The UI displays clean, user-friendly fallback components if the backend API goes offline or drops a connection.
- [ ] **Responsive Flow:** The layout scales cleanly using CSS Flexbox/Grid and media queries across mobile, tablet, and desktop views.
- [ ] **Valid HTTP Status Codes:** The backend responds using appropriate semantic statuses (`200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `500 Server Error`).
- [ ] **Clear README:** A concise `README.md` file is present detailing exactly how to install dependencies, set up environment keys, and boot up both the frontend and backend servers.




## 💾 State Management & Data Flow Architecture

### 1. Complex Client-Side State Management
* **Scenario:** Imagine a dashboard containing multiple standalone analytical widgets that need to read and write to the same central data matrix (e.g., a real-time financial tracking dashboard).
* **Key Tasks:** * Demonstrate when to use local state (`useState`), when to lift state up, and when to migrate to global stores like the React Context API or Redux Toolkit (`@reduxjs/toolkit`).
  * Implement an optimal structure to prevent the "prop-drilling" anti-pattern.
  * Optimize rendering pipelines using structural selectors or slicing to ensure that an update in Widget A does not trigger costly, unnecessary re-renders across unaffected branches of the DOM tree.

### 2. High-Frequency State Synchronization (Optimistic UI Updates)
* **Scenario:** A social media feed component with "Like" and "Bookmark" toggles where network latency shouldn't make the app feel sluggish to the user.
* **Key Tasks:**
  * Implement an optimistic UI update strategy: immediately alter local React state to reflect success, spin up the network request asynchronously, and write robust rollback logic inside the `.catch()` block if the server fires back an error.

---

## ⚡ Deployment & Production Readiness

When requested to deploy or present a system architecture summary, the evaluator looks for structural preparedness:

### Monorepo vs. Polyrepo Setup
* If delivering the app as a single package, configure a root-level `package.json` utilizing workspace scripts so a evaluator can run a single command (like `npm run dev:all`) to spin up both client and server nodes concurrently using tools like `concurrently` or `nodemon`.

### Database Optimization Checklist
- [ ] **Mongoose Indexes:** Ensure unique constraints (e.g., `unique: true` on fields like emails or usernames) are properly backed by database indexes.
- [ ] **Connection Pooling:** Wrap your database boot sequences in clean, reusable connection singletons that reconnect gracefully if the database cluster restarts.
- [ ] **Data Validation:** Implement defensive validation at the database boundary level utilizing Mongoose Built-in validators alongside API validation frameworks like `Joi` or `Zod`.

---

## 📝 Practice Log

| Priority | Challenge Title | Est. Time | Focus Area | Status |
| :--- | :--- | :--- | :--- | :--- |
| 🔴 **High** | Multi-Step Form with DB Save | 90 mins | Full-Stack Context & Validation | *Pending* |
| 🔴 **High** | Custom Debounced API Search Grid | 60 mins | Frontend Optimization / Hooks | *Pending* |
| 🟡 **Med** | Token Auth + Role Middleware | 70 mins | System Backend Security | *Pending* |
| 🟢 **Low** | Media Upload & Gallery View | 120 mins | Static Assets & Middleware | *Pending* |