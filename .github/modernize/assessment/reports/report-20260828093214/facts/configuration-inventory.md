# Configuration & Externalized Settings Inventory

The repository has a small frontend configuration surface consisting of npm package metadata, TypeScript compiler settings, and a Vite configuration file. No environment-specific configuration files, secret stores, or deployment manifests were detected.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| package metadata | npm package manifest | `package.json` | Defines scripts, runtime dependencies, and dev dependencies |
| package lock | npm lockfile | `package-lock.json` | Pins resolved npm dependency versions |
| yarn lock | Yarn lockfile | `yarn.lock` | Alternate lockfile present, creating potential package manager drift |
| TypeScript config | compiler configuration | `tsconfig.json`, `tsconfig.node.json` | Configures TypeScript checking for app and Vite config |
| Vite config | build tool configuration | `vite.config.ts` | Enables the React plugin for Vite |
| HTML entry point | static entry template | `index.html` | Loads the Vite module entrypoint |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies or Plugins |
|---|---|---|---|
| development server | `npm run dev` | Starts Vite local development server | Vite, Vite React plugin |
| production build | `npm run build` | Runs TypeScript checking and Vite production bundling | TypeScript, Vite, Vite React plugin |
| preview | `npm run preview` | Serves the built static bundle locally | Vite preview server |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| default browser runtime | Loading built SPA or running Vite dev server | `index.html`, bundled source files | No runtime profile-specific overrides detected |

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `scripts.dev` | `vite` | all | `package.json` |
| `scripts.build` | `tsc && vite build` | all | `package.json` |
| `scripts.preview` | `vite preview` | all | `package.json` |
| `type` | `module` | all | `package.json` |
| `compilerOptions.target` | `ESNext` | all | `tsconfig.json` |
| `compilerOptions.jsx` | `react-jsx` | all | `tsconfig.json` |
| `compilerOptions.strict` | `true` | all | `tsconfig.json` |
| `vite.plugins` | React plugin | all | `vite.config.ts` |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| linuxbanking frontend development server | Node.js process started by `npm run dev`; no custom Node options detected | Not specified | 1 local process by default |
| linuxbanking frontend production bundle | Static assets emitted by `npm run build`; hosting runtime not defined in repository | Not specified | Not specified |

## Startup Dependency Chain

1. Install npm dependencies with the selected package manager.
2. For development, run the Vite development server; no service readiness dependencies are configured.
3. For production, run `npm run build` and deploy the generated static assets to a host outside the repository scope.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| None detected | N/A | N/A |

### Secrets Provisioning Workflow

No secrets provisioning workflow is present. The application does not include environment variables, secret references, cloud secret store integration, deployment manifests, or CI configuration that binds secrets to runtime services.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| None detected | N/A | N/A |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---:|---|
| React | 18.2.0 | `package-lock.json` |
| React DOM | 18.2.0 | `package-lock.json` |
| React Router DOM | 6.4.0 | `package-lock.json` |
| TypeScript | 4.8.3 locked, 4.6.4 declared | `package-lock.json`, `package.json` |
| Vite | 3.2.7 locked, 3.1.0 declared | `package-lock.json`, `package.json` |
| Vite React plugin | 2.1.0 | `package.json`, `package-lock.json` |
| Node.js used for assessment | 22.23.2 | local execution environment |
| npm used for assessment | 10.9.8 | local execution environment |
