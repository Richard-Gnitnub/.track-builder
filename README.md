# Lightweight-Track-Builder
This project is based on Templot5. 
---
## 3D Generator Logic
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

```plaintext
core/
├── __init__.py
├── admin.py
├── apps.py
├── migrations/
│   └── __init__.py
├── models.py          # Data models for storing core parameters
├── tests.py
├── views.py           # For handling API views or rendering templates
├── urls.py            # For defining app-specific routes
├── logic/             # Core logic directory
│   ├── __init__.py
│   ├── geometry.py    # Placeholder for track geometry calculations
│   ├── exporter.py    # Placeholder for CadQuery STL generation
│   └── utilities.py   # Placeholder for shared utility functionss
```

## TODO List

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
- [ ] Write a **Contributing** guide to encourage community involvement.
