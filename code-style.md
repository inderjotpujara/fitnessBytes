# Code Style Guide

## Language
- Use TypeScript exclusively for both frontend and backend
- Enable strict type checking

## Linting/Formatting
- Enforce ESLint and Prettier rules rigorously
- Integrate into CI pipeline
- Use established configs (e.g., Airbnb style guide, Expo defaults)

## Naming Conventions
- Use clear, descriptive names
- camelCase for variables/functions
- PascalCase for classes/components/types

## Comments
- Write comprehensive JSDoc/TSDoc comments
- Explain the _why_, not just the _what_

## Modularity (React Native)
- Create small, single-purpose functional components
- Utilize hooks for logic reuse
- Separate components into presentational and container layers

## Modularity (Backend)
- Organize code by feature (e.g., `users`, `expenses`, `groups`, `ai`)
- Use dependency injection
- Follow SOLID principles

## Error Handling
- Implement robust error handling
- Use try...catch blocks and custom error classes
- Centralized error logging
- Avoid swallowing errors

## Security
- Validate and sanitize all user inputs
- Use parameterized queries/ORM methods
- Store secrets securely using environment variables
- Implement rate limiting on APIs

## Git Workflow
- Use feature branches
- Create pull requests for code review
- Require CI checks before merging
- Write meaningful commit messages