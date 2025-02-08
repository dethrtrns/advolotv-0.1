# Phase 3: Authentication & Authorization

## Objective
Implement a secure authentication system using JWT and integrate OAuth (Google, with plans for LinkedIn). This phase also establishes role-based access control to clearly separate Clients and Lawyers. All implementations should strictly follow the project structure defined in `project-context.md` and adhere to our coding and documentation standards.

## Detailed Steps

### 1. Create the Auth Module
- **Action:**
  - Generate the Auth module using the NestJS CLI:
    ```bash
    cd backend
    nest generate module auth
    ```
  - Create initial files for controllers, services, and strategies.  
- **Notes:**
  - This module will centralize all authentication and authorization logic.

### 2. Configure JWT Authentication
- **Action:**
  - Install necessary libraries:
    ```bash
    npm install @nestjs/jwt passport-jwt @nestjs/passport passport
    ```
  - Create a JWT strategy (e.g., `jwt.strategy.ts`) that extracts and validates JWT tokens.
  - Configure the JwtModule in the Auth module with environment variables (use the `JWT_SECRET` from your `.env` file).
- **Example Code:**
  ```typescript
  // backend/src/auth/jwt.strategy.ts
  import { Injectable } from '@nestjs/common';
  import { PassportStrategy } from '@nestjs/passport';
  import { ExtractJwt, Strategy } from 'passport-jwt';

  @Injectable()
  export class JwtStrategy extends PassportStrategy(Strategy) {
    constructor() {
      super({
        jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
        ignoreExpiration: false,
        secretOrKey: process.env.JWT_SECRET,
      });
    }

    async validate(payload: any) {
      return { userId: payload.sub, username: payload.username, roles: payload.roles };
    }
  }
  ```
- **Notes:**
  - Ensure your `.env` file contains a secure `JWT_SECRET`.

### 3. Implement OAuth Integrations
- **Action:**
  - For Google OAuth:
    - Install necessary libraries:
      ```bash
      npm install passport-google-oauth20
      ```
    - Create a Google strategy file (e.g., `google.strategy.ts`) to handle OAuth flow.
  - Document the steps needed to add LinkedIn OAuth in the future.
- **Notes:**
  - Securely manage OAuth credentials via environment variables.
  - Use clear comments in your strategy files to outline how to extend this integration.

### 4. Role-Based Access Control
- **Action:**
  - Update your Prisma schema (if not already) to model user roles (e.g., enum with `CLIENT` and `LAWYER`).
  - Create custom decorators (e.g., `@Roles()`) and guards (e.g., `RolesGuard`) to enforce role-based access control at controller endpoints.
- **Example Code:**
  ```typescript
  // backend/src/auth/roles.decorator.ts
  import { SetMetadata } from '@nestjs/common';
  export const Roles = (...roles: string[]) => SetMetadata('roles', roles);
  ```
- **Notes:**
  - Implement comprehensive error handling within your guards.
  - Test the authorization logic thoroughly with both valid and invalid roles.

### 5. Documentation and Testing
- **Action:**
  - Update the API documentation (using Swagger, if applicable) to include details about the authentication endpoints and security flows.
  - Write integration tests to validate the authentication system using Jest. Include tests for token generation, OAuth flows, and role-based route protection.
- **Notes:**
  - Ensure all modifications are committed appropriately with descriptive messages.
  - Document any assumptions or changes in the `project-context.md` if needed.

### 6. Commit and Update Documentation
- **Action:**
  - Commit changes with a clear message:
    ```bash
    git add .
    git commit -m "Phase 3: Implement JWT and OAuth authentication with role-based access control"
    ```
  - Update the `README.md` and any relevant documentation to include an overview of the implemented auth mechanisms.
- **Notes:**
  - Maintain clear and informative commit messages and documentation for onboarding and future reference.

## Expected Outcome
- A fully functional authentication system with both JWT and OAuth support.
- Secure role-based access control mechanisms in place.
- Comprehensive testing and documentation for the authentication process.
- A modular and easily extensible Auth module, in line with our `project-context.md` guidelines.

---

## References
- [NestJS Authentication](https://docs.nestjs.com/security/authentication)
- [Prisma Authentication Example](https://www.prisma.io/docs/guides/authentication)
- [Passport.js Documentation](http://www.passportjs.org/docs/)
- [Google OAuth Integration](https://developers.google.com/identity/protocols/oauth2) 