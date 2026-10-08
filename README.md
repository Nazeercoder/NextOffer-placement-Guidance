# NextOffer – The Job Preparation Tracker

> A full-stack Java Spring Boot web application designed to help students and job seekers organize their job preparation activities, track DSA practice, manage interviews, and monitor their preparation progress.

## 📌 Project Overview

**NextOffer – The Job Preparation Tracker** is a full-stack web application developed using **Java 17 and Spring Boot**.

The main goal of NextOffer is to provide students and job seekers with a centralized platform where they can manage different activities related to job preparation.

Instead of maintaining DSA problems, interview schedules, and preparation progress separately, users can manage them through a single application.

The project was initially developed with core user functionality and was later improved with:

- A redesigned and more professional user interface
- A separate Admin module
- Separate Admin and General User login pages
- Role-based access control for Admin functionality
- Restricted access to Admin URLs for General Users
- Admin user-management capabilities
- Improved navigation and overall application structure

---

## 🎯 Objectives

The main objectives of NextOffer are:

- Provide a centralized platform for job preparation.
- Help users maintain and track DSA problems.
- Allow users to schedule and manage interviews.
- Provide a dashboard to monitor preparation progress.
- Provide separate access for Administrators and General Users.
- Prevent unauthorized users from accessing Admin functionality.
- Allow Administrators to manage registered users.
- Provide a clean and professional user interface.
- Demonstrate practical implementation of Spring Boot MVC, JPA, Hibernate, database integration, authentication, authorization, and CRUD operations.

---

# 🚀 Key Features

## 👤 General User Module

General users can register and access their own account through the General User login page.

### User Registration

Users can create an account by providing information such as:

- Full Name
- Email
- Password
- Phone Number

The registration information is stored in the database.

### User Login

Registered users can log in through the **General User Login** page.

The application validates the user's credentials before allowing access to the user dashboard.

### Dashboard

The dashboard provides an overview of the user's preparation activities.

It can display information such as:

- Total DSA Problems
- Solved Problems
- Remaining Problems
- Completion Percentage
- Interview-related information

---

# 🧠 DSA Problem Tracker

The DSA Problem Tracker allows users to maintain their coding-practice progress.

Users can:

- Add DSA problems
- View all problems
- Edit existing problems
- Delete problems
- Search for problems
- Filter problems based on difficulty
- Mark problems as solved or unsolved
- Track overall DSA completion progress

### Example

| Problem | Topic | Difficulty | Status |
|---|---|---|---|
| Two Sum | Arrays | Easy | Solved |
| Binary Search | Searching | Easy | Solved |
| Merge Sort | Sorting | Medium | Unsolved |

This module helps users keep track of the coding problems they have practiced during interview preparation.

---

# 📅 Interview Tracker

The Interview Tracker allows users to manage their interview preparation and schedules.

Users can:

- Add interviews
- View interviews
- Edit interview information
- Delete interviews
- Track interview status

Each interview can contain information such as:

- Company Name
- Job Role
- Interview Date
- Interview Status

### Example

| Company | Role | Interview Date | Status |
|---|---|---|---|
| ABC Technologies | Java Developer | 10-10-2026 | Scheduled |
| XYZ Solutions | Software Engineer | 15-10-2026 | Completed |

---

# 🛡️ Admin Module

A separate Admin module was introduced as part of the improved version of NextOffer.

The Admin module is separated from the General User module.

## 🔐 Separate Admin Login

Administrators have a dedicated login page.

```text
General User
    ↓
General User Login

Administrator
    ↓
Admin Login
```

General users do not use the Admin login page.

Similarly, Admin functionality is not exposed through the normal user interface.

---

## 🔒 Admin Authorization

The Admin module contains restricted functionality.

Only authorized administrators are allowed to access Admin pages and Admin activities.

For example, if a General User manually tries to access an Admin URL:

```text
http://localhost:8080/admin/...
```

the application verifies the user's authorization before allowing access.

Unauthorized users are restricted from accessing Admin functionality.

This prevents General Users from directly opening Admin pages simply by entering the URL.

### Access concept

```text
                    NextOffer
                       |
              -------------------
              |                 |
          General User        Admin
              |                 |
        User Dashboard      Admin Dashboard
              |                 |
        User Modules       User Management
```

---

# 👨‍💼 Admin User Management

Administrators have additional privileges that General Users do not have.

The Admin module allows administrators to:

- View registered users
- View the number of registered users
- View user information
- Delete users when required
- Manage user-related information

General users do not have access to these Admin operations.

This provides a clear separation between:

