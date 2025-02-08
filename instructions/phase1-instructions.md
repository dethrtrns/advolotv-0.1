# Phase 1: Project Setup

## Objective
Restart the project from scratch to address existing structural and architectural problems. From the very beginning, ensure that Clients and Lawyers are modeled as separate entities. Create only the necessary files and folders at each stage following the structure defined in our project-context. This phase establishes a solid, organized foundation for the entire project.

## Detailed Steps

### 1. Repository Initialization and Branch Setup
- **Action:**
  - Create a new Git repository (e.g., on GitHub, GitLab, etc.).
  - Clone the repository locally.
  - Configure Git (set your user name and email if not already set).
  - Create an initial commit.
- **Commands Example:**
  ```bash
  git init
  git config user.name "Your Name"
  git config user.email "your.email@example.com"
  git add .
  git commit -m "Initial commit – Repository setup"
  ```
- **Notes:**
  - Use branch naming conventions (e.g., `feature/`, `bugfix/`) as outlined in the Code Editor Rules.

### 2. Establish Project Structure Based on `project-context.md`
- **Action:**
  - Create only the necessary folders and files as defined in our project-context.
  - **Required Structure for Phase 1:**
    - Root:
      - `README.md` (Initial project overview and links to documentation)
      - `.gitignore`
      - `project-context.md` (reviewed and updated)
      - `roadmap.md`
    - `src/` (will contain future code; to be created as needed)
    - `prisma/` (for database schema and migrations; create folder but add content only when schema changes are needed)
    - `docs/` (for future detailed documentation)
    - `restart-project-with-o1/` (contains phase instruction files and relevant documentation)
- **Notes:**
  - Only create additional folders/files (e.g., for Clients and Lawyers separation) when needed in subsequent phases.
  - Ensure that every file/folder adheres to the naming conventions and structure specified in the `project-context.md`.

### 3. Initial README.md Setup
- **Action:**
  - Create a basic `README.md` file with:
    - Project title (e.g., "Advolot Project")
    - Brief description of the project's purpose (legal consultation platform)
    - Links to `project-context.md` and `roadmap.md`
- **Example Content:**
  ```markdown
  # Advolot Project
  
  Advolot is a legal consultation platform connecting clients with lawyers. This repository serves as the foundation for a modular, scalable system designed with clear separation of concerns starting from the client and lawyer modules.
  
  ## Documentation
  - [Project Context](./restart-project-with-o1/project-context.md)
  - [Project Roadmap](./restart-project-with-o1/roadmap.md)
  ```

### 4. Setting Up Environment
- **Action:**
  - Create basic configuration files:
    - A `.gitignore` file to exclude Node modules, environment files (`.env`), logs, and build artifacts.
    - A basic `.env` template file that will be expanded in later phases (include placeholders for `DATABASE_URL`, `JWT_SECRET`, etc.).
- **Example `.gitignore` Content:**
  ```plaintext
  node_modules/
  .env
  dist/
  coverage/
  ```
- **Notes:**
  - This helps ensure that sensitive information is not committed to the repository.

### 5. Initialize Package Managers for Frontend and Backend
- **Action:**
  - **Backend (NestJS & TypeScript):**
    - Create a new NestJS application:
      ```bash
      cd backend
      npm install -g @nestjs/cli
      nest new backend --package-manager npm
      ```
    - Use the default structure initially; modifications will be made in later phases.
  - **Frontend (Next.js & TypeScript):**
    - Create a new Next.js application:
      ```bash
      cd ../frontend
      npx create-next-app@latest . --typescript --use-npm --app
      ```
- **Notes:**
  - Follow the version recommendations provided in the project documentation or README.
  - Ensure the created folders adhere to our `project-context.md` structure.

### 6. Configure Code Quality Tools
- **Action:**
  - Install and set up ESLint and Prettier based on our Code Editor Rules.
  - Create configuration files (e.g., `.eslintrc.js` and `.prettierrc`) in the root of each project (frontend and backend).
- **Notes:**
  - This step ensures automated code reviews and consistent formatting from the start.

### 7. Documentation and Context Linkage
- **Action:**
  - Verify that the `project-context.md` and `roadmap.md` are present in the `restart-project-with-o1/` directory.
  - Cross-reference these documents in `README.md` so that every team member or AI assistant can easily get an overview of project architecture and goals.
- **Notes:**
  - This linkage helps avoid the need to parse the entire codebase to understand project requirements.

## Expected Outcome
- A newly initialized repository with the defined minimal folder structure.
- Essential configuration files and initial application setups for both frontend (Next.js) and backend (NestJS).
- Clear documentation linking to the project context and roadmap to guide further development.
- Adherence to strict file/folder creation based on our pre-defined project structure ensuring scalability and maintainability.

---

## References
- [Git Documentation](https://git-scm.com/doc)
- [npm Documentation](https://docs.npmjs.com/) 