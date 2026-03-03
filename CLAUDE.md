# CLAUDE.md

This file provides guidance to Claude Code when working with code in this repository.

## Project Overview

Happy Coder is a monorepo providing mobile, web, and CLI clients for Claude Code and Codex with end-to-end encryption. It allows users to control AI coding agents remotely via iOS, Android, and web applications.

## Monorepo Structure

```
packages/
├── happy-cli/      # CLI wrapper for Claude Code (Node.js/TypeScript)
├── happy-app/      # Mobile app (React Native + Expo) & Web UI
├── happy-server/   # Backend server (Fastify + PostgreSQL)
├── happy-agent/    # Remote agent control CLI
└── happy-wire/     # Shared wire protocols and Zod schemas
```

Each package has its own `CLAUDE.md` with package-specific guidelines — always read the relevant one before working in a package.

## Commands

### Root
- `yarn cli` - Run the CLI from source
- `yarn web` - Run the web app
- `yarn release` - Trigger release process

### happy-cli (`yarn workspace happy-coder <cmd>`)
- `yarn build` - Build with pkgroll
- `yarn test` - Run tests (Vitest)
- `yarn dev` - Development mode (tsx)

### happy-app
- `yarn start` - Expo dev server
- `yarn ios` / `yarn android` / `yarn web` - Platform-specific dev
- `yarn typecheck` - TypeScript type checking
- `yarn test` - Run tests (Vitest)
- `yarn ota` - Deploy OTA updates

### happy-server
- `yarn build` - TypeScript type checking
- `yarn start` - Start the server
- `yarn dev` - Development mode
- `yarn test` - Run tests (Vitest)
- `yarn migrate` - Run Prisma migrations
- `yarn generate` - Generate Prisma client

### happy-wire
- `yarn build` - Build
- `yarn test` - Run tests (Vitest)

## Code Style (All Packages)

- **4 spaces** for indentation (not 2)
- **TypeScript strict mode** — no untyped code
- **Explicit type annotations** on function parameters and return types
- **Functional programming** preferred — avoid classes
- **Named exports** preferred
- **All imports at the top** of the file — never import mid-code
- **Path alias `@/`** for src imports in all packages
- **Yarn** for package management (not npm)
- Avoid enums; use maps instead
- Avoid creating unnecessary small functions, getters, or setters
- No backward compatibility unless explicitly requested

## Testing

- All packages use **Vitest**
- happy-cli: test files colocated with source (`.test.ts`), no mocking
- happy-server: test files use `.spec.ts` suffix, write tests before implementation for utilities
- Run `yarn test` in the relevant package directory

## Key Architectural Decisions

1. **End-to-end encryption** for all communications (TweetNaCl in CLI, libsodium in app)
2. **Socket.IO** for real-time WebSocket communication
3. **Zod** for runtime type validation across all packages
4. **Prisma** as ORM for the server (never create migrations manually)
5. **Dual mode** in CLI: interactive (terminal) and remote (mobile control)

## DO NOT

- Create files unless absolutely necessary — prefer editing existing files
- Create documentation files unless explicitly requested
- Add logging, error handling, or features beyond what was asked
- Run non-transactional operations (like file uploads) inside database transactions
- Use npm — always use yarn
