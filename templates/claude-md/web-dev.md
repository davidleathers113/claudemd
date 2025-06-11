# [PROJECT_NAME] - Web Application

## Overview
TODO: Describe your web app, target users, and main features.

**Tech Stack:**
- Frontend: TODO: React/Vue/Angular + version
- State Management: TODO: Redux/Vuex/Context/etc
- Styling: TODO: CSS/Sass/Tailwind/Styled-components
- Build Tool: TODO: Vite/Webpack/Next.js/etc
- Package Manager: TODO: npm/yarn/pnpm

## 🛠 Commands
```bash
# Development
npm run dev          # Start dev server on http://localhost:3000
npm run build        # Build for production
npm run preview      # Preview production build

# Quality
npm test            # Run tests
npm run test:watch  # Run tests in watch mode
npm run lint        # ESLint check
npm run format      # Prettier format

# TODO: Add your specific commands
```

## 📁 Project Structure
```
├── src/
│   ├── components/     # Reusable components
│   ├── pages/         # Page components
│   ├── hooks/         # Custom React hooks
│   ├── utils/         # Helper functions
│   ├── services/      # API services
│   ├── styles/        # Global styles
│   └── types/         # TypeScript types
├── public/            # Static assets
├── tests/            # Test files
└── [TODO: Add other important directories]
```

## 🎨 Development Guidelines

### Component Standards
- **Naming**: PascalCase for components, camelCase for utilities
- **Structure**: One component per file
- **Props**: Use TypeScript interfaces, destructure in parameters
- **Hooks**: Custom hooks start with 'use'

### Code Style
```typescript
// Component template
interface ComponentProps {
  // TODO: Define your prop interface pattern
}

export const Component: React.FC<ComponentProps> = ({ prop1, prop2 }) => {
  // Hooks at the top
  // Event handlers next
  // Render logic last
  return <div>{/* JSX */}</div>
};
```

### State Management
TODO: Describe your state management patterns
- Local state: useState for component-specific
- Global state: [Your solution]
- Server state: [React Query/SWR/etc]

### API Integration
```typescript
// Service pattern
export const apiService = {
  async getItems() {
    // TODO: Your API pattern
  }
};
```

### Testing Strategy
- Unit tests: Components and utilities
- Integration tests: API interactions
- E2E tests: Critical user flows
- Coverage target: TODO: 80%?

## 🚀 Development Workflow

### Starting a New Feature
1. Create feature branch: `git checkout -b feat/feature-name`
2. Implement with tests
3. Run `npm run lint && npm test`
4. Create PR with description

### Component Creation
TODO: Do you use component generators? Specific patterns?

### Performance Considerations
- Lazy load routes
- Memoize expensive computations
- Optimize images
- TODO: Add project-specific performance rules

## 🔧 Environment Setup
```env
# .env.example
VITE_API_URL=http://localhost:8000
TODO: Add other env vars
```

## 🚫 Important Rules
- Never commit sensitive data
- Always handle loading and error states
- Accessibility is required (WCAG 2.1 AA)
- TODO: Add project-specific rules

## 💡 Claude-Specific Context
- We use TODO: [specific UI library]
- Authentication is handled by TODO: [auth solution]
- Forms should use TODO: [form library]
- Error boundaries are required for all pages
- TODO: Add other architectural decisions

## 📚 Resources
- Design System: TODO: Link to design docs
- API Docs: TODO: Link to backend docs
- Deployment Guide: TODO: Link to deployment docs