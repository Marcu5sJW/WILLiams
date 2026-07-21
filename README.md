# Will Tracking & Asset Distribution App

## Overview
This project is a **Python-based application** (potentially using **Flask**) designed to help track and clearly present the distribution of a will. It is tailored for a user who is financially knowledgeable but not highly technical, prioritising **clarity, simplicity, and ease of updates**.

The application will provide a **clean, user-friendly interface** that visually breaks down assets, allocations, and estimated taxes. Data will be managed through a **spreadsheet (e.g., CSV or Excel)**, allowing simple updates without interacting directly with code.

---

## Goals
- Provide a **clear breakdown of total assets (~£3,000,000)**
- Show **who receives what** in an easy-to-understand format
- Estimate and display **tax implications**
- Allow **simple updates via spreadsheet**
- Keep the UI **minimal, clean, and accessible**

---

## Key Requirements

### 1. User Interface (UI)
- Clean, simple dashboard
- Large, readable numbers and labels
- Sections:
  - Total Assets
  - Distribution Breakdown
  - Individual Allocations
  - Tax Estimates
- Visual aids:
  - Pie charts for distribution
  - Tables for detailed breakdowns

---

### 2. Asset Distribution Logic

#### Total Estate
- Approximate value: **£3,000,000**

#### Allocation Rules
- **3 Children** → each receives **1/4 (25%)**
- **Remaining 1/4 (25%)** → split among **9 grandchildren**

#### Example Breakdown

| Group          | Share (%) | Total Amount (£) | Per Person (£) |
|----------------|----------|------------------|----------------|
| Child 1        | 25%      | £750,000         | £750,000       |
| Child 2        | 25%      | £750,000         | £750,000       |
| Child 3        | 25%      | £750,000         | £750,000       |
| Grandchildren  | 25%      | £750,000         | £83,333 each   |

---

### 3. Tax Considerations
- Include **basic inheritance tax estimation**
- UK inheritance tax (example rules):
  - 40% tax above threshold (e.g., £325,000, subject to change)
- Display:
  - Gross estate value
  - Taxable amount
  - Estimated tax
  - Net distribution

---

### 4. Data Source (Spreadsheet Integration)

#### File Format
- CSV or Excel (`.xlsx`)

#### Example Structure

| Name          | Category        | Share (%) | Notes          |
|---------------|----------------|-----------|----------------|
| Child 1       | Child          | 25        |                |
| Child 2       | Child          | 25        |                |
| Child 3       | Child          | 25        |                |
| Grandchild 1  | Grandchild     | 2.78      |                |
| ...           | ...            | ...       |                |

#### Features
- App reads spreadsheet on load
- Changes to file automatically reflected in UI
- Optional: “Refresh Data” button

---

### 5. Backend (Python + Flask)

#### Suggested Structure