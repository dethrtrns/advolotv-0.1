# Advolot Project Context

## Overview
Advolot is an online legal consultation platform designed to connect clients with qualified lawyers. The platform facilitates scheduling consultations, managing appointments, and enabling secure communication between clients and legal professionals. Key features include:

- **User Roles:** Separate roles for Clients and Lawyers, each with distinct profiles and functionalities.
- **Authentication:** Secure authentication system using JWT and Google OAuth.
- **Profile Management:** Users can manage their profiles, with Lawyers having additional fields like specialties and hourly rates.
- **Appointment Scheduling:** Clients can schedule consultations with lawyers, featuring real-time availability checks and conflict resolution.
- **Real-time Communication:** Integrated chat functionality with support for text, audio, and video interactions via Twilio.
- **Document Management:** Secure document upload and sharing capabilities using Google Cloud Storage.
- **Notifications:** Email and SMS notifications for appointment confirmations and reminders.
- **Payments:** Integration with Stripe for handling transactional payments.

For more details on how the user navigations and interactions are structured, please refer to the [UserFlow.md](./UserFlow.md) document.

## Security & Architecture
- **Security:** Implements best practices including CORS restrictions, rate limiting, CSRF protection, SSL/TLS, and request validation.
- **Tech Stack:**
  - **Frontend:**
    - Next.js (App Router)
    - MantineUI + Tailwind CSS
    - TypeScript
    - WebRTC (Twilio) for real-time features
  - **Backend:**
    - NestJS
    - PostgreSQL with Prisma ORM
    - JWT Authentication
    - WebSocket for real-time communication

## Current Status
- **Completed:**
  - User roles implementation (CLIENT/Lawyer)
  - User profile management with lawyer-specific fields
  - Lawyer search functionality with filtering
  - Responsive dashboard layout
  - Basic navigation and user menu
  - JWT-based authentication setup
- **Pending:**
  - Complete LinkedIn OAuth verification
  - Enhance error handling in authentication guards
  - Implement password reset functionality
  - Add profile image upload and validation
  - Implement appointment scheduling with conflict checks
  - Develop real-time chat functionality
  - Set up email and SMS notifications
  - Integrate payment gateway and document management
  - Establish comprehensive testing strategies

## Core Architecture & Technology Stack

### Frontend
- **Framework:** Next.js (App Router)
- **UI Libraries:** MantineUI (core, hooks, form, etc.) and Tailwind CSS
- **Language:** TypeScript
- **Real-time Features:** WebRTC (Twilio)
- **State Management:** React Query with Context API
- **Additional Packages:**
  - `@mantine/core` for UI components
  - `@mantine/hooks` for reusable hooks
  - `@mantine/form` for form management
  - `react-query` for data fetching and caching
  - `next-pwa` for Progressive Web App (PWA) capabilities

### Backend
- **Framework:** NestJS
- **Database:** PostgreSQL with Prisma ORM
- **Authentication:** JWT and Google OAuth
- **Real-time Communication:** WebSockets (Socket.io)
- **Payments:** Stripe API
- **Storage:** Google Cloud Storage

## Folder/File Structure 

