# 🏠 RentFix

> A simple maintenance request and issue-tracking system for tenants, landlords, and property managers.

RentFix helps property managers move maintenance requests away from scattered WhatsApp messages and phone calls into one organised platform.

Tenants can report issues, track their requests, and receive updates, while landlords or property managers can manage, assign, and resolve maintenance requests from a central dashboard.

---

## 🚨 The Problem

Maintenance issues in rental properties are often reported through:

* WhatsApp messages
* Phone calls
* Verbal communication
* Paper records

This makes it easy for requests to be forgotten, delayed, or difficult to track.

A tenant may report a leaking tap today and have no clear way of knowing whether the issue has been assigned, worked on, or resolved.

### RentFix solves this by providing a centralised maintenance workflow.

```text
Tenant reports issue
        ↓
Maintenance request created
        ↓
Manager receives notification
        ↓
Request assigned to technician
        ↓
Technician works on issue
        ↓
Request marked as resolved
        ↓
Tenant receives update
```

---

## ✨ Features

### 👤 Tenant

* Register and log in
* Submit maintenance requests
* Select maintenance category
* Add issue description
* Upload an optional image
* View submitted requests
* Track request status
* View resolution notes

### 🏢 Property Manager

* Dashboard overview
* View all maintenance requests
* Filter requests by status/category
* Assign requests to technicians
* Update request status
* Add resolution notes
* Monitor outstanding issues

### ⚙️ Automation

RentFix integrates with **n8n** to automate repetitive communication.

Example:

```text
New maintenance request
        ↓
Laravel API
        ↓
n8n Webhook
        ↓
Notify property manager
```

Another automation:

```text
Request remains unresolved
for 24 hours
        ↓
n8n scheduled workflow
        ↓
Send reminder
```

---

## 🔄 Request Status Workflow

```text
PENDING
   ↓
ASSIGNED
   ↓
IN PROGRESS
   ↓
RESOLVED
```

Managers can update the status as the issue progresses.

---

## 🛠️ Tech Stack

### Backend

* Laravel
* PHP
* MySQL
* Laravel Sanctum / Authentication
* REST API

### Frontend

* Blade / Laravel frontend

or, if using a separate frontend:

* Next.js
* TypeScript
* Tailwind CSS

### Automation

* n8n
* Webhooks
* Scheduled workflows
* Email/notification automation

### Development

* Git
* GitHub
* Postman

---

## 🗄️ Core Database Structure

Main entities include:

```text
users
  │
  ├── tenants
  │
  ├── managers
  │
  └── technicians

properties
  │
  └── maintenance_requests
          │
          ├── category
          ├── assigned technician
          └── status
```

### Maintenance Request

Example fields:

```text
id
user_id
property_id
category_id
assigned_to
title
description
image
status
priority
resolution_notes
created_at
updated_at
```

---

## 🔌 API Example

Create a maintenance request:

```http
POST /api/maintenance-requests
```

Example request:

```json
{
    "title": "Leaking kitchen tap",
    "description": "The kitchen tap has been leaking continuously.",
    "category_id": 2,
    "priority": "medium"
}
```

Example response:

```json
{
    "message": "Maintenance request created successfully",
    "request": {
        "id": 15,
        "status": "pending"
    }
}
```

---

## 🤖 n8n Integration

RentFix exposes webhooks that can trigger n8n workflows.

### Example Workflow

```text
Laravel
   │
   │ Webhook
   ↓
 n8n
   │
   ├── Send Email
   │
   ├── Send Notification
   │
   └── Log Event
```

This makes the system extensible without putting every automation directly inside Laravel.

Future workflows could include:

* Automatic tenant notifications
* Overdue maintenance reminders
* Weekly maintenance reports
* Technician notifications
* Property manager summaries

---

## 🔐 Security

The application is designed with basic application security in mind:

* Authentication
* Authorisation
* Request validation
* Protected API routes
* CSRF protection
* Secure password hashing
* Role-based access control

---

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/rentfix.git

cd rentfix
```

### 2. Install dependencies

```bash
composer install
```

### 3. Create environment file

```bash
cp .env.example .env
```

### 4. Generate application key

```bash
php artisan key:generate
```

### 5. Configure database

Update `.env`:

```env
DB_DATABASE=rentfix
DB_USERNAME=root
DB_PASSWORD=
```

Create the database in MySQL:

```sql
CREATE DATABASE rentfix;
```

### 6. Run migrations

```bash
php artisan migrate
```

### 7. Start the application

```bash
php artisan serve
```

The application will be available at:

```text
http://127.0.0.1:8000
```

---

## 🔧 n8n Setup

Start your n8n instance and create a webhook workflow.

Example:

```text
Webhook
   ↓
Check Request
   ↓
Send Notification
```

Configure Laravel to send the maintenance request event to the n8n webhook.

Example `.env`:

```env
N8N_WEBHOOK_URL=your-webhook-url
```

---

## 📁 Project Structure

```text
app/
├── Http/
│   ├── Controllers/
│   └── Requests/
│
├── Models/
│
├── Notifications/
│
└── Services/

database/
├── migrations/
└── seeders/

routes/
├── api.php
└── web.php

resources/
├── views/
└── css/

tests/
├── Feature/
└── Unit/
```

---

## 🧪 Testing

Run the test suite with:

```bash
php artisan test
```

Example areas covered:

* User authentication
* Maintenance request creation
* Request validation
* Status updates
* Request assignment
* Authorisation

---

## 🗺️ Roadmap

### MVP

* [x] Authentication
* [ ] Tenant dashboard
* [ ] Maintenance request creation
* [ ] Request tracking
* [ ] Manager dashboard
* [ ] Request assignment
* [ ] Status management
* [ ] Basic notifications
* [ ] n8n webhook integration

### Future

* [ ] Multiple properties
* [ ] Technician accounts
* [ ] Email notifications
* [ ] WhatsApp notifications
* [ ] Maintenance analytics
* [ ] Recurring maintenance
* [ ] Property-specific dashboards
* [ ] Mobile application
* [ ] AI-powered issue categorisation

---

## 💡 Future AI Integration

A future version could use AI to automatically categorise maintenance requests.

For example:

```text
Tenant:
"My bathroom pipe is leaking badly."

             ↓

          AI Model

             ↓

Category: Plumbing
Priority: High
```

This could then trigger an n8n workflow to notify the appropriate technician automatically.

---

## 🎯 Project Goal

RentFix is designed as a practical demonstration of how a relatively simple Laravel application can solve a real-world operational problem while integrating modern automation tools.

The project focuses on:

* Backend development
* REST APIs
* Database design
* Authentication and authorisation
* Workflow management
* Automation
* System integration
* Software architecture

---

## 👨‍💻 Author

**Harrison Opondo**

Built with Laravel, MySQL, and n8n.

---

## 📄 License

This project is open-source and available under the MIT License.
