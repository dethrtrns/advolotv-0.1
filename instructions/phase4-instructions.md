# Phase 4: User Management

## Objective
Develop a comprehensive user management system that includes profile handling, role assignments, and administrative controls. This phase emphasizes the separate treatment of Clients and Lawyers and ensures that all changes adhere to the pre-defined project structure found in `project-context.md`.

## Detailed Steps

### 1. User Profile Module Enhancement
- **Action:**
  - Enhance the existing User module or create a new one if necessary.
  - Define models that capture distinct profile information for Clients and Lawyers, utilizing separate fields as required.
- **Prisma Schema Update:**
  - Update the `prisma/schema.prisma` file to include user role enumerations and associated fields. Example:
    ```prisma
    model User {
      id        Int      @id @default(autoincrement())
      email     String   @unique
      password  String
      name      String
      role      Role     // Enum: CLIENT or LAWYER
      // Lawyer-specific fields (nullable, for Clients)
      barNumber String?  
      specialty String?
      createdAt DateTime @default(now())
      updatedAt DateTime @updatedAt
    }
    
    enum Role {
      CLIENT
      LAWYER
    }
    ```
- **Notes:**
  - Ensure that the schema clearly differentiates between the two user types.
  - Run migrations after update:
    ```bash
    npx prisma migrate dev --name add_user_roles
    ```

### 2. Implement Role-Based Endpoints and Validation
- **Action:**
  - Create endpoints within the User controller for profile creation, editing, and deletion.
  - Validate incoming data so that Client and Lawyer profiles follow their specific format.
- **Example:**
  - Use DTOs (Data Transfer Objects) in NestJS to enforce validation rules.
  - Create separate DTOs if needed (e.g., `CreateClientDto` and `CreateLawyerDto`).
- **Notes:**
  - Ensure proper error handling and clear response messages if validations fail.

### 3. Role-Specific Business Logic and Administrative Controls
- **Action:**
  - Integrate business logic in the User service that handles role-specific operations.
  - Develop an Admin module for managing user accounts, including actions like deactivating accounts, role adjustments, and auditing changes.
- **Notes:**
  - Refer to [UserFlow.md](./UserFlow.md) for detailed insights into role-based navigation and interactions.

### 4. Frontend Integration for User Profiles
- **Action:**
  - In the Next.js frontend, build responsive pages for user registration, profile editing, and viewing.
  - Use MantineUI components to create forms that dynamically adjust based on the selected role (Client or Lawyer).
- **Example Instructions:**
  - Create a registration page with two separate tabs or conditional forms.
  - Ensure that the form validations reflect backend rules.
- **Notes:**
  - Utilize React Query for managing server-side state and updates for user profiles.

### 5. Testing and Documentation
- **Action:**
  - Write unit and integration tests to verify that user creation, profile updates, and administrative functions work as expected.
  - Update API documentation (Swagger or similar) to reflect endpoints and required input formats.
- **Notes:**
  - Include tests for both successful operations and expected failures (e.g., trying to update a lawyer field on a client profile).

### 6. Commit and Review
- **Action:**
  - Once all updates are tested, commit your changes with a descriptive message:
    ```bash
    git add .
    git commit -m "Phase 4: Implement comprehensive user management with role-based controls for Clients and Lawyers"
    ```
  - Ensure that documentation in `project-context.md` and `README.md` is updated accordingly.

## Expected Outcome
- A fully functional user management system with clear separation between Clients and Lawyers.
- Improved profile handling through validated endpoints and role-based business logic.
- Frontend pages that allow users to register, update, and view their profiles seamlessly.
- Comprehensive tests and documentation that make the system maintainable and extensible.

---

## References
- [NestJS Roles and Permissions](https://docs.nestjs.com/security/authorization)
- [Prisma Relations](https://www.prisma.io/docs/concepts/components/prisma-schema/relations)
- [Passport.js Roles Guard](https://docs.nestjs.com/security/authorization#roles-guards) 