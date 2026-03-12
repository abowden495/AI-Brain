# Prototype Setup

Create a prototype development environment by copying the **Liminal Prototype Template** — a pre-configured, self-contained copy of the production link-ui app with mock authentication, user context, and feature toggles. The prototype boots instantly with the full app shell (sidebar, header, navigation, design system) on port 3000.

**Approach:** Copy from a proven template, not scaffold from scratch.

---

## Prototype Template

**Source repo:** [owi-link/design-prototypes](https://github.com/owi-link/design-prototypes) — the template lives at `_liminal_template/` in the repo root.

The user must have a local clone of this repo. The location is not assumed — it will be asked in Step 1.

This template is a copy of the production **link-ui** codebase with the following modifications pre-applied:

| What | How |
|------|-----|
| **Authentication** | `Auth0Context.tsx` replaced with mock provider — `isAuthenticated: true`, mock user "Demo User" |
| **User profile** | `UserContext.tsx` replaced with mock provider — static user with `Provider` role, Liminal Demo org |
| **Feature toggles** | `FeatureTogglesContext.tsx` replaced with mock provider — all features enabled, no Unleash API call |
| **External services** | Pendo, IP fetch, Sentry guarded behind `VITE_PROTOTYPE_MODE` env var |
| **CookieBanner** | Removed from `App.tsx` (no Termly dependency) |
| **Sentry Vite plugin** | Removed from `vite.config.ts` (no auth token needed) |
| **Husky git hooks** | `prepare` script removed from `package.json` (no git) |
| **pnpm workspace** | Simplified `pnpm-workspace.yaml` (no `packages: src/**`) |
| **Environment** | `.env` with mock values — no real API keys, `VITE_PROTOTYPE_MODE=true` |
| **Test files** | Removed (`*.test.*`, `*.spec.*`, `__test__/` dirs) |

### Tech Stack (Mirrors link-ui Production)

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 18.2.x | UI framework |
| TypeScript | ~5.6.x | Type safety |
| Vite | ~5.4.x | Build tool + dev server |
| pnpm | latest | Package manager (**required**, not npm) |
| @owi-link/link-ds | 0.14.x | Liminal design system (37 components + pre-compiled Tailwind) |
| @owi-link/link-data-viz | 0.1.x | Data visualization components |
| Tailwind CSS | v3 | Utility CSS with `tw-` prefix |
| React Router | v6 | Client-side routing |
| React Query | v5 | Server state / data fetching |
| React Hook Form + Zod | latest | Form handling + validation |
| PrimeReact | 9.1.x | Additional UI components |

**Important:** Do NOT use shadcn/ui, Radix UI, or Lucide icons. These are not part of the link-ui stack.

---

## Execution Steps

### Step 1: Gather Setup Details

**IMPORTANT:** Before creating the prototype, ask the user for **three things**:

> "I need a few details to set up your prototype:
>
> 1. **Prototype name** — lowercase with hyphens (e.g., `insights-v2`, `sales-dashboard`, `monitor-redesign`). This will be used as the folder name and the repo entry name.
>
> 2. **Local repo path** — where is your local clone of [owi-link/design-prototypes](https://github.com/owi-link/design-prototypes)? (e.g., `~/design-prototypes`, `/Users/you/projects/design-prototypes`)
>
> 3. **Target directory** — where should the working prototype be created? Options:
>    - **Inside the repo** (default): `[REPO_PATH]/prototypes/[name]/` — ready to commit/push later
>    - **Standalone location**: Any path you prefer (e.g., `~/Desktop/Projects/[name]/`) — you can copy it into the repo later if needed"

Wait for user confirmation on all three before continuing.

**Variables used in remaining steps:**
- `[REPO_PATH]` — user's local clone of design-prototypes
- `[PROTOTYPE_NAME]` — the chosen prototype name
- `[TARGET_PATH]` — where the prototype is created (either `[REPO_PATH]/prototypes/[PROTOTYPE_NAME]` or a standalone path)

### Step 2: Choose Reference Pages

**IMPORTANT:** After gathering setup details, prompt the user to choose existing pages from the template as style/pattern references for the new prototype.

> "Before I set up the project, I'd like to align the look and feel of your prototype with existing pages.
>
> **Which existing pages should I use as references** for component patterns, layout structure, SCSS conventions, and design system usage?
>
> I'll scan the available pages in the template and list them for you."

**Action:** List the top-level page directories available in the template:

```bash
ls -1 "[REPO_PATH]/_liminal_template/src/pages/"
```

Present the list to the user and ask them to pick **one or more** pages. Common good references:
- **GamePlan/Detail** — Tabs, SectionCard compound component, sticky headers, SCSS with `$color-*` vars
- **Insights** — Card layouts, Badge/Chip usage, empty states
- **Monitor** — Feed layouts, filtering patterns
- **Discover** — Table/grid layouts, search patterns

Store the user's selections as `[REFERENCE_PAGES]` (e.g., `GamePlan/Detail`, `Insights`).

### Step 2b: Analyze Reference Pages

**Before writing any prototype code**, read and internalize the patterns from the selected reference pages. For each `[REFERENCE_PAGE]`:

1. **Read the main entry point** (`index.tsx`) — understand the page structure, imports, and wrapper pattern
2. **Read the SCSS file** (`styles.scss` or similar) — catalog the SCSS variables used (e.g., `$color-positive-*` not `$color-green-*`, `$color-notice-*` not `$color-yellow-*`, `$color-negative-*` not `$color-red-*`)
3. **Read key sub-components** — understand compound component patterns (e.g., `SectionCard` with `Header`, `Title`, `Subtitle`, `Divider`)
4. **Catalog the design system imports** — which `@owi-link/link-ds` components are used and how (Button variants, Chip props, Tabs structure)

**Build a reference checklist before writing code:**

| Pattern | Source | Notes |
|---------|--------|-------|
| Page wrapper class | `[REFERENCE_PAGE]/index.tsx` | e.g., `<div className="page-name">` + SCSS file |
| SCSS color variables | `[REFERENCE_PAGE]/styles.scss` | Use only variables from `src/styles/base/_colors.scss` |
| Card component | Identified sub-component | e.g., `SectionCard` compound component |
| Button variants | `@owi-link/link-ds` usage | e.g., `variant="primary"`, `variant="ghost-secondary"` |
| Tab pattern | `@owi-link/link-ds` Tabs | e.g., `Tabs/TabsList/TabsTrigger/TabsContent` |
| Breadcrumbs | `useBreadcrumbs()` hook | Navigation context |
| Loading states | `Skeleton` from primereact | Matching card structure |

**Critical — SCSS variable validation:** Before using any `$color-*` variable in SCSS, verify it exists in `[TARGET_PATH]/src/styles/base/_colors.scss`. The design system uses semantic names:
- Green/success = `$color-positive-*`
- Yellow/warning = `$color-notice-*`
- Red/error = `$color-negative-*`
- Blue/info = `$color-informative-*`
- **Do NOT use** `$color-green-*`, `$color-yellow-*`, `$color-red-*`, `$color-blue-*` — these do not exist and will cause Vite compilation errors that crash the page.

### Step 3: Copy Prototype Template

Copy the template to the target directory, excluding `node_modules/` (will be reinstalled):

```bash
rsync -a --exclude='node_modules' --exclude='.DS_Store' --exclude='pnpm-lock.yaml' "[REPO_PATH]/_liminal_template/" "[TARGET_PATH]/"
```

### Step 4: Install Dependencies

```bash
cd "[TARGET_PATH]"
pnpm install
```

**Prerequisite:** `GITHUB_TOKEN` must be set in the shell environment with `read:packages` scope. This is required to install `@owi-link/link-ds` and `@owi-link/link-data-viz` from the GitHub Packages registry.

If install fails with authentication errors, ask the user to verify their `GITHUB_TOKEN` is exported.

### Step 5: Start Development Server

```bash
pnpm dev
```

This starts the Vite dev server on `http://localhost:3000` with hot reload enabled.

### Step 6: Confirm to User

Once the server is running, inform the user:

> "Prototype is running at `http://localhost:3000`
>
> The app loads with the full link-ui shell (sidebar, header, navigation) using mock authentication as "Demo User".
>
> **Reference pages:** I've analyzed `[REFERENCE_PAGES]` and will follow their patterns for components, layout, SCSS variables, and design system usage when building new pages.
>
> **What's available:**
> - All design system components from `@owi-link/link-ds`
> - All existing link-ui components and pages
> - React Query, React Router, React Hook Form + Zod
> - Tailwind CSS with `tw-` prefix
>
> **To add a new page:** Create in `src/pages/YourFeature/`, then add a route in `src/hooks/routes/useAuthRoutes.ts`
>
> **GitHub:** This prototype lives locally at `[TARGET_PATH]`. When you're ready to push it to the repo, just ask."

---

## Pushing to GitHub

**NEVER push to GitHub automatically.** Only push when the user explicitly asks (e.g., "push this to the repo", "commit and push", "save to GitHub").

When the user requests a push:

1. If the prototype was created **inside the repo** (`[REPO_PATH]/prototypes/[PROTOTYPE_NAME]/`), stage and commit:
   ```bash
   cd [REPO_PATH]
   git add prototypes/[PROTOTYPE_NAME]/
   git commit -m "feat([PROTOTYPE_NAME]): <description from user or inferred from work>"
   ```

2. If the prototype was created at a **standalone location**, copy it into the repo first:
   ```bash
   rsync -a --exclude='node_modules' --exclude='.DS_Store' --exclude='.vite' --exclude='pnpm-lock.yaml' "[TARGET_PATH]/" "[REPO_PATH]/prototypes/[PROTOTYPE_NAME]/"
   cd [REPO_PATH]
   git add prototypes/[PROTOTYPE_NAME]/
   git commit -m "feat([PROTOTYPE_NAME]): <description from user or inferred from work>"
   ```

3. Push to main:
   ```bash
   git push origin main
   ```

4. Confirm the commit SHA and link to the user.

**Reminders:**
- Exclude `node_modules/`, `.vite/`, `.DS_Store` from commits (should be covered by `.gitignore`)
- Check `.env` files for real secrets before pushing — mock values are fine
- Use the repo's conventional commit format: `feat(<prototype>): <description>`

---

## Building on the Prototype

### Adding New Pages

1. **Follow the reference pages** selected in Step 2 — match their page wrapper, SCSS structure, component imports, and layout patterns
2. Create your page component in `src/pages/YourFeature/index.tsx`
3. Add a route entry in `src/hooks/routes/useAuthRoutes.ts`
4. The page will render inside the app shell with sidebar and header

### Using Design System Components

```tsx
import { Button, Input, DataTable, Badge, Tabs } from '@owi-link/link-ds';
```

All 37 components from `@owi-link/link-ds` are available: Button, Input, Textarea, Checkbox, Radio, Switch, Select, Combobox, DataTable, Table, Modal, Drawer, Tooltip, Panel, Popover, Tabs, Pagination, Avatar, Badge, Chip, Tag, Progress, Toast, and more.

### Using Existing link-ui Components

All components from the production app are available:

```tsx
import CompanyCard from 'components/CompanyCard';
import Loader from 'components/Loader';
```

### Mocking Page Data

For prototype pages that need data, either:
- Hardcode data inline in the component
- Create JSON files in `src/mocks/data/` and import them
- Create mock hooks that return static data

### Styling Conventions

- **Follow reference page patterns first** — use the same SCSS structure, class naming (BEM), and component composition as the pages selected in Step 2
- **SCSS color variables** — only use variables defined in `src/styles/base/_colors.scss`:
  - `$color-positive-*` (green/success), `$color-notice-*` (yellow/warning), `$color-negative-*` (red/error), `$color-informative-*` (blue/info)
  - `$color-gray-*`, `$color-primary-*`, `$color-purple-*`, `$color-teal-*`
  - **Never use** `$color-green-*`, `$color-yellow-*`, `$color-red-*`, `$color-blue-*` — they don't exist and cause Vite crashes
- **Tailwind CSS with `tw-` prefix** for utility classes:
  ```tsx
  <div className="tw-flex tw-flex-col tw-gap-4 tw-rounded-lg tw-bg-white tw-p-4">
  ```
- **clsx** for conditional className composition:
  ```tsx
  import clsx from 'clsx';
  <div className={clsx('tw-flex tw-gap-4', { 'tw-hidden': !isVisible })} />
  ```
- **Never use inline `style={}` props** (only exception: dynamic CSS custom properties)
- **Tabler Icons** via webfont (`ti ti-icon-name`) or React (`@tabler/icons-react`)

### Path Aliases

These path aliases are configured in `vite.config.ts` and `tsconfig.json`:

`components/*`, `contexts/*`, `hooks/*`, `pages/*`, `types/*`, `utils/*`, `lib/*`, `assets/*`

### Key Directories

| Folder | Purpose |
|--------|---------|
| `src/pages/` | Route-level page components |
| `src/components/` | Shared React components |
| `src/components/__ds__/` | Design system wrappers |
| `src/hooks/` | Domain-organized React Query hooks |
| `src/contexts/` | React context providers (3 are mocked) |
| `src/types/` | Shared TypeScript type definitions |
| `src/utils/` | Utility functions |
| `src/lib/api.ts` | API client singleton |
| `src/assets/` | Global styles, variables, images |
| `src/routes/` | Route configuration |

---

## Mock Providers Reference

The prototype has 3 context providers replaced with mocks. If you need to customize the mock user or behavior, edit these files:

| File | What It Mocks |
|------|---------------|
| `src/contexts/Auth0Context.tsx` | Authentication — always returns `isAuthenticated: true` with mock user |
| `src/contexts/UserContext.tsx` | User profile — Provider role, Liminal Demo org, premium account |
| `src/contexts/FeatureTogglesContext.tsx` | Feature flags — `isFeatureEnabled()` always returns `true` |

To change the mock user's role (e.g., to test admin views), edit `src/contexts/UserContext.tsx` and change `role: ['Provider']` to `role: ['Internal Admin']`.

---

## Optional: Sharing Prototypes via Vercel

When the design is ready for stakeholder review, deploy to Vercel for a shareable URL.

**Vercel Account:** Use the team or personal Vercel account configured for the user.

### Prerequisites

Create a `vercel.json` in the project root:

```json
{
  "buildCommand": "pnpm build",
  "outputDirectory": "build"
}
```

### Deployment Steps

1. Navigate to the project directory:
   ```bash
   cd "[TARGET_PATH]"
   ```

2. Deploy to Vercel:
   ```bash
   npx vercel --prod --yes
   ```

3. Share the generated URL (e.g., `https://liminal-[project-name].vercel.app`)

### First-Time Setup

If deploying a new project for the first time and need to link to a specific account:

```bash
npx vercel logout
npx vercel login
npx vercel --prod --yes --name [project-name]
```

### Notes

- This step is optional and only needed when sharing designs externally
- Each deployment creates a new URL; use `--prod` to update the production alias
- Vercel requires project names to be lowercase with no spaces

---

## Permissions Required

- **Network:** Required for `pnpm install` and dev server
- **All:** May be required if sandbox restrictions prevent pnpm operations

---

## Related Rules

- `rule-mosaic-guidelines-2026.md` - Liminal design token values (colors, spacing scale, typography)
- `globals.css` - CSS custom properties and design tokens

---

## Maintaining the Template

The Prototype Template lives in the [owi-link/design-prototypes](https://github.com/owi-link/design-prototypes) repo at `_liminal_template/`.

**To pull the latest template:**
```bash
cd [REPO_PATH] && git pull origin main
```

**Update the template when:**
- **link-ui updates its design system** (`@owi-link/link-ds` version bump) — re-copy from link-ui and re-apply mock providers
- **New shared components are added** to link-ui that prototypes should access
- **The mock user shape changes** due to UserData type changes

To refresh the template, re-run the original scaffolding process: copy link-ui app files, replace the 3 context providers with mocks, apply the same edits to App.tsx/routes/vite.config.ts/package.json, install dependencies, then commit and push to the [owi-link/design-prototypes](https://github.com/owi-link/design-prototypes) repo.
