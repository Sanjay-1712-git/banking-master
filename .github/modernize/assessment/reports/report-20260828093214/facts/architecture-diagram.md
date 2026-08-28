# Architecture Diagram

LinuxBanking is a single page React application built with TypeScript and Vite. The application is entirely client-side, with page components handling navigation, display logic, and lightweight in-browser state.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Web Browser"]
    end
    subgraph AppLayer["Frontend Application - React 18 and Vite"]
        Router["React Router"]
        Shell["App Shell Header Sidebar Footer"]
        Pages["Page Components"]
        UIState["React Local State"]
        Assets["CSS and Image Assets"]
    end
    subgraph External["External Services"]
        CurrencyAPI["AwesomeAPI Currency API"]
        StaticImages["External GNU Image Assets"]
    end
    subgraph Build["Build Tooling"]
        TypeScript["TypeScript Compiler"]
        Vite["Vite Bundler"]
    end

    Browser -->|"loads static app"| Shell
    Shell -->|"routes paths"| Router
    Router -->|"renders"| Pages
    Pages -->|"stores form and display state"| UIState
    Pages -->|"uses"| Assets
    Pages -->|"fetches exchange rates"| CurrencyAPI
    Pages -->|"loads remote images"| StaticImages
    TypeScript -->|"compiles"| Vite
    Vite -->|"emits static assets"| Browser
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---:|---:|---|
| Presentation | React | 18.2.0 | Component based browser UI |
| Routing | React Router DOM | 6.4.0 | Client side route matching and page rendering |
| Language | TypeScript | 4.8.3 locked, 4.6.4 declared | Static typing and JSX compilation |
| Build | Vite | 3.2.7 locked, 3.1.0 declared | Development server and production bundle generation |
| Styling | CSS modules by folder convention | N/A | Page and component styling |

### Data Storage & External Services

No database, cache, message broker, or server-side data store is declared in the repository. Runtime data is kept in React component state, with the home page retrieving USD and EUR exchange rates directly from the AwesomeAPI public currency API and several pages loading remote GNU image assets by URL.

### Key Architectural Decisions

- Implements a static single page application with browser-side routing rather than a backend API layer.
- Keeps banking demo state such as balances, login inputs, signup inputs, and transaction amounts in local React component state only.
- Uses direct browser navigation through anchors and `window.location.href` for several flows instead of centralized navigation helpers.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation["Presentation"]
        AppShell["App"]
        HomePage["Home"]
        SigninPage["Signin"]
        SignupPage["Signup"]
        DashboardPage["Dashboard"]
        WithdrawPage["Withdraw"]
        ExtractPage["Extract Page"]
        FinancesPage["Finances"]
        AboutPage["About"]
        NotFoundPage["NotFound"]
        SuccessPage["SuccessTransaction"]
        ExtractItem["ExtractItem"]
    end
    subgraph Navigation["Routing"]
        BrowserRouter["BrowserRouter"]
        Routes["Routes"]
    end
    subgraph State["Local State"]
        FormState["Form Inputs"]
        BalanceState["Balance Visibility"]
        CurrencyState["Exchange Rates"]
    end
    subgraph ExternalCalls["External Calls"]
        CurrencyService["Currency API"]
    end

    BrowserRouter -->|"wraps"| AppShell
    AppShell -->|"declares"| Routes
    Routes -->|"renders"| HomePage
    Routes -->|"renders"| SigninPage
    Routes -->|"renders"| SignupPage
    Routes -->|"renders"| DashboardPage
    Routes -->|"renders"| WithdrawPage
    Routes -->|"renders"| ExtractPage
    Routes -->|"renders"| FinancesPage
    Routes -->|"renders"| AboutPage
    Routes -->|"renders"| NotFoundPage
    Routes -->|"renders"| SuccessPage
    ExtractPage -->|"composes"| ExtractItem
    HomePage -->|"updates"| CurrencyState
    SignupPage -->|"updates"| FormState
    SigninPage -->|"updates"| FormState
    DashboardPage -->|"updates"| BalanceState
    WithdrawPage -->|"updates"| FormState
    FinancesPage -->|"updates"| FormState
    HomePage -->|"fetches"| CurrencyService
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| App | Presentation | React component and route shell | Provides shared header, sidebar, footer, and client route declarations |
| Home | Presentation | React page | Displays landing content and current currency exchange rates |
| Signup | Presentation | React page | Collects user registration fields and displays a temporary confirmation |
| Signin | Presentation | React page | Collects login inputs and navigates to the dashboard when both fields are populated |
| Dashboard | Presentation | React page | Displays the mock account balance and navigation to statements, withdrawals, deposits, and financing |
| Withdraw | Presentation | React page | Lets users choose withdrawal or deposit mode and submit a mock transaction |
| Extract Page | Presentation | React page | Displays fixed statement rows using the reusable ExtractItem component |
| ExtractItem | Presentation | React component | Renders one statement row with invoice metadata and a download link |
| Finances | Presentation | React page | Simulates financing interest at a fixed percentage |
| SuccessTransaction | Presentation | React page | Displays transaction success and redirects back to the dashboard |
| About | Presentation | React page | Presents static project and Linux related information |
| NotFound | Presentation | React page | Displays a not found page and redirects to home |
