# VibeTravels

A web application that helps amateur tourists plan their trips effectively through AI-enhanced note organization.

![Project Status: Development](https://img.shields.io/badge/Project%20Status-Development-yellow)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-Latest-green)](https://www.djangoproject.com/)
[![HTMX](https://img.shields.io/badge/HTMX-1.17.2-purple)](https://htmx.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Table of Contents
- [Project Description](#project-description)
- [Tech Stack](#tech-stack)
- [Getting Started Locally](#getting-started-locally)
- [Available Scripts](#available-scripts)
- [Project Scope](#project-scope)
- [Project Status](#project-status)
- [License](#license)

## Project Description

VibeTravels is a web application designed to help amateur tourists plan their trips efficiently. The main functionality allows users to create notes about attractions and places they want to visit, then organize them into coherent trip plans. The application leverages artificial intelligence to analyze notes and generate suggestions that optimize users' travel experiences.

### Key Features

- Create and manage trips with personalized information
- Add notes with details about attractions, dates, and prices
- Organize notes in chronological order
- Generate AI-powered suggestions for plan improvements
- Export trip plans in simple formats (markdown/JSON)
- Calculate estimated trip budgets based on note entries

### Problem Statement

Amateur tourists often struggle with effective trip planning between locations, leading to wasted valuable time during their trips. They may lack sufficient knowledge about places they want to visit, resulting in inefficient travel plans.

Specific problems addressed by VibeTravels:
- Difficulty in determining the optimal order of visiting attractions
- Lack of awareness about opening hours, closure days, or other attraction restrictions
- Difficulty in estimating total trip costs
- Absence of tools for organizing and storing information about planned trips

## Tech Stack

### Frontend
- **Primary**: Django Templates + HTML/CSS
- **Interactive Elements**: HTMX
- **CSS Framework**: TailwindCSS
- **Benefits**:
  - Faster MVP development through backend integration
  - Minimal JavaScript requirements
  - Easy implementation of interactive elements with HTMX
  - Rapid UI prototyping with TailwindCSS

### Backend
- **Framework**: Python Django
- **Database**: PostgreSQL
- **Benefits**:
  - Built-in authorization and authentication mechanisms
  - ORM for easy database interaction
  - "Batteries included" - ready solutions for most MVP functionalities
  - Large community and documentation

### AI Integration
- **Service**: OpenRouter.ai
- **Features**:
  - Access to a wide range of models (OpenAI, Anthropic, Google, etc.)
  - Single API endpoint for all models
  - Caching system reducing costs for repetitive queries
  - Ability to set financial limits on API keys
  - OpenAI-compatible API format

### DevOps
- **Version Control**: GitHub
- **CI/CD**: GitHub Actions
- **Containerization**: Docker
- **Hosting**: DigitalOcean

## Getting Started Locally

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- PostgreSQL
- Git

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/vibetravel.git
   cd vibetravel
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   - Create a `.env` file in the project root based on `.env.example`
   - Fill in the required environment variables

   ```
   # Django settings
   DEBUG=True
   SECRET_KEY=your_secret_key_here
   ALLOWED_HOSTS=localhost,127.0.0.1

   # Database credentials
   DB_NAME=vibetravel
   DB_USER=postgres
   DB_PASSWORD=your_password
   DB_HOST=localhost
   DB_PORT=5432

   # Email settings
   EMAIL_HOST=smtp.example.com
   EMAIL_PORT=587
   EMAIL_USE_TLS=True
   EMAIL_HOST_USER=your_email@example.com
   EMAIL_HOST_PASSWORD=your_email_password

   # OpenRouter API
   OPENROUTER_API_KEY=your_openrouter_api_key

   # Security settings
   CSRF_TRUSTED_ORIGINS=https://localhost:8000
   SESSION_COOKIE_SECURE=True
   CSRF_COOKIE_SECURE=True
   ```

5. Set up the database:
   ```bash
   python manage.py migrate
   ```

6. Create a superuser:
   ```bash
   python manage.py createsuperuser
   ```

7. Run the development server:
   ```bash
   python manage.py runserver
   ```

8. Access the application at `http://localhost:8000`

### Docker Setup (Alternative)

1. Make sure Docker and Docker Compose are installed
2. Build and start the containers:
   ```bash
   docker-compose up -d
   ```
3. Access the application at `http://localhost:8000`

## Available Scripts

### Development
- `python manage.py runserver` - Start the development server
- `python manage.py createsuperuser` - Create an admin user
- `python manage.py makemigrations` - Create database migration files
- `python manage.py migrate` - Apply database migrations

### Testing & Linting
- `pre-commit run --all-files` - Run all pre-commit hooks
- `black .` - Format Python code
- `isort .` - Sort Python imports
- `flake8` - Run code linter
- `mypy .` - Run static type checking

### Database
- `python manage.py check_migrations` - Check migration conflicts
- `python manage.py check_constraints` - Validate database constraints

## Project Scope

### MVP Includes
- Simple user account system
- Creating, editing, viewing, and deleting trips
- Adding, editing, viewing, and deleting notes
- Basic AI integration (OpenRouter.ai) for generating suggestions
- Presentation of notes as a list/timeline
- Trip search by name and location
- Attraction cost summation
- Simple trip export format

### MVP Excludes
- Sharing trip plans between accounts
- Rich media handling and analysis
- Advanced time and logistics planning
- Various plan views (e.g., map view)
- User feedback collection mechanisms
- Advanced filtering and searching within note content

### Future Enhancements
- Mobile application version
- Advanced AI features
- Social sharing capabilities
- Integration with travel booking services
- Offline access to trip plans

## Project Status

VibeTravels is currently in the development phase. The core functionality is being built according to the MVP requirements outlined in the PRD.

### Current Focus
- Setting up the basic project structure
- Implementing user authentication
- Building the core trip and note management features

### Next Steps
- Implement AI integration for trip suggestions
- Design and implement the user interface
- Set up CI/CD pipeline with GitHub Actions

## License

This project is licensed under the MIT License - see the LICENSE file for details.

© 2023 VibeTravels Team 