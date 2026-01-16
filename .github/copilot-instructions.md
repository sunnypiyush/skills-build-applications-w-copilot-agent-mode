<!--
Guidance for AI coding agents working in this repository.
Keep this file short, concrete, and focused on patterns that are discoverable
from the repo and the workshop documentation in `docs/`.
-->

# Copilot Agent Instructions — OctoFit Tracker Workshop

Purpose: give an AI coding agent the specific, actionable context needed to be
productive in this workspace (OctoFit Tracker workshop materials and starter
app design).

- **Big picture**: this project is a full-stack web prototype.
  - `frontend/` (React) connects to a Django REST backend.
  - `backend/` (Django + DRF) is configured to use MongoDB via `djongo`/`pymongo`.
  - Docs and workshop narrative live in `docs/` (see `docs/octofit_story.md`).

- **Key files & locations** (look here first):
  - `README.md` — repo overview and exercise link.
  - `docs/octofit_story.md` — product goals, stack, and workshop flow.
  - `backend/requirements.txt` — required Python packages and versions.
  - `backend/` — Django project root (models, serializers, views, urls).
  - `frontend/` — React app (components, API clients, routes).

- **Project conventions & patterns** (explicit, discoverable):
  - Backend uses Django + Django REST Framework patterns: models -> serializers -> views -> urls.
  - Database: MongoDB is the target DB; project relies on `djongo` and `pymongo` packages. Use Django ORM constructs where possible — do not write direct Mongo shell scripts for schema/data.
  - Virtual environment: the project expects a venv at `octofit-tracker/backend/venv` (see workshop instructions) and a `backend/requirements.txt` listing pinned packages.
  - Never change directories when agent mode is running commands — when running shell commands in automation or in-code guidance, always reference absolute or repo-root-relative paths.

- **Developer workflows (concrete commands)**
  - Create venv (run from any location but reference full path):
    ```bash
    python3 -m venv octofit-tracker/backend/venv
    source octofit-tracker/backend/venv/bin/activate
    pip install -r octofit-tracker/backend/requirements.txt
    ```
  - Check MongoDB process before backend work:
    ```bash
    ps aux | grep mongod
    ```
  - Run Django dev server (listen publicly on Codespaces):
    ```bash
    python3 octofit-tracker/backend/manage.py runserver 0.0.0.0:8000
    ```
  - Run React dev server (typical):
    ```bash
    # from repo root or reference frontend path explicitly
    cd frontend && npm install && npm start
    ```
  - Ports to expose in Codespaces: only `8000` (backend) and `3000` (frontend) publicly; `27017` for MongoDB (private). Do not propose other ports.

- **Integration & testing notes**
  - Use the Django ORM for data migrations and models where possible — the workshop docs explicitly instruct to avoid direct MongoDB scripts.
  - The stack assumes Codespaces + Copilot agent mode; prefer small, incremental changes (add a model + serializer + view + test) and run the backend locally if possible.

- **Examples of concise agent prompts (use these exact forms)**
  - "Add a DRF serializer for `Activity` model in `backend/app/serializers.py` and wire it to a basic `ActivityViewSet` in `backend/app/views.py`. Update `backend/app/urls.py` to register the route `/api/activities/`. Keep changes minimal and include a unit test." 
  - "Create a React `ActivityLog` component at `frontend/src/components/ActivityLog.jsx` that POSTs to `/api/activities/`. Use fetch/axios and show a simple form with `type`, `duration`, and `date` fields."

- **What not to do**
  - Do not run or suggest global system changes (installing system packages) without asking — the workshop assumes Codespaces and controlled environment.
  - Do not invent files or directories as canonical; if a path doesn't exist, create it only after confirming minimal project structure and updating imports/exports consistently.

If anything in these instructions is unclear or you want me to add examples for a specific task (e.g., authentication, leaderboards, or team management), tell me which area and I will extend this file.
