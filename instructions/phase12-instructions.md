# Phase 12: Frontend Setup

## Objective
Set up the frontend using Next.js with TypeScript to establish a modern, maintainable base for the Advolot application. Configure UI frameworks (MantineUI and Tailwind CSS), integrate React Query for data fetching, and prepare the project for Progressive Web App (PWA) capabilities. Ensure all new files and folders adhere to the structured guidance provided in `project-context.md`.

## Detailed Steps

### 1. Initialize the Next.js Project
- **Action:**
  - Navigate to the frontend directory (create a dedicated `frontend` folder if it doesn't exist).
  - Initialize a Next.js project with TypeScript support using the appropriate command.
- **Commands Example:**
  ```bash
  cd frontend
  npx create-next-app@latest . --typescript --use-npm --app
  ```
- **Notes:**
  - This command generates the basic Next.js application structure. Ensure that the generated folder structure aligns with the `project-context.md` guidelines.

### 2. Install Required Dependencies
- **Action:**
  - Install the necessary packages, including:
    - MantineUI: For UI components.
    - Tailwind CSS: For styling.
    - React Query: For data fetching.
    - Next PWA: For enabling PWA capabilities.
- **Commands Example:**
  ```bash
  npm install @mantine/core @mantine/hooks @mantine/notifications tailwindcss postcss autoprefixer @tanstack/react-query next-pwa
  npx tailwindcss init -p
  ```
- **Notes:**
  - Ensure that all peer dependencies are installed.

### 3. Setup Global Styling with Tailwind CSS
- **Action:**
  - Configure Tailwind CSS:
    - Update `tailwind.config.js` with the proper content paths for your Next.js project.
    - Import Tailwind CSS in your global stylesheet (e.g., `styles/globals.css`).
- **Example Configuration:**
  ```javascript
  // Example tailwind.config.js
  module.exports = {
    content: [
      "./pages/**/*.{js,ts,jsx,tsx}",
      "./components/**/*.{js,ts,jsx,tsx}",
    ],
    theme: {
      extend: {},
    },
    plugins: [],
  };
  ```
- **Notes:**
  - Ensure that your custom styles do not conflict with MantineUI defaults.

### 4. Setup PWA Functionality
- **Action:**
  - Configure Next PWA by updating `next.config.js`:
  ```javascript
  // frontend/next.config.js
  const withPWA = require('next-pwa')({
    dest: 'public',
    disable: process.env.NODE_ENV === 'development',
    register: true,
    skipWaiting: true,
  });

  module.exports = withPWA({
    reactStrictMode: true,
    // Additional Next.js configuration...
  });
  ```
- **Notes:**
  - Verify PWA functionality using Lighthouse in Chrome DevTools.

### 5. Organize Folder Structure
- **Action:**
  - Ensure the frontend folder structure aligns with the project organization:
    - `/pages`: For route-based components.
    - `/components`: For reusable UI parts.
    - `/styles`: For global styles.
    - `/public`: For static assets such as the PWA manifest and icons.
- **Notes:**
  - Follow standardized naming conventions and ensure consistency across the project.

### 6. User Flow Reference
- **Action:**
  - Review the [UserFlow.md](./UserFlow.md) document for a detailed outline of the user journey, which includes both client and lawyer perspectives.
- **Notes:**
  - Use the user flow guidelines to inform UI/UX decisions during development.

### 7. Commit and Document Setup
- **Action:**
  - Document the frontend setup process in the `README.md` or a dedicated frontend documentation file.
  - Commit all configurations and initial setup files.
- **Example Commit Command:**
  ```bash
  git add .
  git commit -m "Phase 12: Set up Next.js frontend with necessary tools and PWA functionality"
  ```

## Expected Outcome
- A fully configured Next.js frontend application leveraging TypeScript, MantineUI, and Tailwind CSS.
- PWA capabilities enabled and verified using industry-standard testing (e.g., Lighthouse).
- A structured project layout that complies with `project-context.md` and is informed by the detailed user flow in [UserFlow.md](./UserFlow.md).
- Comprehensive documentation of the frontend setup for effective onboarding and maintenance.

---

## References
- [Next.js Documentation](https://nextjs.org/docs)
- [Mantine Documentation](https://mantine.dev/docs/getting-started/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs/guides/nextjs)
- [React Query Documentation](https://tanstack.com/query/v4/docs/overview)
- [next-pwa Documentation](https://github.com/shadowwalker/next-pwa) 