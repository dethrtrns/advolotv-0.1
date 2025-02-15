# Advolot Project Development Rules
description: Rules for AI assistance in developing the Advolot legal consultation platform
author: Project Team
version: 1.0.0

# Global Architecture Standards
architecture:
  - Follow clean architecture principles with clear separation of concerns
  - Maintain strict module boundaries between client and lawyer functionalities
  - Implement progressive complexity - start monolithic, evolve to modular
  - Use TypeScript strictly with proper type definitions
  - Follow SOLID principles and DRY methodology
  - Implement proper error handling and logging
  - Ensure security best practices at all layers

# Frontend (Next.js) Rules
frontend:
  structure:
    - Use Next.js 14+ with App Router
    - Organize by feature/module in src/app directory
    - Separate components into atomic design pattern:
      - atoms/ (basic components)
      - molecules/ (component combinations)
      - organisms/ (complex components)
      - templates/ (page layouts)
    - Keep pages clean, logic in hooks/services

  components:
    - Use functional components with TypeScript
    - Implement proper prop typing
    - Follow naming convention: PascalCase for components
    - Include JSDoc comments for complex components
    - Structure:
      ```tsx
      import { FC } from 'react'
      
      interface ComponentProps {
        // prop definitions
      }
      
      export const Component: FC<ComponentProps> = ({ props }) => {
        // implementation
      }
      ```

  state_management:
    - Use React Query for server state
    - Context API for global UI state
    - Keep component state minimal
    - Implement proper loading/error states

  styling:
    - Use MantineUI components as base
    - Tailwind CSS for custom styling
    - Follow BEM methodology for custom classes
    - Maintain consistent spacing/sizing units

# Backend (NestJS) Rules
backend:
  structure:
    - Follow NestJS module architecture
    - Separate business logic from controllers
    - Implement repository pattern with Prisma
    - Clear separation of DTOs and entities

  modules:
    - One module per feature domain
    - Structure:
      ```
      feature/
        ├── dto/
        ├── entities/
        ├── feature.controller.ts
        ├── feature.service.ts
        ├── feature.module.ts
        └── feature.types.ts
      ```

  coding_standards:
    - Use dependency injection
    - Implement proper validation pipes
    - Follow RESTful conventions
    - Structure:
      ```typescript
      @Injectable()
      export class FeatureService {
        constructor(
          private prisma: PrismaService,
          private config: ConfigService
        ) {}
        
        async method(): Promise<Result> {
          // implementation
        }
      }
      ```

  database:
    - Use Prisma as ORM
    - Implement proper migrations
    - Follow naming conventions:
      - Tables: plural, snake_case
      - Columns: snake_case
      - Models: singular, PascalCase

# Testing Standards
testing:
  frontend:
    - Jest for unit tests
    - React Testing Library for component tests
    - Cypress for E2E testing
    - Test structure:
      ```typescript
      describe('Component', () => {
        it('should render correctly', () => {
          // test implementation
        })
      })
      ```

  backend:
    - Jest for unit/integration tests
    - Supertest for E2E API testing
    - Mock external services
    - Maintain test database

# Documentation Requirements
documentation:
  - JSDoc comments for complex functions
  - README for each module
  - API documentation using Swagger
  - Maintain changelog
  - Example:
    ```typescript
    /**
     * @description Process user authentication
     * @param {AuthDto} authDto - Authentication credentials
     * @returns {Promise<AuthResponse>} Authentication result
     * @throws {UnauthorizedException} Invalid credentials
     */
    ```

# Error Handling
error_handling:
  frontend:
    - Implement error boundaries
    - Proper error states in components
    - User-friendly error messages

  backend:
    - Use custom exception filters
    - Proper HTTP status codes
    - Structured error responses
    - Example:
      ```typescript
      throw new HttpException({
        status: HttpStatus.BAD_REQUEST,
        error: 'Validation failed',
        details: errors
      }, HttpStatus.BAD_REQUEST);
      ```

# Security Standards
security:
  - Implement proper authentication/authorization
  - Input validation
  - XSS prevention
  - CSRF protection
  - Rate limiting
  - Secure headers
  - Environment variable validation

# Performance Guidelines
performance:
  frontend:
    - Implement proper code splitting
    - Optimize images and assets
    - Use proper caching strategies
    - Minimize bundle size

  backend:
    - Implement caching where appropriate
    - Optimize database queries
    - Handle proper pagination
    - Implement request timeout handling

# Version Control
git:
  - Meaningful commit messages
  - Feature branch workflow
  - Branch naming: feature/, bugfix/, hotfix/
  - Pull request templates
  - Proper version tagging