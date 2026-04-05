# FinFlow — Finance Dashboard

A clean, interactive finance dashboard built with **React 18**, **Chart.js 4**, and **Tailwind CSS** — all delivered as a single self-contained HTML file with no build step required.

---

## Quick Start

1. Unzip the archive
2. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
3. No server, no npm, no build step needed — it just works

> **Note:** The app persists data to `localStorage`. Your transactions and role preference survive page refreshes.

---

## Features

### Dashboard Overview
- **4 Summary Cards** — Total Balance, Total Income, Total Expenses, Savings Rate
- **Income vs Expenses Line Chart** — monthly trend from January to June 2025 (Chart.js)
- **Spending Breakdown Doughnut Chart** — top expense categories with percentages
- **Recent Transactions** — last 5 entries with quick-glance amounts

### Transactions Page
- **Search** — live filter by description or category keyword
- **Filter** — by type (income/expense), category, and month
- **Sort** — click any column header (Date, Description, Amount) to toggle asc/desc
- **Export CSV** — downloads filtered transactions as a CSV file
- **Export JSON** — downloads filtered transactions as a JSON file
- **Add Transaction** (Admin only) — modal with type toggle, amount, date, category
- **Edit Transaction** (Admin only) — inline edit modal pre-filled with existing values
- **Delete Transaction** (Admin only) — confirmation prompt before deletion

### Role-Based UI
Switch roles via the dropdown in the top-right header:

| Feature           | Admin | Viewer |
|-------------------|-------|--------|
| View all data     | ✅    | ✅     |
| Add transactions  | ✅    | ❌     |
| Edit transactions | ✅    | ❌     |
| Delete entries    | ✅    | ❌     |
| Export data       | ✅    | ✅     |

### Insights Page
- **Top Expense Category** — ranked by total spend with percentage share
- **Best Savings Month** — month with highest net (income − expenses)
- **Monthly Averages** — average income and expense across the 6-month period
- **Smart Tip** — context-aware financial observation
- **Monthly Performance Bars** — dual progress bars showing income vs expense per month
- **Category Ranking** — all categories ranked with color-coded progress bars

---

## Tech Stack

| Technology       | Purpose                             | Delivery  |
|------------------|-------------------------------------|-----------|
| React 18         | UI components and state management  | CDN (unpkg)|
| ReactDOM 18      | DOM rendering                       | CDN (unpkg)|
| Babel Standalone | JSX transpilation in the browser    | CDN (unpkg)|
| Chart.js 4       | Line chart and doughnut chart       | CDN (jsDelivr)|
| Tailwind CSS     | Utility classes (Play CDN)          | CDN       |
| Google Fonts     | Sora + JetBrains Mono               | CDN       |

---

## Architecture & State Management

The app uses **React Context API** for global state — no external library needed.

```
AppProvider (Context)
├── transactions[]          ← persisted to localStorage
├── role: 'admin'|'viewer'  ← persisted to localStorage
├── page: string            ← current active page
├── filters: object         ← search, type, category, month, sort
├── addTx / updateTx / deleteTx  ← CRUD actions
└── summary: { income, expense, balance, savingsRate }  ← memoized

App
├── Sidebar              ← navigation + logo
├── Header               ← page title + role switcher
└── Pages (conditional render)
    ├── DashboardPage    ← cards + charts + recent transactions
    ├── TransactionsPage ← filterable/sortable table + CRUD modal
    └── InsightsPage     ← analytics, breakdowns, monthly comparison
```

All derived values (`filtered`, `summary`, `getCatBreakdown`, `getMonthlyData`) use `useMemo` to avoid unnecessary recalculations.

---

## Mock Data

48 realistic transactions across 6 months (Jan–Jun 2025) covering:
- **Income:** Salary (₹75K/month), Freelance projects, Investment returns, Annual bonus
- **Expenses:** Housing (rent), Food & Dining, Transport, Utilities, Shopping, Entertainment, Healthcare, Education

Total dataset: ₹5.5L+ income, covering a typical salaried professional in India.

---

## Responsiveness

| Breakpoint | Behavior |
|------------|----------|
| ≥ 900px    | Sidebar fixed on left, full 4-column card grid, side-by-side charts |
| < 900px    | Sidebar slides in as drawer (hamburger menu), charts stack vertically, table collapses to 3 columns |
| < 560px    | Cards go to single column, modal uses compact padding |

---

## Data Persistence

- Transactions are saved to `localStorage` key `ff_txs` on every change
- Role preference saved to `ff_role`
- Refresh the page — your data is still there
- To reset: use browser DevTools → Application → Local Storage → Delete keys, then reload

---

## Optional Enhancements Implemented

- ✅ Data persistence (localStorage)
- ✅ Export functionality (CSV + JSON)
- ✅ Dark mode (always-on luxury dark theme)
- ✅ Animations (page transitions, card hover lifts, modal slide-up)
- ✅ Advanced filtering (multi-filter + search + month picker)
- ✅ Role-based UI simulation

---

## Design Decisions

- **Dark luxury aesthetic** — deep `#080a0f` background with `#f5a623` gold accent, emerald for income, rose for expenses
- **Typography** — Sora (clean geometric sans) for UI, JetBrains Mono for all monetary values to ensure alignment
- **Color semantics** — green always means positive/income, red always means expense/negative — consistent throughout
- **No external UI library** — all components hand-crafted in CSS for full control over aesthetics
- **Single file** — intentional for portability; the code is structured in 15 clearly labeled sections to demonstrate modularity

---

## File Structure

```
finance-dashboard/
├── index.html    ← Complete app (all JS, CSS, and HTML in one file)
└── README.md     ← This file
```

The `index.html` is internally organized into 15 sections:

```
Section 1  — Constants & Mock Data
Section 2  — Utility Functions (formatting, export, aggregation)
Section 3  — State Management (React Context + useReducer pattern)
Section 4  — Icon System (inline SVG paths)
Section 5  — Sidebar Component
Section 6  — Header Component
Section 7  — Summary Card Component
Section 8  — Balance Trend Chart (Chart.js Line)
Section 9  — Spending Breakdown Chart (Chart.js Doughnut)
Section 10 — Dashboard Page
Section 11 — Transaction Modal (Add/Edit)
Section 12 — Transactions Page (Table + Filters + CRUD)
Section 13 — Insights Page (Analytics + Rankings)
Section 14 — Root App Component
Section 15 — ReactDOM Mount
```

---

*Built for evaluation purposes. All data is mock/static. No backend dependency.*
