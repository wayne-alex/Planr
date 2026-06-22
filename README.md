# Project Management System

A comprehensive Django-based project management system with advanced permission controls, organization management, and task tracking capabilities.

## Features

### Core Functionality
- **User Authentication**: Secure authentication system with email-based login
- **Role-Based Access Control**: Multiple user roles (Super Admin, Admin, Project Manager, Member, Viewer)
- **Organization Management**: Create and manage organizations with subscription packages
- **Project Management**: Create projects within organizations with customizable permissions
- **Task Management**: Create, assign, and track tasks with statuses, priorities, and deadlines
- **Timeline & Milestones**: Visual project timelines with milestone tracking
- **Collaboration**: Task comments and status history tracking
- **Custom Permission System**: Granular permission controls using octal-based permissions (read/write/execute)

### Advanced Features
- **Subscription Packages**: Different tiers (Free, Pro, Enterprise) with varying limits
- **Flexible Permission System**: 
  - Owner always retains execute permissions
  - Group and others permissions configurable
  - Per-member execute overrides
  - Task-level permission inheritance/override
- **Audit Logging**: Track organizational changes and user actions
- **Subscription Management**: Storage limits, member limits, project limits per package
- **Rich Data Models**: UUID-based primary keys, comprehensive model relationships

## Technology Stack

- **Backend**: Django 6.0.5
- **Database**: SQLite3 (development), configurable for production
- **Authentication**: Custom user model with email verification
- **Frontend**: Django templates with Bootstrap/CSS
- **Other**: 
  - UUID for primary keys
  - GenericForeignKey for audit logging
  - ContentType framework

## Project Structure

```
ProjectManagementSystem/
├── authentication/           # User authentication and management
│   ├── models.py            # Custom User model with roles
│   ├── views.py             # Authentication views (login, register, etc.)
│   ├── urls.py              # Authentication URL patterns
│   └── templates/           # HTML templates for auth pages
├── organization/             # Core project management functionality
│   ├── models.py            # Organizations, Projects, Tasks, Permissions, etc.
│   ├── views.py             # Business logic views
│   ├── urls.py              # Organization URL patterns
│   └── templates/           # HTML templates for project management
├── planr/                    # Django project settings
│   ├── settings.py          # Django configuration
│   ├── urls.py              # Root URL configuration
│   └── wsgi.py              # WSGI deployment
├── manage.py                 # Django management script
├── db.sqlite3               # SQLite database
└── README.md                # This file
```

## Installation & Setup

### Prerequisites
- Python 3.8+
- pip (Python package manager)
- Virtual environment tool (venv, virtualenv, etc.)

### Step-by-Step Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/wayne-alex/Project-Managment-System.git
   cd ProjectManagementSystem
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   *(If requirements.txt is missing, install Django manually:)*
   ```bash
   pip install django
   ```

4. **Apply database migrations**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create a superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

6. **Run the development server**
   ```bash
   python manage.py runserver
   ```

7. **Access the application**
   - Open your browser and navigate to `http://127.0.0.1:8000/`
   - Admin panel: `http://127.0.0.1:8000/admin/`

## Usage

### Initial Setup
1. Register a new account or log in with superuser credentials
2. Create an organization (choose a subscription package)
3. Invite team members to your organization
4. Create projects within your organization
5. Add tasks to projects and assign them to team members

### Permission System
The system uses a custom octal-based permission model:
- **Read (2)**: View task/project details
- **Write (4)**: Change task statuses
- **Execute (1)**: Modify project structure (add members, change timeline, etc.)

Permissions are represented as three-digit octal numbers:
- First digit: Owner permissions
- Second digit: Group (project members) permissions  
- Third digit: Others (organization members not in project) permissions

Example: `762` means:
- Owner: 7 (read+write+execute = full access)
- Group: 6 (read+write = can view and change task status)
- Others: 2 (read-only = can only view)

### Subscription Packages
The system includes predefined subscription packages:
- **Free**: Limited members, projects, storage
- **Pro**: Increased limits, additional features
- **Enterprise**: Unlimited limits, premium features

## API Endpoints

While primarily a server-rendered Django application, the system includes RESTful endpoints for:
- Authentication (login, logout, register, password reset)
- Organization CRUD operations
- Project management (creation, updates, permissions)
- Task management (CRUD, status updates)
- Timeline and milestone management
- Commenting and activity feeds

Refer to the `urls.py` files in each app for detailed endpoint specifications.

## Models Overview

### Authentication App
- **User**: Extended Django User with email verification, roles, and status tracking
- **RefreshTokenRecord**: JWT refresh token management
- **PasswordResetToken**: Secure password reset functionality
- **EmailVerificationToken**: Email verification for new accounts

### Organization App
- **SubscriptionPackage**: Defines limits and features for organization tiers
- **Organization**: Container for projects with subscription and settings
- **OrganizationMember**: Links users to organizations with roles
- **Project**: Main work container with custom permission system
- **ProjectMember**: Explicit project membership with permission overrides
- **Task**: Work items with assignees, status, priority, and permissions
- **ProjectTimeline**: Milestones and phases for project planning
- **TaskComment**: Discussion thread on tasks
- **TaskStatusHistory**: Audit trail of task status changes
- **AuditLog**: Organization-wide activity logging

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure your code follows Django best practices and includes appropriate tests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Django Framework for the robust backend foundation
- All contributors who have helped shape this project
- Open-source libraries and tools used throughout the system

---

*Last updated: June 2026*
