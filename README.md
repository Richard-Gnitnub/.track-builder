# Lightweight-Track-Builder
This project is based on Templot5, thank you Martin Wynne.

---
##Project Charter

MVP Outline:
Framework: Flask.
Deployment: Docker Desktop for local testing and validation.
Track Design Standards: REA bullhead rail.
Core Features:
Admin Panel: Built using the Flask-Admin extension for managing track configurations and data.
Straight Track Generator: Generate a straight piece of track to the user’s specified length.
Modular Components:
Timbers and Chairs: Base components for track generation.
Rails: Placeholder logic, added manually post-MVP.
Planned Enhancements (Post-MVP):
Support for curves and turnouts.
3D model refinement for snap-fit designs.
Advanced track configuration options.
Development Plan:
Setup:
Use Flask for the application logic.
Integrate Flask-Admin for the admin panel.
Set up SQLite for configuration storage.
Docker Integration:
Create a Dockerfile and Docker Compose setup to containerize the application for testing on Docker Desktop.
Features:
User Input: Accept track length from users via a simple form or API endpoint.
Geometry Processing: Calculate the straight track layout based on user input.
STL Generation: Use CadQuery to generate 3D models of the track.
File Output: Provide a downloadable STL file for the user.
Testing:
Ensure the admin panel functions as expected for data management.
Validate the track generation logic and STL export.
Deployment (Local):
Deploy and test on Docker Desktop.
Ensure the application is stable and logic works before future iterations.

---
## Application Logic
```
flowchart TD
    A[User Input] -->|Track Parameters| B[Input Validation]
    B -->|Check for Errors| C{Valid Input?}
    C -->|Yes| D[Fetch Data from Database]
    C -->|No| E[Return Error Message]
    D -->|Configurations Loaded| F[Process Geometry]
    F -->|Generate Timbers and Chairs| G[Create 3D Model with CadQuery]
    G -->|Convert to STL| H[STL Export]
    H -->|Save File| I[Provide Download Link]
    I -->|User Access| J[Download STL File]

    subgraph Flask Workflow
        B --> C --> D --> F
    end

    subgraph External Logic
        G --> H
    end

    subgraph Final Output
        I --> J
    end
```
---
## Core App Directory Structure

```
project/
│
├── app/
│   ├── __init__.py    # Application initialization
│   ├── models.py      # Database models
│   ├── routes.py      # Application routes
│   ├── geometry.py    # Track geometry logic
│   ├── templates/     # HTML templates (if needed)
│   ├── static/        # Static files (if needed)
│
├── migrations/        # Database migration files
├── tests/             # Unit tests
├── Dockerfile         # Docker container configuration
├── docker-compose.yml # Docker Compose setup
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation

```
---
[## TODO List

### 1. Project Setup
- [ ] Set up the project directory structure for a Django application.
- [ ] Create a Python virtual environment (`venv` or `conda`) for isolated development.
- [ ] Install Django and essential dependencies:
  - `django`
  - `djangorestframework` (for future API support)
  - `cadquery` (for geometry generation)
  - `numpy`
- [ ] Initialise a Git repository and push to GitHub using the desktop app.
- [ ] Add a `.gitignore` file (e.g., ignore `__pycache__`, `.DS_Store`, virtual environments, STL files, etc.).
- [ ] Create a Django project and a core app for managing track components (e.g., `trackbuilder`).
- [ ] Configure static and media file handling for storing and serving STL files.
- [ ] Deploy to Digital Ocean

### 2. Core Functionality

#### a. Database Models
- [ ] Define models for chairs, rails, turnouts, and layouts in `models.py`:
  - Chairs: Include dimensions, types, and materials.
  - Rails: Define profiles, types, and tolerances.
  - Turnouts: Define angle, radius, and type.
  - Layouts: Store metadata and relationships between components.
- [ ] Set up relationships between layouts and their components (e.g., many-to-many relationships).
- [ ] Create migrations and populate the database with example data.

#### b. Geometry and STL Export
- [ ] Implement functions to generate geometry for chairs, rails, and turnouts.
- [ ] Integrate geometry generation with Django models.
- [ ] Implement STL export logic using `cadquery`.
- [ ] Add functionality to trigger STL exports from the web interface (e.g., a "Generate STL" button).
- [ ] Validate the integrity of exported STL files using an STL viewer (e.g., MeshLab).
- [ ] Implement geometry scaling based on user-defined input.

#### c. Web Interface
- [ ] Use Django’s admin interface to manage database entries (e.g., chairs, rails, turnouts).
- [ ] Create a user-friendly web interface for:
  - Viewing and managing track layouts.
  - Adding, editing, and deleting components (e.g., chairs, rails).
  - Configuring track settings (e.g., scale, tolerances).
  - Generating and downloading STL files.
- [ ] Ensure the interface is responsive and accessible for desktop and mobile users.

### 3. REST API (Optional for Future Use)
- [ ] Set up **Django REST Framework** (DRF) to expose APIs for:
  - Fetching chair, rail, and turnout data.
  - Submitting custom layouts for processing.
  - Downloading generated STL files programmatically.
- [ ] Create an example API endpoint for:
  - Submitting a layout: `POST /api/layout/`
  - Downloading an STL file: `GET /api/layout/<id>/stl/`
- [ ] Document the API for community use.

### 4. Hosting and Deployment
- [ ] Set up a PostgreSQL database for production (better scalability than SQLite).
- [ ] Use Django’s settings to handle environment-specific configurations (e.g., `.env` file with `django-environ`).
- [ ] Configure static and media file hosting for STL files and assets.
- [ ] Host the application using:
  - **Heroku** (simple deployment for MVP).
  - Or **AWS**, **DigitalOcean**, or **Vercel** for more control.
- [ ] Configure a production-ready web server (e.g., Gunicorn or uWSGI) with Django.
- [ ] Set up HTTPS using Let’s Encrypt or a similar service.
- [ ] Automate deployment using CI/CD workflows (e.g., GitHub Actions, GitLab CI).

### 5. Testing
- [ ] Write unit tests for models, views, and geometry generation functions.
- [ ] Test STL export functionality with various track layouts.
- [ ] Test the web interface for usability and bugs using browser-based testing tools (e.g., Selenium).
- [ ] Perform end-to-end testing to ensure the system works seamlessly.
- [ ] Validate edge cases, such as:
  - Overlapping or conflicting components in layouts.
  - Unusual geometry configurations (e.g., very tight radii).

### 6. Documentation
- [ ] Write a clear **Getting Started** guide for contributors.
- [ ] Document all database models and their relationships.
- [ ] Provide usage examples for the web interface.
- [ ] Create an FAQ or troubleshooting guide for common issues.
- [ ] Include deployment instructions for hosting the application.
- [ ] Write a **Contributing** guide to encourage community involvement.](https://chatgpt.com/g/g-p-67672c944cd0819184a850f0365fb16b-templot-simplified/c/676a5abb-58ec-8001-91e9-fdd0d6532b00#:~:text=updated%20deployment%20plan%3A-,TODO%20List,and%20deployment%20on%20a%20cloud%20platform%20(e.g.%2C%20AWS%20or%20DigitalOcean).,-This%20revised%20plan)
