# Phase 9: Payments Integration

## Objective
Integrate a secure payment gateway to facilitate financial transactions between Clients and Lawyers. This phase will set up both backend and frontend components to manage transactions, ensuring compliance with security standards and smooth user interactions. All implementations follow the predefined project structure and detailed guidelines.

## Detailed Steps

### 1. Create the Payment Module in the Backend
- **Action:**
  - Generate a new Payment module using the NestJS CLI:
    ```bash
    cd backend
    nest generate module payment
    ```
- **Notes:**
  - This module will encapsulate all payment-related functionality, including initiating transactions, handling webhooks, and updating transaction status.

### 2. Install and Configure Stripe
- **Action:**
  - Install the Stripe SDK:
    ```bash
    npm install stripe @types/stripe
    ```
  - Create a service file (e.g., `payment.service.ts`) to encapsulate payment operations.
- **Environment Configuration:**
  - Update the backend `.env` file with the following:
    ```plaintext
    STRIPE_SECRET_KEY=your_stripe_secret_key
    STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
    ```
- **Notes:**
  - Maintain secure handling of Stripe keys via environment variables.

### 3. Implement Payment Processing Endpoints
- **Action:**
  - In the Payment service, develop endpoints to:
    - Initiate payments: Create an endpoint to create a payment intent.
    - Listen to webhook events: Set up an endpoint to handle incoming Stripe webhook events (e.g., payment succeeded, payment failed).
- **Example Code Snippet (Creating a Payment Intent):**
  ```typescript
  // backend/src/payment/payment.service.ts
  import { Injectable, InternalServerErrorException } from '@nestjs/common';
  import Stripe from 'stripe';

  @Injectable()
  export class PaymentService {
    private stripe: Stripe;

    constructor() {
      this.stripe = new Stripe(process.env.STRIPE_SECRET_KEY, {
        apiVersion: '2022-11-15', // use the latest stable version as recommended
      });
    }

    async createPaymentIntent(amount: number, currency: string = 'usd'): Promise<Stripe.PaymentIntent> {
      try {
        const paymentIntent = await this.stripe.paymentIntents.create({
          amount,
          currency,
        });
        return paymentIntent;
      } catch (error) {
        throw new InternalServerErrorException('Failed to create payment intent');
      }
    }
  }
  ```
- **Notes:**
  - Use detailed comments in the code to explain the process and facilitate future maintenance.
  - Ensure that input data is validated, and errors are handled gracefully.

### 4. Secure Payment Processing
- **Action:**
  - Implement middleware or guards to ensure that only authenticated and authorized users (Client and Lawyer roles) can initiate payment requests.
- **Notes:**
  - Cross-check payments with related service logic (e.g., appointment scheduling) to ensure consistency.

### 5. Frontend Payment Integration
- **Action:**
  - In the Next.js frontend, create pages or components for managing payments.
  - Use Stripe's client-side SDK and MantineUI for building a secure payment form.
  - Configure React Query to handle API calls for payment intent creation.
- **Example Instructions:**
  - Create a file at `frontend/src/pages/payments.tsx`.
  - Integrate the Stripe.js library:
    ```bash
    npm install @stripe/stripe-js
    ```
  - Use Stripe Elements to build the payment form.
- **Notes:**
  - Ensure the frontend securely handles customer card information without exposing sensitive data.
  - Validate transaction details before submission.

### 6. Testing and Error Handling
- **Action:**
  - Write unit tests for the Payment service to cover various scenarios, including valid payment intents, failed payments, and webhook event handling.
  - Create end-to-end tests to simulate the complete payment workflow.
- **Notes:**
  - Use Jest for unit tests and integration tests.
  - Log detailed information for debugging and maintain a robust error-handling strategy.

### 7. Commit and Update Documentation
- **Action:**
  - Commit your changes with a descriptive message:
    ```bash
    git add .
    git commit -m "Phase 9: Implement payment integration using Stripe with secure endpoints and webhook handling"
    ```
  - Update API documentation (e.g., Swagger) to include payment endpoints and data models.
  - Reference the payment integration details in the `project-context.md`.
- **Notes:**
  - Ensure the documentation clearly outlines the payment process, integration points, and configuration settings.

### 2. Payment Gateway Integration
- **Action:**
  - Secure endpoints with proper authentication and authorization checks.
- **Notes:**
  - Refer to [UserFlow.md](./UserFlow.md) for the detailed payment and confirmation process.

## Expected Outcome
- A fully integrated Payment module in the backend that seamlessly creates payment intents and handles Stripe webhook events.
- A secure and user-friendly frontend interface to process payments.
- Comprehensive tests ensuring that all payment processing scenarios are handled correctly.
- Detailed documentation and commit history to support future maintenance and scalability.

---

## References
- [Stripe API Documentation](https://stripe.com/docs/api)
- [NestJS Stripe Integration](https://docs.nestjs.com/recipes/stripe)
- [Handling Webhooks Securely](https://stripe.com/docs/webhooks/best-practices) 