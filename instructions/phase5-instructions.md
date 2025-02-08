# Phase 5: Appointment Scheduling

## Objective
Develop a comprehensive appointment scheduling system that enables Clients to book legal consultations with Lawyers. This phase includes setting up the backend modules, implementing scheduling logic with conflict resolution, and creating frontend interfaces to handle bookings. All steps adhere strictly to the project structure defined in `project-context.md`.

## Detailed Steps

### 1. Create the Appointment Module in the Backend
- **Action:**
  - Generate a new module for appointment scheduling using the NestJS CLI.
  - Use the following command to create the module:
    ```bash
    cd backend
    nest generate module appointment
    ```
- **Notes:**
  - This module will encapsulate all appointment-related logic, including scheduling, conflict management, and notifications.

### 2. Define the Appointment Data Model
- **Action:**
  - Update the Prisma schema (`prisma/schema.prisma`) with a new model for appointments.
  - Ensure the model includes key fields such as date, time, duration, Client ID, Lawyer ID, and status.
- **Example Schema:**
  ```prisma
  model Appointment {
    id          Int      @id @default(autoincrement())
    date        DateTime
    duration    Int      // Duration in minutes
    clientId    Int
    lawyerId    Int
    status      String   // e.g., 'scheduled', 'completed', 'cancelled'
    createdAt   DateTime @default(now())
    updatedAt   DateTime @updatedAt

    // Relations
    client User @relation("ClientAppointments", fields: [clientId], references: [id])
    lawyer User @relation("LawyerAppointments", fields: [lawyerId], references: [id])
  }
  ```
- **Next Steps:**
  - Run the Prisma migration command:
    ```bash
    npx prisma migrate dev --name add_appointment_model
    ```

### 3. Implement Conflict Checking and Scheduling Logic
- **Action:**
  - In the Appointment service (e.g., `appointment.service.ts`), implement logic to:
    - Check for scheduling conflicts based on the lawyer's availability.
    - Validate appointment slots to avoid overlapping bookings.
  - Create utility functions to assist with date and time validations.
- **Notes:**
  - Emphasize robust error handling to return clear error messages when scheduling conflicts occur.
  - Refer to [UserFlow.md](./UserFlow.md) for the detailed booking and scheduling process.

### 4. Build Email Notification Integration for Appointment Confirmations
- **Action:**
  - Integrate an email service (using Nodemailer or a similar tool) into the Appointment module.
  - Create a service method to send confirmation emails to Clients upon successful booking.
- **Example Code Snippet:**
  ```typescript
  // backend/src/appointment/appointment.service.ts
  import * as nodemailer from 'nodemailer';

  async function sendConfirmationEmail(email: string, appointmentDetails: any) {
    const transporter = nodemailer.createTransport({
      service: 'gmail',
      auth: {
        user: process.env.EMAIL_USER,
        pass: process.env.EMAIL_PASS,
      },
    });

    const mailOptions = {
      from: process.env.EMAIL_USER,
      to: email,
      subject: 'Appointment Confirmation',
      text: `Your appointment has been scheduled on ${appointmentDetails.date}.`,
    };

    await transporter.sendMail(mailOptions);
  }
  ```
- **Notes:**
  - Store email credentials securely in the `.env` file.
  - Document the email confirmation process in your API documentation.

### 5. Frontend Integration for Booking Appointments
- **Action:**
  - In the Next.js frontend, create a dedicated booking page (e.g., `/appointments`) using MantineUI components.
  - Implement a form where Clients can select a date, time, and desired Lawyer.
  - Use React Query to handle API calls for creating an appointment.
- **Example Instructions:**
  - Create a new file at `frontend/src/pages/appointments.tsx`.
  - Use date pickers and time selectors from MantineUI for input.
- **Notes:**
  - Ensure the form validates user input against business rules (e.g., date selection must be in the future).

### 6. Testing and Verification
- **Action:**
  - Write unit tests for the Appointment service to verify conflict checking and scheduling logic.
  - Create integration tests to validate the booking workflow from frontend submission to backend confirmation.
- **Notes:**
  - Use Jest for backend testing and React Testing Library for frontend tests.
  - Document test cases and expected outcomes.

### 7. Commit and Update Documentation
- **Action:**
  - Commit your changes with a descriptive message:
    ```bash
    git add .
    git commit -m "Phase 5: Implement appointment scheduling with conflict resolution and email notifications"
    ```
  - Update relevant documentation (Swagger API docs, project-context, and README) to include details about the appointment scheduling module.
- **Notes:**
  - Ensure that all updates conform to the predefined project structure and coding standards.

## Expected Outcome
- A fully functional Appointment module in the backend integrated with Prisma and conflict-checking logic.
- Email notifications for appointment confirmations are properly configured and tested.
- Frontend booking pages that allow Clients to select appointment slots, validate inputs, and submit bookings successfully.
- Comprehensive tests and updated documentation to support ongoing maintenance and scalability.

---

## References
- [NestJS Controllers](https://docs.nestjs.com/controllers)
- [Prisma Transactions](https://www.prisma.io/docs/concepts/components/prisma-client/transactions)
- [Class-Validator Documentation](https://github.com/typestack/class-validator) 