advolot/
├── frontend/ # Next.js frontend
│ ├── src/
│ │ ├── app/
│ │ │ ├── auth/
│ │ │ ├── dashboard/
│ │ │ ├── profile/
│ │ │ ├── appointments/
│ │ │ ├── chat/
│ │ │ └── ...
│ │ ├── components/
│ │ │ ├── layout/
│ │ │ ├── ui/
│ │ │ ├── forms/
│ │ │ └── ...
│ │ ├── hooks/
│ │ ├── context/
│ │ ├── styles/
│ │ │ ├── globals.css
│ │ │ ├── tailwind.config.js
│ │ │ └── ...
│ │ ├── utils/
│ │ ├── pages/
│ │ └── ...
│ ├── public/
│ ├── .env.local
│ ├── next.config.js
│ ├── tailwind.config.js
│ ├── postcss.config.js
│ └── ...
├── backend/ # NestJS backend
│ ├── src/
│ │ ├── modules/
│ │ │ ├── auth/
│ │ │ ├── user/
│ │ │ ├── appointment/
│ │ │ ├── chat/
│ │ │ ├── document/
│ │ │ ├── notification/
│ │ │ ├── payment/
│ │ │ ├── prisma/
│ │ │ ├── storage/
│ │ │ └── ...
│ │ ├── common/
│ │ │ ├── guards/
│ │ │ ├── interceptors/
│ │ │ ├── decorators/
│ │ │ └── ...
│ │ ├── config/
│ │ ├── main.ts
│ │ └── ...
│ ├── prisma/
│ │ └── schema.prisma
│ ├── .env
│ └── ...
├── shared/ # Shared code and utilities
├── docs/ # Documentation
│ ├── authentication.md
│ ├── user-management.md
│ ├── appointment-scheduling.md
│ ├── real-time-communication.md
│ ├── document-management.md
│ ├── payments-integration.md
│ ├── notifications.md
│ ├── testing.md
│ ├── deployment.md
│ └── ...
├── restart-project-with-o1/ # Restart project files
│ ├── roadmap.md
│ ├── phase1-instructions.md
│ ├── phase2-instructions.md
│ ├── project-context.md
│ ├── code-editor-rules.md
│ └── ...
├── .gitignore
├── LICENSE
└── README.md

## Codebase Mapping (Data/Code Flow)

1. **User Authentication:**
   - Users register and log in via `AuthController`.
   - `AuthService` handles JWT token generation and validation.
   - Protected routes are guarded by `JwtAuthGuard` and `RolesGuard`.

2. **User Management:**
   - `UserController` manages user profiles.
   - `UserService` interacts with Prisma to handle database operations.
   - Separate data models for Clients and Lawyers ensure role-specific functionalities.

3. **Appointment Scheduling:**
   - `AppointmentController` exposes endpoints to create and manage appointments.
   - `AppointmentService` ensures real-time availability checks and conflict resolution.
   - Integrates with `NotificationService` to send confirmations and reminders.

4. **Real-time Communication:**
   - `ChatGateway` manages WebSocket connections for real-time chat.
   - `ChatService` handles message persistence and retrieval.
   - Twilio integration enables audio/video communication.

5. **Document Management:**
   - `DocumentController` and `DocumentService` handle file uploads and retrievals.
   - Files are securely stored in Google Cloud Storage with restricted access.

6. **Notifications:**
   - `NotificationService` sends emails and SMS messages using MailerModule and Twilio.
   - Integrated across various modules to notify users of important events.

7. **Payments:**
   - `PaymentController` and `PaymentService` manage Stripe checkout sessions and handle webhooks.
   - Securely process payments related to appointments.

## Interdependencies & Integration Points
- **Feature Dependencies:**  
  Appointment scheduling, payment gateway, and document management are closely interlinked. Changes in one may affect the others.
- **External Integrations:**  
  - **OAuth Services:** Google (active) and LinkedIn (pending).
  - **Cloud Storage:** Google Cloud Storage or AWS S3 for document handling.
  - **Payment Services:** Planned integration with Stripe.
  - **Real-Time Communication:** Planned use of Twilio for WebRTC-based features.

## Roadmap & Future Enhancements
For a detailed step-by-step plan on development phases and feature enhancements, please refer to the [Project Roadmap](roadmap.md). Future enhancements include:
- Mobile app development.
- AI-powered lawyer matching.
- Legal document templates.
- Multi-language support.

## Team Communication & Support
For any questions or clarifications regarding the project context, please reach out via the designated communication channel:
- **Team Channel:** [Insert Channel Name/Link]
- **Contact:** [Insert Contact Information]

---

This document is a living reference that should be updated as project requirements, architecture, or status change. It is intended to provide a clear overview for new team members and AI assistants working with the codebase.
