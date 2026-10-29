# 🚀 CMSC 128 Laboratory Activity 4 Guide: Refactor and Deployment

Author: Nikko Gabriel J. Hismaña

## 📋 Overview

This is the **fourth and final** activity in your CMSC 128 To-Do List series. Continue the merged, access-controlled application from [CMSC 128 Laboratory Activity 3 (Multi-Account CRUD: UBAC)](https://github.com/CMSC128-njh/CMSC128_Lab_3_MultiUserCRUD_UBAC) by **refactoring** it — Code, Backend, and UX/UI — and **deploying** it so it can be demoed on a device other than your own development machine.

This is a practice run for another very common real-world scenario: a feature-complete app still needs to be cleaned up, optimized, and shipped before anyone else can use it. "It works on my machine" is not good enough — your instructor must be able to open or install your app on **their own device** during the defense.

> ⚠️ **Read the "Deployment Requirements" and "Submission Requirements" sections below before you start.** Your deployment method depends on the platform you chose back in Activity 1 (web, mobile, or desktop), and you must have it ready and tested **before** your defense slot.

## 🎯 Learning Objectives

After completing this activity, each student should be able to:

1. Refactor existing frontend, backend, and database code for clarity, performance, and maintainability without changing its observable behavior.
2. Apply optimization techniques to backend/database operations (e.g., removing redundant queries/data, adding indexes, reducing payload size).
3. Polish an existing UI against HCI/UX best practices (consistency, feedback, accessibility, responsiveness).
4. Package and deploy an application so it is independently runnable by someone who does not have your development environment — via a hosted URL, a locally-shared build, or an installable file.
5. Explain and defend optimization and deployment decisions, including tradeoffs between local and remote deployment options.

> Ultimately, I just want to see that you can take a working app, make it better, and ship it so someone else can use it without needing your laptop or dev environment. And for the refactoring, I want you to be able to explain HOW and WHY you made the refactoring changes (code-wise) and how you applied your knowledge gained in CMSC 134 into your UX/UI imprvements.

## 🛠️ Prerequisites

Each student or pair should have:

- A completed Activity 1 (CRUD), Activity 2 (Authentication), and Activity 3 (UBAC). Basically, the same PUBLIC GitHub repository used throughout this course.
- Git and a code editor such as VS Code.
- Depending on your deployment path:
  - **Web apps:** a free account with a tunneling service (e.g., [ngrok](https://ngrok.com/)) for the minimum tier, and/or a free account with a hosting provider (see the [Deployment & Hosting Toolkit](#-deployment--hosting-toolkit) below) for the expanded tier.
  - **Mobile apps:** a physical phone (or the instructor's phone) and your dev machine connected to **the same Wi-Fi network**, and, for the expanded tier, the Android build tooling for your framework (Flutter SDK or Expo/EAS CLI).
  - **Desktop apps:** a packaging tool appropriate to your language (e.g., PyInstaller for Python) and, for the expanded tier, [Docker Desktop](https://www.docker.com/products/docker-desktop/) (with WSL2 enabled, since the instructor's machine runs **Windows 10 Enterprise 10.0.19045 x64**).
- The same DB-inspection tool from Activities 2–3 — **still required for the defense.**

## 🌿 Repository and Branch Requirements

1. Use the same PUBLIC GitHub repository from Activities 1–3.
2. Create a new branch named `act4-refactor` off of your latest merged work.
3. Do all refactoring and deployment work on `act4-refactor`, then **merge it back into `main`** (via `git merge` or a pull request) once it's complete and tested — `main` must reflect your final, deployed version.
4. For pairs, each student must use an identifiable branch and contribute through a pull request. No PR/branch/commit evidence means **zero score** for the activity.

## 🛠️ Tech Stack

Keep the tech stack you've been using since Activity 1 — this activity is about refining and shipping your existing app, not rewriting it. You may swap individual tools (e.g., switching your DB-inspection or hosting tool) as long as the core stack and your data stay the same. As before, no full stacks/frameworks/libraries beyond what you've already justified in earlier activities.

> **NOTE:** If there are features from Activities 1–3 that you never implemented, you do **not** need to implement them now. This activity's focus is refinement, optimization, and deployment — unimplemented earlier features will not hurt your score here.

## ✅ Application Requirements

### 🤏 Minimum Requirements

All of the following are required to receive a passing Features score.

#### 1. Code, Backend, and UX/UI Refactor

- **Code:** Clean up naming, remove dead code/console logs, and separate concerns (routes/controllers/models/views) if you haven't already.
- **Backend:** Remove redundant/duplicated data and unnecessary queries (e.g., N+1 queries, repeated lookups that could be joins), and make sure every endpoint still respects the UBAC rules from Activity 3.
- **UX/UI:** Audit your interface against basic HCI heuristics from your CMSC 134 class such as consistent navigation, clear feedback (loading/success/error states), readable contrast/typography, and no dead-end screens.

#### 2. Persistence (carried over from previous activities)

All data (accounts, sessions, tasks/lists) must still persist after a browser refresh/app restart and a backend restart.

#### 3. Runs on a Device Other Than Your Own

The instructor must be able to run or access your app **without using your development machine's `localhost`**. The exact requirement depends on your platform:

| Platform        | Minimum Deployment Requirement                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Web app**     | Exposed through a secure tunneling service (e.g., **ngrok** or a similar tool [see the toolkit below]). This is **not** the same as VS Code's built-in "Forward a Port" feature, which is account-gated and unreliable for an outside user. Use a dedicated tunneling tool instead, and actually test the generated public URL from another device/network before your defense. |
| **Mobile app**  | Produce a **web build** (e.g., `flutter build web`) and serve it from your machine on your local network. With your phone/the instructor's phone on **the same Wi-Fi network**, they open your machine's local-network IP and port (e.g., `http://192.168.1.23:8080`) in a mobile browser.                                                                                      |
| **Desktop app** | Package a **non-dockerized** installable/portable build (e.g., a PyInstaller `.exe`, a `dotnet publish` build, a `jpackage` build) and confirm it actually runs on a machine matching the instructor's spec: **Windows 10 Enterprise 10.0.19045 x64**. Do not assume your machine's installed runtimes/DLLs are present elsewhere — test on a clean machine or VM if you can.   |

> **Why the distinction matters:** A link that only works while your laptop is open and your tunnel session is active is a **minimum**-tier deployment, not an expanded one. A build an instructor must install locally also only counts toward the minimum tier unless it's containerized per the expanded tier below.

### ➕ Expanded Requirements

All of the following are required for the full Features score.

#### 1. All Previous Expanded Features Implemented

Every expanded feature you committed to in Activities 1–3 (undo/filter/calendar, profile/password recovery, collaborative lists, etc.) should still work after your refactor.

#### 2. Full Deployment (platform-specific)

| Platform        | Expanded Deployment Requirement                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Web app**     | **Full remote hosting**. Your app is deployed to an actual hosting provider with a persistent, "always-on" URL that does not depend on your laptop or tunnel session being active. In other words, even if the instructor uses a different network, they should still be able to access your app. See the toolkit below for free options.                                                                                                                                                                                                                                                              |
| **Mobile app**  | Produce an **installable file**. A signed/release **`.apk`** (Flutter) or an Expo **EAS build** that the instructor can side-load directly onto their phone, instead of only reaching a web build over Wi-Fi. Share it via google drive.                                                                                                                                                                                                                                                                                                                                                               |
| **Desktop app** | **Dockerize** your app (or use an equivalent containerization approach) so it's ready to use on the instructor's machine with **no manual dependency installation**, `docker compose up` (or similar) should be enough. If your app is GUI-based and difficult to containerize directly, consider exposing a local web-based UI so the Docker container only needs to run your (web) server. Document this tradeoff in your README. **TL;DR as long as I don't need to install any dependencies manually, and the app should work out of the box, I'll consider it as the expanded req has been met.** |

### 🔒 Backend Optimization and Security Requirements

_NOTE: This affects your Backend Design score._

1. Eliminate redundant/duplicated data in your schema (e.g., storing the same user info inside every task record instead of referencing it by ID).
2. Reduce unnecessary round-trips: batch or join queries where reasonable instead of looping and querying per item.
3. Keep UBAC/ownership checks from Activity 3 intact after refactoring — refactoring must not reopen IDOR issues.
4. Do not commit database credentials, API keys, `.env` files, or tunnel/hosting tokens to GitHub. Use `.gitignore` and environment variables, including on your hosting provider's dashboard.
5. Be ready to explain **what** you optimized and **why** it's faster/safer than before (e.g., "I replaced 3 sequential queries with 1 join," or "I added an index on `user_id` since every task query filters by it").

### 🎨 Frontend/UX-UI Requirements

_NOTE: This affects your Frontend Design score._

1. Consistent layout, spacing, and component styling across all pages/screens.
2. Clear, visible feedback for every action (loading indicators, success/error messages, disabled states while submitting).
3. Legible typography and sufficient color contrast; no unlabeled icons/buttons.
4. Responsive to different screen sizes if web-based (at minimum, usable on a phone browser, since that may be how it's demoed).
5. No raw/unstyled error pages, stack traces, or broken layouts visible to an end user.

### 🤯 BONUS: Pentesting OR Advanced Feature (+2 Points)

Pentesting:
1. Depending on your tech stack, try to break your To Do List app through user input (or URL modification)
2. To get the bonus, you should be able to show your pentest and how you safeguard your application (include these in the Readme)
3. For verification, we'll run the pentest without your security feature (attack works), and with your security feature (attack prevented).

_EXAMPLE: For those utilizing SQL, SQL Injection + your security feature to prevent them._

OR

Advanced Feature:
Determine an **advanced** feature that makes sense in your app (i.e. a chatbot, voice recog, smart parsing, built-in focus timers, etc).
Score depends on how advanced and how well the feature has been implemented (1-2 points).


### 📄 README Requirements

The repository's `main` branch must include a final, updated `README.md` containing:

- Which backend (language/framework) and database you chose, and a short summary of what you refactored/optimized and why.
- How to run the app locally (setup steps, dependencies, commands) — this should still work for someone cloning your repo fresh.
- **How to access your deployed app** — the live/hosted URL (expanded) or the tunnel/local-network/installable-file instructions (minimum), including any setup needed on the instructor's end (e.g., "enable install from unknown sources," "connect to the same Wi-Fi," "run `docker compose up`").
- Example API endpoints (for connecting to your database), consistent with earlier activities.

> **NOTE:** This is worth 1 point in your Features rubrics.

### 🧾 Final Commit

After completing the activity, commit the final version on `main` with:

```text
cmsc128-Final-Lab
```

This commit (on `main`, after merging `act4-refactor`) is the basis of your submission date.

**NOTE:** Minus 1 point for not following this.

## 🧰 Deployment & Hosting Toolkit

Use this as a starting menu, not an exhaustive list — any comparable free/low-cost tool is acceptable as long as you can explain how it works. There is literally dozens of repos on GitHub that provide/compile all free hosting options, so if you find a better one, feel free to use it.

### 🔌 Tunneling Tools (Minimum Tier — Web Apps)

Use one of these instead of VS Code's built-in port forwarding:

- [ngrok](https://ngrok.com/) — most common, free tier gives you a temporary public HTTPS URL.
- [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/) — free, can also be made persistent with a Cloudflare account/domain.
- [localtunnel](https://github.com/localtunnel/localtunnel) — open-source, no account required.
- [Tailscale Funnel](https://tailscale.com/kb/1223/funnel) — free for personal use, also useful for the mobile "same Wi-Fi/network" tier if devices aren't literally on the same router.
- [Pinggy](https://pinggy.io/) / [Serveo](https://serveo.net/) — lightweight SSH-based alternatives.

### 🌐 Full Remote Hosting (Expanded Tier — Web Apps)

Pick based on the stack you chose in Activity 1:

| Your Stack (from Lab 1)                                       | Suggested Free Hosting/Deployment                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| HTML/CSS/JS + **Flask** (Python) + SQLite                     | [Render](https://render.com/) (free web service), [Railway](https://railway.app/), [PythonAnywhere](https://www.pythonanywhere.com/), [Fly.io](https://fly.io/) — note SQLite needs a persistent disk/volume add-on, or switch to a hosted Postgres (below) for reliability.                                                                                                                                                                           |
| **Django** (Python) + SQLite/PostgreSQL                       | Same as Flask above; pair with a hosted Postgres instead of SQLite for a persistent free tier.                                                                                                                                                                                                                                                                                                                                                         |
| **MERN**/**MEAN** (MongoDB + Express + React/Angular + Node)  | Frontend: [Vercel](https://vercel.com/), [Netlify](https://www.netlify.com/), or GitHub Pages (static builds). Backend: [Render](https://render.com/), [Railway](https://railway.app/), [Fly.io](https://fly.io/). Database: [MongoDB Atlas](https://www.mongodb.com/atlas) free M0 cluster.                                                                                                                                                           |
| **FERN**/**FEAN** (Firebase + Express + React/Angular + Node) | Frontend: [Firebase Hosting](https://firebase.google.com/docs/hosting). Backend: Render/Railway or [Cloud Functions for Firebase](https://firebase.google.com/docs/functions). Database: Firestore/Realtime Database (free Spark plan).                                                                                                                                                                                                                |
| **Laravel (PHP)** + MySQL/PostgreSQL                          | [Render](https://render.com/) or [Railway](https://railway.app/) via a Docker image (both support PHP through a Dockerfile), [Fly.io](https://fly.io/) with Docker, or free shared hosts such as [InfinityFree](https://www.infinityfree.net/)/[000webhost](https://www.000webhost.com/) for simpler needs. Database: [Supabase](https://supabase.com/) or [Aiven](https://aiven.io/) free Postgres/MySQL, or Railway's managed MySQL/Postgres add-on. |
| **FlutterFire** (web build)                                   | [Firebase Hosting](https://firebase.google.com/docs/hosting), [Vercel](https://vercel.com/), or [Netlify](https://www.netlify.com/) for the `flutter build web` output.                                                                                                                                                                                                                                                                                |
| Any static frontend                                           | [GitHub Pages](https://pages.github.com/), [Netlify](https://www.netlify.com/), [Vercel](https://vercel.com/), [Cloudflare Pages](https://pages.cloudflare.com/).                                                                                                                                                                                                                                                                                      |

**Database-only hosting (if you need a managed DB separate from your app host):** [Supabase](https://supabase.com/) (Postgres), [Neon](https://neon.tech/) (serverless Postgres), [MongoDB Atlas](https://www.mongodb.com/atlas) (free tier), [Turso](https://turso.tech/) (hosted SQLite/libSQL), [Railway](https://railway.app/) (Postgres/MySQL add-ons).

> Free tiers change their terms over time (and some, like PlanetScale's former free MySQL tier, have been discontinued) — double-check current limits before committing to one, and have a backup option in mind.

### 📱 Mobile Builds and Distribution

- **Minimum (same Wi-Fi):** `flutter build web` (or your framework's web build) served locally — e.g., `python -m http.server` or your framework's own dev server bound to `0.0.0.0` — then opened from the instructor's phone browser via your machine's local IP.
- **Expanded (installable file):**
  - **Flutter:** `flutter build apk --release` → share the generated `.apk` directly (e.g., via USB, Google Drive link, or Wi-Fi transfer); the instructor enables "install from unknown sources" to side-load it.
  - **Expo/React Native:** `eas build -p android --profile preview` via [EAS Build](https://docs.expo.dev/build/introduction/) to get a shareable APK/install link.

### 🖥️ Desktop Packaging and Containerization

- **Minimum (installable/portable build, non-dockerized):**
  - **Python:** [PyInstaller](https://pyinstaller.org/) (`pyinstaller --onefile --windowed app.py`) or [auto-py-to-exe](https://github.com/brentvollebregt/auto-py-to-exe) for a GUI wrapper; optionally wrap the output with [Inno Setup](https://jrsoftware.org/isinfo.php) for a proper Windows installer.
  - **.NET:** `dotnet publish -r win-x64 --self-contained` for a self-contained executable.
  - **Java:** [`jpackage`](https://docs.oracle.com/en/java/javase/17/jpackage/) to produce a native installer/app image.
  - **C++ (Qt):** `windeployqt` + an installer tool such as Inno Setup or NSIS.
  - Always test the packaged build on a machine/VM that matches the instructor's spec (**Windows 10 Enterprise 10.0.19045 x64**) rather than assuming your own machine's runtimes are present elsewhere.
- **Expanded (Dockerized):** Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) (with the WSL2 backend, which is compatible with the instructor's Windows 10 Enterprise machine), write a `Dockerfile` (and `docker-compose.yml` if you have a separate DB service), and confirm `docker compose up` brings the whole app online with no extra manual setup. If your app is a native GUI app that's awkward to containerize, consider shipping a web-based UI/admin view instead so only the server needs to run in the container — document this decision in your README.

## 📤 Submission Requirements

### Deliverables

1. Your GitHub repository link, with the `act4-refactor` branch merged into `main`, and for pairs, the required individual branch/PR evidence.
2. The completed, refactored application with source code and final `README.md` on `main`.
3. Your working deployment, ready **before** the defense:
   - Web: a tested tunnel URL (minimum) or a live hosted URL (expanded).
   - Mobile: your dev machine and a phone on the same Wi-Fi network (minimum), or an installable APK/EAS build ready to side-load (expanded).
   - Desktop: your packaged installable/portable build (minimum), or your Docker setup ready to run with one command (expanded).
4. Your DB-inspection tool from prior activities, installed and ready.
5. A live F2F demonstration: show the refactor/optimizations you made, then have the instructor access or install the app on **their own device** using your chosen deployment method.
6. A Code Defense. Each student must be able to explain their own implementation — including what was refactored and how deployment was set up — without notes, outside assistance, or an AI tool during the defense.

**For pairs:** Ensure you have pull requests (or at least branches) showing each partner's contribution. No PRs/branches/commits means a zero score.

Refer to the class Google Sheet for the submission/defense schedule and deadlines(and early commit bonuses).

## 🗣️ Possible Defense Questions

The following questions are examples and are not exhaustive.

### Refactoring and Optimization

1. What specifically did you refactor in your code, backend, and UI, and why?
2. Show a query or data access pattern you optimized. What was it before, and what is it now?
3. How did you make sure your refactor didn't break UBAC/ownership checks from Activity 3?
4. What redundant data or duplicate logic did you find and remove?
5. How would you measure whether your backend is actually faster/more efficient now?

### Deployment

1. Walk through exactly how the instructor can access or install your app right now, step by step.
2. What's the difference between what you did for the minimum tier versus the expanded tier?
3. If you used a tunneling tool (ngrok/etc.), why is this different from VS Code's port forwarding, and why is it still not equivalent to "real" hosting?
4. If you did full remote hosting: what host/service did you use, and how does your deployed app connect to your database?
5. If you built a mobile APK or Dockerized your desktop app: walk through the build/packaging steps you ran.
6. What would happen to your deployment if your laptop were turned off right now?
7. What secrets/credentials did you have to keep out of your public GitHub repo, and how did you manage them in your deployed environment?

### Code Defense

1. Open the part of your code you changed the most during this refactor and explain exactly what changed.
2. Trace a request from the instructor's device, through your deployment setup, to your backend and database, and back.
3. Point to one optimization decision and justify it with a concrete before/after comparison.

## 📊 Rubrics for Grading

| Criteria                     | Excellent                                                                                                                                                         | Good                                                                                              | Satisfactory                                                                                            | Needs Improvement                                                                                                                                                              |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Features (10 pts)**        | All expanded deployment/feature requirements implemented. No/minimal bugs. **(10-9)**                                                                             | Expanded features implemented but with some bugs. **(8-7)**                                       | Only minimum features/deployment implemented. **(6)**                                                   | Only minimum features attempted, with significant bugs or issues running on another machine/device. **(5-1)**                                                                  |
| **Frontend Design (10 pts)** | Polished UX/UI, follows HCI best practices with no/negligible issues, consistent and responsive across devices. **(10-9)**                                        | Good UX/UI with minor, non-disruptive issues. **(8-7)**                                           | Usable interface but with a few noticeable design issues. **(6)**                                       | Several and/or significant UX/UI issues that would confuse a real user. **(5-1)**                                                                                              |
| **Backend Design (10 pts)**  | Backend and database are fully optimized (no repeating/redundant data, efficient queries), and the student can clearly explain the optimizations made. **(10-9)** | Backend is mostly optimized with minor inefficiencies or gaps. **(8-7)**                          | Works as intended but with clear, numerous areas for improvement. **(6)**                               | Several issues including unoptimized backend, security issues, or broken session/UBAC handling. **(5-1)**                                                                      |
| **Code Defense (10 pts)**    | Clearly explains every refactored part of the code and the deployment setup; can trace a request end to end on the deployed app. **(10-9)**                       | Explains most of the code/deployment correctly but struggles with a few specific parts. **(8-7)** | Can only explain the code/deployment at a surface level; struggles with implementation details. **(6)** | **Cannot recall, explain, or trace their own source code or deployment setup** when asked. **AUTOMATIC FAILURE for this activity**, regardless of other rubric scores. **(0)** |

**TOTAL: 40 (PASSING SCORE: 24/40)**

> ⚠️ **Note on Code Defense**: As with every prior activity, this checks whether **you** wrote, understand, and can defend **your own code and deployment decisions**. Using AI tools to help you learn, refactor, or debug is fine; not understanding what your own program does — or how it got deployed — is not, and results in an automatic failure for this activity regardless of how polished the final app looks.

## 📁 Suggested Project Structure

Your structure from Activity 3 should mostly carry over, with deployment-specific additions depending on your platform:

```text
your-project/
├── frontend/ or src/          # pages, screens, components, styles
├── backend/ or server/        # routes, controllers, middleware (incl. ownership checks)
├── models/ or database/       # schema for users, tasks, and list membership
├── Dockerfile                 # expanded desktop tier, or containerized web backend
├── docker-compose.yml         # if your app has multiple services (app + db)
├── .env.example                # variable names only; no real secrets
├── .gitignore
└── README.md                  # updated with deployment/access instructions
```

## 📚 Helpful Resources

- [Render Free Tier Docs](https://render.com/docs/free)
- [Railway Docs](https://docs.railway.app/)
- [Fly.io Docs](https://fly.io/docs/)
- [Vercel Docs](https://vercel.com/docs) / [Netlify Docs](https://docs.netlify.com/)
- [Firebase Hosting Docs](https://firebase.google.com/docs/hosting)
- [Supabase Docs](https://supabase.com/docs) / [Neon Docs](https://neon.tech/docs/introduction)
- [ngrok Docs](https://ngrok.com/docs) / [Cloudflare Tunnel Docs](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/)
- [PyInstaller Docs](https://pyinstaller.org/en/stable/)
- [Docker Desktop Docs](https://docs.docker.com/desktop/) / [Docker Compose Docs](https://docs.docker.com/compose/)
- [Flutter: Build and Release for Android](https://docs.flutter.dev/deployment/android)
- [Expo EAS Build Docs](https://docs.expo.dev/build/introduction/)
- [Web Content Accessibility Guidelines (WCAG) Quick Reference](https://www.w3.org/WAI/WCAG21/quickref/)

## 💡 Support

If you encounter issues:

1. Check your hosting/packaging tool's official documentation first — most deployment failures are free-tier configuration issues (build commands, environment variables, start commands).
2. Test your deployment from a device/network that is **not** your own dev machine before the defense — a friend's phone on mobile data is a good sanity check for "real" hosting.
3. Ask classmates for conceptual help, but do not copy their deployment config or code — you will be asked to explain your own setup during the defense.
4. Use AI tools (ChatGPT, Claude, Copilot) for refactoring/debugging/deployment troubleshooting — but understand every change, since you will be asked to defend it.
5. Contact the instructor during office hours when you are blocked.

## 🎉 Closing Note

This is the final activity in the indiv/pair lab. Congratulations on taking your To-Do List app from a basic CRUD prototype all the way to a refactored, deployed, multi-user application. Good luck, guys!
