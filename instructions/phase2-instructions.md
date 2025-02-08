# Phase 2: Backend Architecture

## Objective
Develop a robust backend that addresses current structural challenges. Build the backend from scratch using NestJS with TypeScript, integrate PostgreSQL with Prisma ORM, and set up cloud storage (Google Cloud Storage/AWS S3) for document handling. Maintain strict adherence to the project structure as defined in `project-context.md`.

## Detailed Steps

### 1. NestJS Project Initialization
- **Action:**
  - Navigate to the backend directory.
  - Install the NestJS CLI globally if not already installed.
  - Create a new NestJS project using the CLI.
- **Commands Example:**
  ```bash
  cd backend
  npm install -g @nestjs/cli
  nest new backend --package-manager npm
  ```
- **Notes:**
  - The newly generated code will follow the default NestJS structure. Future modifications will align with our module structure outlined in `project-context.md`.

### 2. Set Up Prisma ORM and PostgreSQL
- **Action:**
  - Install Prisma as a development dependency along with the Prisma client.
  - Initialize Prisma to create the basic configuration and schema directory.
- **Commands Example:**
  ```bash
  npm install prisma --save-dev
  npm install @prisma/client
  npx prisma init
  ```
- **Next Steps:**
  - Update `prisma/schema.prisma` with initial models for Users, Roles, and other entities as needed.
  - Ensure that the models reflect early separation of Clients and Lawyers as indicated in the project context.
- **Notes:**
  - Version the Prisma schema file carefully; commit changes incrementally as new fields/entities are needed.

### 3. Environment Configuration
- **Action:**
  - Create or update the `.env` file in the backend root.
  - Add essential environment variables, such as:
    - `DATABASE_URL` for your PostgreSQL connection.
    - `JWT_SECRET` for authentication.
    - Cloud storage keys (e.g., `GCS_KEY`, if using Google Cloud Storage).
  - Use placeholders if the actual values are not available.
- **Example `.env` Content:**
  ```plaintext
  DATABASE_URL=postgresql://user:password@localhost:5432/advolot_db
  JWT_SECRET=your_jwt_secret
  GCS_KEY=your_google_cloud_storage_key
  ```

### 4. Cloud Storage Integration Setup
- **Action:**
  - Decide on the cloud storage service (Google Cloud Storage or AWS S3) as per the project context.
  - Install the corresponding client library.
    - For Google Cloud Storage: 
      ```bash
      npm install @google-cloud/storage
      ```
    - For AWS S3 (if preferred in future iterations):
      ```bash
      npm install aws-sdk
      ```
  - Create a dedicated service (e.g., `storage.service.ts`) within the backend to handle file uploads/downloads.
- **Notes:**
  - Ensure the service utilizes environment variables for secure access to storage credentials.

### 5. Modular Architecture and Code Organization
- **Action:**
  - Organize the backend into key modules (Auth, User, Document, etc.).
  - Create modules using NestJS CLI to ensure consistency:
    ```bash
    nest generate module auth
    nest generate module user
    nest generate module document
    ```
- **Notes:**
  - Follow naming and file structure conventions as outlined in `project-context.md`. Emphasize separation between Client and Lawyer functionalities starting from user models.

### 6. Configure Code Quality & Linting Tools
- **Action:**
  - Set up ESLint and Prettier for the backend as per the Code Editor Rules.
  - Generate configuration files (e.g., `.eslintrc.js`, `.prettierrc`) in the backend root.
- **Notes:**
  - This step ensures that the backend code adheres to our strict style and quality guidelines from the start.

### 7. Commit and Document
- **Action:**
  - Once initial setup is complete, commit all changes with a descriptive message.
  - Update `README.md` (or related documentation) to reflect the backend architecture.
- **Example Commit Command:**
  ```bash
  git add .
  git commit -m "Phase 2: Initialize backend with NestJS, Prisma ORM, and cloud storage integration"
  ```
- **Notes:**
  - Documentation should reference the `project-context.md` for ongoing architectural context.

## Expected Outcome
- A fully initialized NestJS project with a modular structure.
- Integrated Prisma ORM configured with PostgreSQL.
- Basic implementation of cloud storage services for document management.
- Environment configuration and code quality tools in place.
- A solid backend foundation that adheres to the project-context structure and sets the stage for subsequent phases.

---

## References
- [NestJS Documentation](https://docs.nestjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs/)
- [Google Cloud Storage Documentation](https://cloud.google.com/storage/docs)
- [JWT Authentication](https://jwt.io/introduction/) 