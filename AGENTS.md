# AGENTS.md

This document provides guidelines for AI agents working in this repository.

## Build, Lint, and Test Commands

This is a Node.js/TypeScript project using the OpenCode AI SDK.

### Package Management

- **Install dependencies**: `npm install` or `bun install`
- **Add new dependency**: `npm install <package>` or `bun add <package>`
- **Remove dependency**: `npm uninstall <package>` or `bun remove <package>`

### Development

- **Type checking**: `npx tsc --noEmit` (if TypeScript is configured)
- **Lint**: `npm run lint` (if configured in package.json)
- **Format**: Use Prettier on changed files
- **Build**: `npm run build` (if build script exists)

### Testing

- **Run all tests**: `npm test`
- **Run single test**: `npm test -- --testNamePattern="test name"` or `npm test -- test-file-name`
- **Run tests in watch mode**: `npm test -- --watch`

## Code Style Guidelines

### TypeScript Usage

- Use TypeScript for all new code
- Enable `strict` mode in tsconfig.json
- Prefer explicit types over inference for function parameters and return types
- Use `interface` for object types and `type` for unions, primitives, or mapped types
- Avoid `any` - use `unknown` when type is truly unknown
- Use `as const` for literal values that shouldn't widen

### Naming Conventions

- **Files**: kebab-case for files (e.g., `user-service.ts`, `data-utils.ts`)
- **Classes/PInterfaces**: PascalCase (e.g., `UserService`, `ApiResponse`)
- **Variables/Constants/functions**: camelCase (e.g., `userName`, `getUserData`)
- **Constants**: SCREAMING_SNAKE_CASE for configuration constants (e.g., `MAX_RETRIES`)
- **Private members**: Prefix with underscore `_` (e.g., `_cache`, `_initialize()`)
- **Booleans**: Use `is`, `has`, `should` prefixes (e.g., `isValid`, `hasError`)

### Imports

- Use absolute imports when available (configured via tsconfig paths)
- Group imports in this order:
  1. Built-in Node.js modules
  2. External packages
  3. Relative imports (using `./` and `../`)
- Use named imports: `import { foo, bar } from 'module'`
- Default imports only for main export: `import React from 'react'`
- Avoid side-effect imports: `import './style.css'` (use only when necessary)

### Formatting

- Use 2 spaces for indentation
- Semicolons: Required
- Quotes: Single quotes for strings
- Line length: 100 characters maximum
- Trailing commas: Required for multi-line objects/arrays
- No blank lines at end of file
- One blank line between function declarations

### Error Handling

- Use try/catch for async operations
- Create custom error classes extending `Error` for domain errors
- Always include error messages: `throw new Error('Descriptive message')`
- Use Result/Either types for operations that can fail
- Log errors with context before re-throwing or handling
- Never expose internal error details to users in production
- Use error boundaries for UI components

### Async/Await

- Use `async/await` over Promise chains
- Handle async errors with try/catch
- Avoid `await` in loops when parallel execution is safe
- Use `Promise.all()` for parallel async operations
- Add type annotations for async return types

### Component Structure

- Keep components small and focused (single responsibility)
- Extract complex logic into custom hooks or utility functions
- Use composition over inheritance
- Destructure props for readability
- Define prop types with TypeScript interfaces

### Testing Guidelines

- Write tests for all business logic functions
- Use descriptive test names: `it('should return user when valid id provided')`
- Mock external dependencies
- Test edge cases and error conditions
- Aim for meaningful coverage, not just line coverage

### General Practices

- Keep functions small (under 50 lines when possible)
- Single responsibility per function
- Avoid deep nesting (max 3-4 levels)
- Use early returns to reduce nesting
- Comments: Explain *why*, not *what*
- Keep code DRY (Don't Repeat Yourself)
- Refactor when duplication is found
- Update documentation when changing behavior