```text
General User Permissions
```

and

```text
Administrator Permissions
```

---

# 🎨 Improved User Interface

The original application interface was redesigned to provide a more professional and user-friendly experience.

UI improvements include:

- Improved page layouts
- Better navigation
- Responsive Bootstrap components
- Improved forms
- Improved tables
- Better spacing and alignment
- Consistent buttons and UI components
- Improved dashboard presentation
- Separate Admin and General User interfaces
- Improved login and registration pages

The goal of the redesign was to make NextOffer look and feel more like a practical real-world application rather than a basic academic CRUD project.

---

# 🏗️ Application Architecture

NextOffer follows a **layered Spring MVC architecture**.

```text
                        USER
                         |
                         ↓
                      Browser
                         |
                         ↓
                  DispatcherServlet
                         |
                         ↓
                  ┌──────────────┐
                  │  Controller  │
                  └──────────────┘
                         |
                         ↓
                  ┌──────────────┐
                  │   Service    │
                  └──────────────┘
                         |
                         ↓
                  ┌──────────────┐
                  │  Repository  │
                  └──────────────┘
                         |
                         ↓
                  ┌──────────────┐
                  │ JPA/Hibernate│
                  └──────────────┘
                         |
                         ↓
                  ┌──────────────┐
                  │ SQL Server   │
                  └──────────────┘
```

### Response Flow

```text
SQL Server
    ↓
Hibernate
    ↓
Repository
    ↓
Service
    ↓
Controller
    ↓
Model
    ↓
Thymeleaf
    ↓
HTML
    ↓
Browser
```

---

# 🧩 Layer Responsibilities

## Controller Layer

The Controller layer handles incoming HTTP requests and determines which operation needs to be performed.

Examples include:

- Login requests
- Registration requests
- DSA problem requests
- Interview requests
- Admin requests

Spring MVC annotations such as:

```java
@GetMapping
@PostMapping
@RequestParam
@PathVariable
@ModelAttribute
```

are used for request handling.

---

## Service Layer

The Service layer contains the application's business logic.

It acts as an intermediate layer between Controllers and Repositories.

For example:

```text
Controller
    ↓
Service
    ↓
Repository
```

This separation keeps business logic away from the Controller and improves maintainability.

---

## Repository Layer

The Repository layer is responsible for communicating with the database.

Spring Data JPA provides commonly used operations such as:

```text
save()
findAll()
findById()
deleteById()
count()
```

Custom repository methods can also be created for operations such as searching and filtering.

---

## Entity Layer

Entities represent the application's database tables.

Examples include entities for:

- Users
- DSA Problems
- Interviews

JPA annotations such as:

```java
@Entity
@Id
@GeneratedValue
@Column
@Table
```

are used to map Java classes to database tables.

---

# 🔄 Example Request Flow

### Adding a DSA Problem

When a user adds a DSA problem:

```text
User
  ↓
Add Problem Form
  ↓
POST Request
  ↓
DispatcherServlet
  ↓
DSAProblemController
  ↓
DSAProblemService
  ↓
DSAProblemRepository
  ↓
Spring Data JPA
  ↓
Hibernate
  ↓
SQL Server
```

After saving:

```text
SQL Server
  ↓
Hibernate
  ↓
Repository
  ↓
Service
  ↓
Controller
  ↓
Model
  ↓
Thymeleaf
  ↓
HTML
  ↓
Browser
```

---

# 🔐 Authentication & Authorization

NextOffer contains separate authentication flows for General Users and Administrators.

### General User

```text
Register
   ↓
General User Login
   ↓
Credential Validation
   ↓
User Session
   ↓
User Dashboard
```

### Administrator

```text
Admin Login
   ↓
Credential Validation
   ↓
Admin Authorization
   ↓
Admin Dashboard
   ↓
Admin-only Operations
```

Authorization checks ensure that General Users cannot access restricted Admin functionality through direct URLs.

> **Note:** The current implementation uses the application's authentication/session and authorization logic. Spring Security is not required to describe the current implementation unless it has been explicitly added to the project.

---

# 🗄️ Database

NextOffer uses **Microsoft SQL Server** as its relational database.

The database stores application data such as:

- User information
- DSA problems
- Interview information
- Authentication-related data

Spring Data JPA and Hibernate are used to communicate between the Java application and SQL Server.

### Database Flow

