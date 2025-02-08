# Phase 8: Notifications

## Objective
Implement a comprehensive notification system that alerts users about key events such as appointment confirmations, real-time chat messages, and system updates. The system should support both in-app notifications (using MantineUI) and email notifications, ensuring that users are promptly informed about system activity. All implementations must adhere to the project structure defined in `project-context.md` and follow our strict coding and documentation standards.

## Detailed Steps

### 1. Create the Notification Module in the Backend
- **Action:**
  - Generate a new Notification module using the NestJS CLI:
    ```bash
    cd backend
    nest generate module notification
    ```
- **Notes:**
  - This module will be responsible for handling all notification-related operations including triggers from various actions (e.g., appointment bookings, chat messages).

### 2. Notification System Setup
- **Action:**
  - Develop a Notification module with services for email (using Nodemailer) and in-app notifications.
- **Notes:**
  - Refer to [UserFlow.md](./UserFlow.md) for the detailed notification flow.

### 3. Implement Email Notification Service
- **Action:**
  - Install Nodemailer (or a similar email-sending package) to handle email notifications:
    ```bash
    npm install nodemailer
    ```
  - Create a dedicated service file (e.g., `notification-email.service.ts`) to encapsulate email notification logic.
- **Example Code Snippet:**
  ```typescript
  // backend/src/notification/notification-email.service.ts
  import { Injectable, InternalServerErrorException } from '@nestjs/common';
  import * as nodemailer from 'nodemailer';

  @Injectable()
  export class NotificationEmailService {
    private transporter;
    
    constructor() {
      this.transporter = nodemailer.createTransport({
        service: 'gmail', // Replace with your preferred email service
        auth: {
          user: process.env.EMAIL_USER,
          pass: process.env.EMAIL_PASS,
        },
      });
    }

    async sendNotificationEmail(to: string, subject: string, message: string): Promise<void> {
      const mailOptions = {
        from: process.env.EMAIL_USER,
        to,
        subject,
        text: message,
      };

      try {
        await this.transporter.sendMail(mailOptions);
      } catch (error) {
        throw new InternalServerErrorException('Failed to send email notification');
      }
    }
  }
  ```
- **Notes:**
  - Store email credentials securely in the `.env` file.
  - Document the email notification flow for future reference.

### 4. Develop In-App Notification Functionality
- **Action:**
  - In the Notification module, implement endpoints and services to handle in-app notifications.
  - Create a service (e.g., `notification.service.ts`) that stores and retrieves notification records.
- **Example Data Model:**
  - Update the Prisma schema to include a Notification model:
    ```prisma
    model Notification {
      id         Int      @id @default(autoincrement())
      userId     Int
      message    String
      read       Boolean  @default(false)
      createdAt  DateTime @default(now())

      user User @relation(fields: [userId], references: [id])
    }
    ```
  - Run the migration command:
    ```bash
    npx prisma migrate dev --name add_notification_model
    ```
- **Notes:**
  - Ensure endpoints are secured so that only authenticated users can retrieve their notifications.
  - Implement pagination and filtering if needed.

### 5. Integrate Notification Triggers Across Modules
- **Action:**
  - Tie notifications into critical user actions:
    - **Appointment Scheduling:** Trigger email and in-app notifications upon successful booking or cancellation.
    - **Chat Messages:** Optionally, use real-time triggers to notify users of new messages.
  - Update respective services (e.g., Appointment service, Chat service) to call the Notification module's methods.
- **Notes:**
  - Centralize notification logic to ensure consistency across the application.

### 6. Frontend Implementation for In-App Notifications
- **Action:**
  - In the Next.js frontend, build a notifications panel/page (e.g., `/notifications`), using MantineUI components for a polished look.
  - Use React Query to fetch and update in-app notifications.
- **Example Instructions:**
  - Create a new file at `frontend/src/pages/notifications.tsx`.
  - Implement components to display a list of notifications, mark them as read, and auto-refresh the list for real-time updates.
- **Notes:**
  - Ensure clear UI feedback and error handling for a seamless user experience.

### 7. Testing and Verification
- **Action:**
  - Write unit tests for the Notification services (both email and in-app) using Jest.
  - Develop integration tests to validate the complete notification workflow from triggering events to user delivery.
- **Notes:**
  - Document expected scenarios and edge cases, especially for error handling in email delivery.

### 8. Commit and Documentation
- **Action:**
  - Commit all changes with a clear and descriptive commit message:
    ```bash
    git add .
    git commit -m "Phase 8: Implement comprehensive notification system with email and in-app notifications"
    ```
  - Update API documentation to include notification endpoints and flows.
  - Link the notification system details to the `project-context.md` for overall architectural context.
- **Notes:**
  - Ensure that documentation and commit messages remain clear to support ongoing maintenance.

## Expected Outcome
- A fully functional Notification module in the backend supporting both email and in-app notifications.
- End-to-end integration, where actions from other modules trigger relevant notifications.
- A responsive frontend interface for users to view and manage their in-app notifications.
- Comprehensive tests and documentation ensuring the reliability and scalability of the notification system.

---

## References
- [NestJS Mailer Module](https://github.com/nest-modules/mailer)
- [Twilio Node.js SDK](https://www.twilio.com/docs/libraries/node)
- [Handlebars Templates](https://handlebarsjs.com/)
- [Prisma Relations](https://www.prisma.io/docs/concepts/components/prisma-schema/relations) 