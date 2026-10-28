# JAPA Global — Annual Supplier Purchases Tracker 2026
**System Architecture Blueprint & Antigravity IDE Implementation Prompt**  
*Creator/Owner:* Gain Carlo Cayabyab  
*Project:* Japa Global Annual Supplier Purchases Tracker 2026 (`21.03_Japa_Global_Annual_Supplier_Purchases_Tracker 2026 - System`)

---

## Part 1: Full System Plan & Technical Blueprint

### 1. Executive Summary & Core Objectives
The objective is to transform a standard OneDrive Excel spreadsheet tracking 116 suppliers into a fast, mobile-responsive web dashboard at **$0 cost**. 

The system directly fetches and auto-cleans live OneDrive spreadsheet data, eliminating the need for manual row-by-row Excel formatting while providing real-time financial insights, search capabilities, and payment alerts.

---

### 2. High-Level Metrics & Key Data Points
* **Total Vendors Tracked:** 116 Suppliers (`SUP-001` through `SUP-116`)
* **Total Annual Spend (2026):** $\text{PHP } 6,061,517.24$
* **Total Paid to Date:** $\text{PHP } 4,922,401.06$
* **Total Outstanding Balance:** $\text{PHP } 419,275.18$
* **Key Outstanding Vendors:**
  1. **Xarion Industries (`SUP-004`):** $\text{PHP } 286,422.68$ (Printing Consumables & Inks | 30 Days)
  2. **Manchester Textile Marketing (`SUP-002`):** $\text{PHP } 120,000.00$ (Fabrics & Sewing Materials | 30 Days)
  3. **Genesis (`SUP-006`):** $\text{PHP } 12,852.50$ (Plain Shirts | 60 Days)

---

### 3. Data Resiliency & Smart Auto-Cleaning Pipeline
Rather than fixing raw Excel errors manually, the frontend JS pipeline automatically cleans data on load using the following rules:

1. **Header Detection:** Data rows are identified by checking if Column 0 begins with `SUP-`. Footer totals and non-supplier rows are automatically filtered out.
2. **Currency Sanitization:** Regex cleans non-numeric symbols, handling character encoding bugs (such as `?` or missing `₱` symbols):
   $$\text{Clean Value} = \text{parseFloat}(\text{String}(v).\text{replace}(/[^\d.-]/g, '')) \parallel 0.0$$
3. **Dynamic Formula Calculation:**
   $$\text{Outstanding Balance} = \max(0, \text{Total Purchases} - \text{Total Paid})$$
   $$\text{Overall Status} = \begin{cases} \text{"Terms / Pending"}, & \text{if } \text{Outstanding Balance} > 0 \\ \text{"Up to Date"}, & \text{otherwise} \end{cases}$$
4. **Offline Fallback Caching:** Parsed JSON data is stored in `localStorage` to ensure instant loading even if the OneDrive network fetch fails.

---

### 4. Technical Architecture & Tech Stack ($0 Cost)
* **IDE / Development:** Antigravity IDE
* **Frontend UI:** HTML5 + Tailwind CSS (via CDN) + Lucide Icons (CDN)
* **Parsing Engine:** PapaParse JS (`xlsx` / CSV parser)
* **Data Visualization:** Chart.js (Interactive Category Spend Doughnut Chart)
* **Hosting Platform:** Netlify Drop / GitHub Pages ($0 Forever)

---

## Part 2: Master Prompt for Antigravity IDE

*Copy and paste the entire block below into **Antigravity IDE** to start building your application:*

```text
You are an expert full-stack web developer building a modern, light-themed, single-file web dashboard for "JAPA Global Annual Supplier Purchases Tracker 2026".

### CORE PROJECT GOAL
Create a single self-contained `index.html` web application with embedded Tailwind CSS (CDN), Lucide Icons, PapaParse, and Chart.js. The web app must fetch CSV/Excel data live from a OneDrive link, auto-clean raw formatting errors, display summary KPI cards, render interactive charts, highlight overdue balances, and provide real-time search and filtering across all 116 suppliers.

### LIVE DATA SOURCE
- Default CSV Fetch URL: "https://1drv.ms/x/c/b750e9ddb4b03ccf/IQBOPBrUVbipSrm0mYI9GxLaAT6NpZPzqLyd7HVYrNjTtxc?e=ml78jA&download=1"
- Provide an easily customizable input modal or configuration variable `ONEDRIVE_CSV_URL` in JS to update the direct CSV link anytime.

### SYSTEM SPECIFICATIONS & UI LAYOUT

1. **Header & Brand Section:**
   - Title: "JAPA Global — Annual Supplier Purchases Tracker 2026"
   - Subtitle: "Real-time Vendor Spend, Payments & Pending Balances Dashboard"
   - Action Buttons: "Refresh Data", "Export CSV", "Settings / Link Config".

2. **Top Metric Summary Cards (4 KPIs):**
   - Total Suppliers (Count of valid rows starting with SUP-)
   - Total Annual Purchases (Formatted in PHP ₱)
   - Total Amount Paid (Formatted in PHP ₱)
   - Total Outstanding Balance (Formatted in PHP ₱, color-coded red if > 0)

3. **Pending Balances Alert Banner:**
   - Automatically filter and display top pending suppliers (e.g., Xarion Industries, Manchester Textile, Genesis) with high balances in an actionable warning box with a quick "View Details" action.

4. **Analytics & Spend Breakdown Section:**
   - A modern Chart.js Doughnut Chart displaying "Spend Distribution by Primary Category" (Fabrics & Sewing Materials, Printing Consumable & Inks, Plain Shirts, Print Outsource, Others).
   - A progress bar showing Overall Collection / Payment Percentage (Paid vs Outstanding).

5. **Search & Filter Controls:**
   - Search bar: Real-time search by Supplier Name, Supplier ID (e.g., SUP-004), or PO Ref.
   - Category Filter: Dropdown to filter by category.
   - Status Filter: Dropdown filter for "All", "Terms / Pending", or "Up to Date".

6. **Interactive Data Table:**
   - Columns: Supplier ID, Supplier Name, Category, Payment Terms, Total Purchases, Total Paid, Outstanding Balance, Status, Actions (View OneDrive Ledger).
   - Features: Sortable headers, visual status badges (Green for "Up to Date", Amber/Red for "Terms / Pending"), responsive table wrapper.

7. **Data Parsing & Auto-Cleaning Logic:**
   - Read CSV lines with PapaParse.
   - Filter rows where Column 0 starts with `SUP-`.
   - Strip out encoding artifacts (`?`, `₱`, commas) and convert financial fields to float.
   - Auto-calculate: Balance = Purchases - Paid.
   - Auto-assign: Status = Balance > 0 ? "Terms / Pending" : "Up to Date".
   - Cache cleaned output in `localStorage` for offline fallback.

Generate a completely clean, responsive, bug-free, single-file HTML/JS application ready for instant browser testing and Netlify deployment.
```

---

## Part 3: Step-by-Step Execution Plan

1. **Open Antigravity IDE:** Create a new workspace folder named `japa-supplier-dashboard`.
2. **Paste Prompt:** Paste the **Master Prompt for Antigravity IDE** from Part 2 into the AI chat window.
3. **Save Code:** Save the generated output as `index.html`.
4. **Preview:** Open `index.html` directly in your browser or run a simple local web server (`python -m http.server 8000`).
5. **Deploy for Free:** Drag and drop your project folder onto [Netlify Drop](https://app.netlify.com/drop) to publish your live system on a `.netlify.app` domain.