```text
Java Entity
    ↓
JPA
    ↓
Hibernate
    ↓
SQL Query
    ↓
Microsoft SQL Server
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Java 17 | Core programming language |
| Spring Boot | Backend framework |
| Spring MVC | Web MVC architecture |
| Spring Data JPA | Database access |
| Hibernate | ORM / JPA implementation |
| Microsoft SQL Server | Relational database |
| Thymeleaf | Server-side HTML rendering |
| Bootstrap | Responsive UI |
| Maven | Dependency and build management |
| Apache Tomcat | Embedded web server |

---

# 📁 Project Structure

The project follows a layered structure similar to:

```text
NextOffer/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── nazeer/
│   │   │           └── NextOffer/
│   │   │               │
│   │   │               ├── controller/
│   │   │               │   ├── HomeController.java
│   │   │               │   ├── UserController.java
│   │   │               │   ├── DSAProblemController.java
│   │   │               │   ├── InterviewController.java
│   │   │               │   └── AdminController.java
│   │   │               │
│   │   │               ├── service/
│   │   │               │   ├── UserService.java
│   │   │               │   ├── DSAProblemService.java
│   │   │               │   ├── InterviewService.java
│   │   │               │   └── AdminService.java
│   │   │               │
│   │   │               ├── repository/
│   │   │               │   ├── UserRepository.java
│   │   │               │   ├── DSAProblemRepository.java
│   │   │               │   └── InterviewRepository.java
│   │   │               │
│   │   │               ├── entity/
│   │   │               │   ├── User.java
│   │   │               │   ├── DSAProblem.java
│   │   │               │   └── Interview.java
│   │   │               │
│   │   │               └── NextOfferApplication.java
│   │   │
│   │   └── resources/
│   │       ├── templates/
│   │       │   ├── login.html
│   │       │   ├── register.html
│   │       │   ├── dashboard.html
│   │       │   ├── problems.html
│   │       │   ├── add-problem.html
│   │       │   ├── edit-problem.html
│   │       │   ├── interviews.html
│   │       │   ├── add-interview.html
│   │       │   ├── edit-interview.html
│   │       │   ├── admin-login.html
│   │       │   └── admin-dashboard.html
│   │       │
│   │       └── application.properties
│   │
│   └── test/
│
├── pom.xml
└── README.md
```

> The exact package and file names may vary depending on the final implementation.

---

# ⚙️ Installation & Setup

## Prerequisites

Before running NextOffer, install:

- Java 17 or later
- Maven
- Microsoft SQL Server
- SQL Server Management Studio (optional but recommended)
- Git
- IDE such as IntelliJ IDEA, Eclipse, or VS Code

---

## 1. Clone the Repository

```bash
git clone <your-github-repository-url>
```

Navigate into the project:

```bash
cd NextOffer
```

---

## 2. Configure SQL Server

Create a database in Microsoft SQL Server.

For example:

```sql
CREATE DATABASE NextOfferDB;
```

Update the database configuration inside:

```text
src/main/resources/application.properties
```

Example configuration:

```properties
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=NextOfferDB;encrypt=true;trustServerCertificate=true
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.SQLServerDialect
```

Use your own SQL Server configuration rather than copying the example credentials.

---

## 3. Run the Application

Using Maven:

```bash
mvn spring-boot:run
```

Or using the Maven wrapper on Windows:

```bash
.\mvnw.cmd spring-boot:run
```

Alternatively, run the main Spring Boot class:

```text
NextOfferApplication.java
```

---

## 4. Open the Application

Once the application starts successfully, open:

```text
http://localhost:8080
```

The available pages depend on the final controller mappings.

Typical application flow:

```text
Home
 ↓
General User Login / Registration
 ↓
Dashboard
 ↓
DSA Tracker / Interview Tracker
```

Administrator:

```text
Admin Login
 ↓
Admin Dashboard
 ↓
