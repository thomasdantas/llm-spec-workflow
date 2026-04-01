# AGENTS.md

<!-- TODO: Add guide for AI agents working with the code in this repository -->

Guide for AI agents working with the code in this repository.

### Priorities

<!-- TODO: Add priorities -->

- Always verify the skills
- Always use `pnpm` as package manager

### Commands

<!-- TODO: Add commands -->

- `pnpm install` to install dependencies
- `pnpm run dev` to start the development server
- `pnpm run build` to build the project
- `pnpm run start` to start the production server
- `pnpm run test` to run the tests
- `pnpm run lint` to run the linter
- `pnpm run format` to format the code
- `pnpm run type-check` to check the types

### Recommended stack and skills

<!-- TODO: Add recommended stack and skills -->

- `Node.js` 18+
- `pnpm` 9+
- `TypeScript` 5+
- `React` 18+
- `Next.js` 14+
- `Tailwind CSS` 3+
- `Shadcn UI` 1+
- `Lucide React` 1+
- `React Hook Form` 7+

### Project structure

<!-- TODO: Add project structure -->

```
frontend/
├── src/
│   ├── components/ui/   # Shadcn UI components
│   ├── lib/             # Utilities (utils.ts)
│   ├── App.tsx
│   └── main.tsx
backend/
├── src/
│   └── index.ts         # App Express, routes, middleware
```

### Git

<!-- TODO: Add git directives -->

- Never execute `git restore`, `git reset`, `git clean` or destructive commands without explicit permission from the user.

### Anti-patterns

<!-- TODO: Add anti-patterns -->

1. Skip skill activation
2. Activate only one skill when the code touches multiple domains
3. Avoid making workarounds
