# Code Generation Prompt: React Registration Module

## Objective
Create a basic registration module in React with the following components and features:

## Requirements

### 1. Login Page
- Create a responsive login page with the following fields:
  - Email input field (with validation)
  - Password input field (with password masking)
  - "Remember Me" checkbox
  - "Login" button
  - Link to navigate to the registration page
  - "Forgot Password?" link
- Implement form validation:
  - Email must be in valid format
  - Password must not be empty
  - Display appropriate error messages for invalid inputs
- Handle login submission with mock authentication
- Show loading state during authentication
- Redirect to dashboard upon successful login

### 2. Register Page
- Create a responsive registration page with the following fields:
  - Full Name input field
  - Email input field (with validation)
  - Password input field (with password strength indicator)
  - Confirm Password input field
  - "Register" button
  - Link to navigate back to the login page
- Implement comprehensive form validation:
  - Full name must not be empty
  - Email must be in valid format and unique
  - Password must meet minimum security requirements (min 8 characters, at least one uppercase, one lowercase, one number)
  - Confirm password must match the password field
  - Display real-time validation feedback
- Handle registration submission with mock API
- Show success message and redirect to login page after successful registration

### 3. Dashboard
- Create a basic dashboard that displays after successful login:
  - Header with user name and logout button
  - Welcome message with personalized greeting
  - Navigation sidebar with menu items:
    - Dashboard (active)
    - Profile
    - Settings
  - Main content area showing:
    - User statistics cards (placeholder data)
    - Recent activity section (placeholder data)
    - Quick actions section
- Implement logout functionality that:
  - Clears user session
  - Redirects back to login page
- Make the dashboard responsive for mobile and desktop views

## Technical Specifications

### Technology Stack
- React (with functional components and hooks)
- React Router for navigation
- CSS Modules or Styled Components for styling
- Context API or local state for authentication state management
- Form handling with controlled components

### Project Structure
```
src/
├── components/
│   ├── Login/
│   │   ├── Login.jsx
│   │   └── Login.module.css
│   ├── Register/
│   │   ├── Register.jsx
│   │   └── Register.module.css
│   └── Dashboard/
│       ├── Dashboard.jsx
│       ├── Dashboard.module.css
│       ├── Header.jsx
│       ├── Sidebar.jsx
│       └── MainContent.jsx
├── context/
│   └── AuthContext.jsx
├── utils/
│   └── validation.js
├── App.jsx
└── App.css
```

### Key Features to Implement
1. **Protected Routes**: Dashboard should only be accessible when user is authenticated
2. **Form Validation**: Real-time validation with user-friendly error messages
3. **Responsive Design**: Works seamlessly on mobile, tablet, and desktop
4. **State Management**: Proper state management for authentication and form data
5. **Mock Authentication**: Simulate API calls with setTimeout for realistic UX
6. **Loading States**: Show loading indicators during async operations
7. **Error Handling**: Display appropriate error messages for failed operations
8. **Accessibility**: Ensure forms are accessible with proper labels and ARIA attributes

## Additional Guidelines
- Use modern React best practices (hooks, functional components)
- Implement proper error boundaries
- Add PropTypes or TypeScript for type checking
- Include comments for complex logic
- Follow consistent naming conventions
- Ensure code is modular and reusable
- Add basic animations/transitions for better UX
- Store mock user data in localStorage for persistence across page refreshes

## Expected Deliverables
1. Fully functional Login page with validation
2. Fully functional Register page with validation
3. Fully functional Dashboard with user information
4. Protected routing between pages
5. Responsive design for all screen sizes
6. Clean, maintainable, and well-documented code