User Management
```

---

# 🔑 Access Control

The application separates General User and Administrator access.

### General Users

General users can access their own application modules, including:

- Dashboard
- DSA Tracker
- Interview Tracker
- CRUD operations within permitted modules

### Administrators

Administrators have additional privileges, including:

- Admin dashboard
- View registered users
- View user count
- Delete users
- Access Admin-only activities

### Restricted Access

General Users are restricted from accessing Admin-only pages and operations, including attempts to access protected Admin URLs directly.

---

# 📊 CRUD Operations

NextOffer demonstrates complete CRUD functionality.

### Create

Users can create:

- Accounts
- DSA problems
- Interviews

### Read

Users/Admins can view permitted information.

### Update

Users can modify their:

- DSA problem information
- Interview information

### Delete

Users can delete permitted records, while Administrators can delete registered users through Admin functionality.

---

# 🧪 Validation & Error Handling

The application includes validation for user input where required.

Examples include:

- Required fields
- Email validation
- Password length validation
- Phone number validation
- Database constraints such as unique email addresses

The application also handles common request and database-related errors through the application layers.

---

# 📚 Concepts Demonstrated

This project helped demonstrate practical knowledge of:

### Java

- Object-Oriented Programming
- Classes and Objects
- Encapsulation
- Collections
- Exception handling
- Java 17 features

### Spring Boot

- Dependency Injection
- Inversion of Control
- Spring Beans
- Spring MVC
- Controllers
- Services
- Repositories
- Request mappings
- Form handling

### JPA & Hibernate

- Entity mapping
- Primary keys
- Generated IDs
- CRUD operations
- ORM
- Repository abstraction
- Database interaction

### Web Development

- HTML
- Thymeleaf
- Bootstrap
- Forms
- HTTP GET/POST requests
- Server-side rendering
- Sessions
- Authentication
- Authorization

### Database

- Microsoft SQL Server
- Tables
- CRUD operations
- SQL queries
- Relational database concepts

---

# 💡 Challenges & Solutions

## 1. Understanding Layered Architecture

Initially, understanding how Controller, Service and Repository layers communicate was challenging.

This was addressed by separating each responsibility clearly:

```text
Controller → Request handling
Service → Business logic
Repository → Database operations
```

---

## 2. Thymeleaf Form Binding

Handling form data between HTML pages and Java objects required understanding:

```text
th:object
th:field
@ModelAttribute
```

This allowed form fields to bind directly to Java entity objects.

---

## 3. Database Integration

Connecting Spring Boot with Microsoft SQL Server and mapping Java entities to database tables provided practical experience with:

```text
JPA
Hibernate
Spring Data JPA
SQL Server
```

---

## 4. Authentication and Authorization

As the project evolved, simply having a login page was not sufficient for separating administrator functionality.

A separate Admin module was introduced with authorization checks so that:

- General Users have normal application access.
- Administrators have additional privileges.
- General Users cannot access Admin pages directly through URLs.

---

## 5. UI Improvement

The initial UI was functional but basic.

The application was redesigned using Bootstrap and improved layouts to provide a more professional and consistent user experience.

---

# 🔮 Future Enhancements

Possible future improvements include:

- Integration with Spring Security
- BCrypt password hashing
- More advanced role-based access control
- JWT-based authentication
- Forgot password functionality
- Email notifications for interviews
- Interview reminders
- DSA difficulty and topic analytics
- Progress charts
- Resume management
- Job application tracking
- REST API layer
- React-based frontend
- Cloud deployment
- Automated testing
- Docker containerization

---

# 📸 Screenshots

Add screenshots of your application here after uploading them to the repository.

Recommended screenshots:

1. Home / Welcome Page
2. General User Login
3. Registration Page
4. User Dashboard
5. DSA Problem Tracker
6. Add DSA Problem
7. Interview Tracker
8. Admin Login
9. Admin Dashboard
10. Admin User Management

Example:

```markdown
## Screenshots

### Home Page
![Home Page](screenshots/home.png)

### User Dashboard
![Dashboard](screenshots/dashboard.png)

### Admin Dashboard
![Admin Dashboard](screenshots/admin-dashboard.png)
```

---

# 🎓 Learning Outcome

Developing NextOffer provided practical experience in building a complete Java-based web application from the backend to the database and user interface.

The project helped strengthen understanding of:

- Java application development
- Spring Boot
- Spring MVC architecture
- Dependency Injection
- CRUD operations
- Spring Data JPA
- Hibernate ORM
- Microsoft SQL Server
- Thymeleaf
- Bootstrap
- Authentication
- Authorization
- Session management
- Layered application architecture
- Database-driven web applications

---

# 👨‍💻 Developer

**Nazeer K**

MCA Graduate | Java & Spring Boot Developer

### Skills

- Java
- Spring Boot
- Spring MVC
- Spring Data JPA
- Hibernate
- SQL
- Microsoft SQL Server
- Thymeleaf
- Bootstrap
- HTML/CSS
- Git/GitHub

---

# ⭐ Project Highlights

- Full-stack Java Spring Boot application
- Layered MVC architecture
- User registration and login
- Separate Admin authentication module
- Admin-only authorization
- User management
- DSA problem tracking
- Interview tracking
- CRUD functionality
- SQL Server database integration
- JPA/Hibernate ORM
- Thymeleaf server-side rendering
- Responsive Bootstrap UI
- Improved professional interface
- Role-based access concept

---

## 📄 License

This project was developed for educational, portfolio, and learning purposes.
