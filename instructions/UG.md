# User Guide (UG): Phased Project Restart Overview

## Introduction
This guide summarizes the comprehensive phased instructions for the project restart. It provides an overview of each phase (P1–P14) to help you quickly reference the key objectives and major actions for each step of the restart process.

## Phase Overview

1. **Phase 1: Project Setup**  
   **Objective:** Restart from scratch ensuring a clean architecture that separates Clients and Lawyers from the beginning.  
   **Key Actions:**  
   - Initialize the Git repository and set branch conventions.
   - Establish the minimal folder/file structure based on `project-context.md`.
   - Set up the initial README, `.gitignore`, and environment configurations.
   - Bootstrap backend (NestJS) and frontend (Next.js) projects using TypeScript.

2. **Phase 2: Backend Architecture**  
   **Objective:** Build a robust backend using NestJS, Prisma ORM with PostgreSQL, and cloud storage integration.  
   **Key Actions:**  
   - Initialize the NestJS project using the CLI.
   - Set up Prisma with PostgreSQL and create initial models (Users, Roles).
   - Configure essential environment variables and integrate cloud storage.
   - Organize backend modules (Auth, User, Document, etc.).

3. **Phase 3: Authentication & Authorization**  
   **Objective:** Implement secure authentication using JWT with OAuth integrations (Google, future support for LinkedIn).  
   **Key Actions:**  
   - Create an Auth module and set up the JWT strategy.
   - Implement OAuth integrations.
   - Enforce role-based access control using custom decorators and guards.

4. **Phase 4: User Management**  
   **Objective:** Develop comprehensive user management featuring distinct profiles for Clients and Lawyers.  
   **Key Actions:**  
   - Update the Prisma schema with user roles and associated fields.
   - Create endpoints using DTOs for validated user operations.
   - Integrate administrative functions for user account management.

5. **Phase 5: Appointment Scheduling**  
   **Objective:** Develop an appointment scheduling system for Clients to book consultations with Lawyers.  
   **Key Actions:**  
   - Create a dedicated Appointment module and define appointment models.
   - Implement logic for slot selection, conflict resolution, and email notifications upon booking.
   - Build frontend interfaces for scheduling with proper validations.

6. **Phase 6: Real-Time Communication**  
   **Objective:** Enable live chat functionality between Clients and Lawyers using Socket.io.  
   **Key Actions:**  
   - Create a Chat module with a Socket.io gateway.
   - Integrate authentication into the real-time communication layer.
   - Develop a responsive chat interface in the frontend.

7. **Phase 7: Document Management**  
   **Objective:** Implement a secure document management system for uploading, viewing, and downloading legal documents.  
   **Key Actions:**  
   - Create a Document module and update the Prisma schema with a Document model.
   - Integrate with cloud storage for efficient file handling.
   - Build RESTful endpoints and corresponding frontend pages for document operations.

8. **Phase 8: Notifications**  
   **Objective:** Set up a comprehensive notification system to alert users about appointment updates, chat messages, and system events.  
   **Key Actions:**  
   - Develop a Notification module with services for email (using Nodemailer) and in-app notifications.
   - Update the Prisma schema with a Notification model.
   - Create frontend components to display and manage notifications.

9. **Phase 9: Payments Integration**  
   **Objective:** Integrate a secure payment gateway (Stripe) to manage financial transactions between Clients and Lawyers.  
   **Key Actions:**  
   - Create a Payment module and implement services to create payment intents and handle webhooks.
   - Secure endpoints with proper authentication and authorization checks.
   - Develop frontend pages to integrate and process payments using Stripe.

10. **Phase 10: Testing & Documentation**  
    **Objective:** Establish exhaustive testing workflows and comprehensive documentation practices across the project.  
    **Key Actions:**  
    - Configure Jest for unit and integration testing on both backend and frontend.
    - Set up Cypress for end-to-end testing.
    - Update API documentation (e.g., Swagger) and maintain project documents (README, project-context).
    - Implement CI/CD pipelines to enforce testing standards on every commit.

11. **Phase 11: Deployment**  
    **Objective:** Deploy the application in a secure, scalable production environment with automated CI/CD pipelines and robust monitoring.  
    **Key Actions:**  
    - Prepare production configuration files and build production bundles.
    - Configure CI/CD workflows (e.g., via GitHub Actions) to automate builds, tests, and deployments.
    - Integrate monitoring and logging tools.
    - Conduct production readiness testing (load testing, end-to-end testing) before release.

12. **Phase 12: Frontend Setup**  
    **Objective:** Establish the Next.js frontend project using TypeScript along with MantineUI, Tailwind CSS, React Query, and PWA support.  
    **Key Actions:**  
    - Initialize the Next.js project and install required dependencies.
    - Set up global styling with Tailwind CSS.
    - Configure providers for MantineUI and React Query in the custom App component.
    - Enable PWA functionality through appropriate manifest and service worker configurations.

13. **Phase 13: Frontend Development**  
    **Objective:** Develop core frontend features such as authentication pages, a responsive dashboard, and integration with backend services.  
    **Key Actions:**  
    - Create login and registration pages with form validations.
    - Build a role-based dashboard and navigation system.
    - Develop pages for appointment scheduling, chat, document management, and notifications.
    - Manage state and API calls using React Query, ensuring error handling and loading states.
    - Write component and integration tests for key features.

14. **Phase 14: PWA Configuration**  
    **Objective:** Finalize and enhance the Progressive Web App capabilities to provide offline support and a native app–like experience on mobile devices.  
    **Key Actions:**  
    - Configure the service worker with Next PWA for caching essential assets.
    - Verify the manifest and ensure high-quality icons are included.
    - Optimize performance through lazy loading and efficient utilization of Next.js features.
    - Conduct offline testing and performance audits with tools like Lighthouse.
    - Update documentation to reflect these configurations and optimizations.

## User Flow
For a detailed view of the user journey and interaction flow, please refer to the [UserFlow.md](./UserFlow.md) file. Key highlights include:
- **Entry Points & Landing Pages:** The client-focused landing page with hero section, location selection, and specialized lawyer cards.
- **Lawyer-Side Flow:** Dedicated pages for lawyer registration and dashboard access.
- **Client Discovery and Interaction:** Detailed lawyer list pages, authenticated lawyer details, and booking & payment processes.
- **Auxiliary Features:** The "Help me Find the Right Lawyer" wizard and enquiry modal to assist with refined searches.
- **Authentication Checkpoints:** Users must sign in to view detailed lawyer information, secure bookings, and access communication tools.

## Final Notes
Each phase is meticulously documented to ensure clarity, maintainability, and ease of onboarding for junior or AI-assisted developers. The overall goal is to build a scalable, secure, and performant legal consultation platform featuring distinct capabilities for Clients and Lawyers, supported by robust backend services and a sophisticated frontend experience.

If you have any further questions or need additional details on any phase or feature, please refer to the respective guides in this repository.

_End of User Guide._ 