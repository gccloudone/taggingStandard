# Cloud Tagging Standard (WIP)

> ⚠️ **Work in Progress – Not Official**  
> This repository contains a **draft** tagging standard and supporting tooling.  
> It is **not yet an approved or official standard**.  
> Tag names, definitions, scopes, and requirements are subject to change through discussion and governance review.

## Overview

This repository contains:

- A **draft cloud tagging standard**, defined in a single YAML file (`tags.yaml`)
- Simple **static HTML pages** that render the YAML into a human‑readable catalogue
- Lightweight tooling intended to support **discussion, iteration, and validation** of a tagging approach before formal adoption

The goal is to make tag definitions:

- Easy to review
- Easy to iterate on
- Easy to consume by both humans and automation

## Why a Tagging Standard?

Consistent tags and labels are foundational to effective cloud governance and operations. A clearly defined tagging standard enables:

- **Cost allocation & chargeback**  
    Attribute cloud spend to departments, applications, and environments.

- **Security & compliance**  
    Identify data sensitivity, audience, and regulatory requirements.

- **Operational management**  
    Drive backups, power policies, monitoring, and lifecycle automation.

- **Inventory & traceability**  
    Connect cloud resources back to business context such as applications and owners.

Without a shared standard, organizations tend to accumulate:

- Duplicate or overlapping tags
- Inconsistent naming and formats
- Gaps that limit horizontal or aligned automation and reporting

## Tag Categories

Each tag in `tags.yaml` is assigned a **status** that reflects its maturity and adoption expectations.

### Mandatory

- **Required for all adopters of the standard**
- Must be applied where the tag’s scope is applicable
- Deviations or exceptions require an **official waiver**
- Designed to support core governance, compliance, and billing needs

Examples:

- Environment
- Data classification
- Enterprise identifiers used for cost allocation

### Recommended

- **Optional, but strongly advised**
- Intended to cover common operational and business needs
- Should be used **instead of creating bespoke tags** for the same purpose
- Consumers should avoid duplicating these tags under different names or formats

Recommended tags may become mandatory in future revisions.

### Under Consideration

- **Proposed but not finalized**
- Included to promote discussion and early feedback
- Definitions, formats, or even inclusion may change
- Should not yet be treated as stable or enforceable

These tags highlight areas where additional governance or alignment is needed.

## YAML Structure

All tag definitions live in a single file:  
`tags.yaml`

### High‑Level Structure

```yaml
tags:
  - key: envr
    status: mandatory
    description: Which SDLC environment the workload runs in
    rationale: Enables policy scoping and cost allocation
    source_hierarchy_target: Environment
    format: string(lowercase)
    sample:
      key: envr
      value: prod
```

### Field Definitions

Each tag entry includes:

- **`key`**  
    The exact tag/label name to be applied to resources.

- **`status`**  
    One of:
    - `mandatory`
    - `recommended`
    - `consider` (rendered as “Under consideration”)

- **`description`**  
    What the tag represents.

- **`rationale`**  
    Why the tag exists and what capability it supports.

- **`source_hierarchy_target`**  
    Indicates where the tag originates or is best applied  
    (e.g., environment, application/workload, resource).

- **`format`**  
    Expected value type, casing, or enumeration.

- **`sample`**  
    Example key/value pair for clarity and consistency.

## HTML Catalogue Pages

Two static HTML files are included to render the YAML into tables in a browser.

### `tagsDev.html` — Development / Exploration View

- Loads `tags.yaml` automatically (when served over HTTP)
- Includes:
    - Inline YAML editor (fallback)
    - File upload option for alternate YAML files
- Intended for:
    - Iterating on tag definitions
    - Testing changes locally
    - Reviewing draft proposals


### `tags.html` — Read‑Only Catalogue View (can be printed to PDF)

- Always loads `tags.yaml`
- No editor or file upload
- Intended for:
    - Simple viewing
    - Sharing a clean, consistent catalogue
    - Demonstrations or reviews

## Running Locally

Because browsers block fetching local files via `file://`, these pages must be served over HTTP.

### Option 1: Python (recommended)

From the repository root:

```bash
python3 -m http.server 8080
```

Then open:

- <http://localhost:8080/tags.html>
- <http://localhost:8080/tagsDev.html>

### Option 2: Node / npm

If you have Node.js installed:

```bash
npx serve .
```

or, using http-server:

```bash
npm install -g http-server
http-server -p 8080
```

Then open the same URLs as above.

## Intended Use Cases

This repository is intended to support:

- Early development of a cloud tagging strategy
- Cross‑team review and discussion
- Validation of tag definitions before enforcement
- Visual inspection of YAML‑based standards
- Lightweight documentation without build tooling

It is **not**:

- A final policy document
- An enforcement engine
- A production‑ready governance solution

## Contributing & Next Steps

Contributions are expected while this is in draft form, including:

- Refining definitions and rationales
- Identifying gaps or overlaps
- Promoting “Under Consideration” tags to Recommended or Mandatory
- Aligning formats and naming conventions

Formal governance, versioning, and enforcement decisions are out of scope for this repository **until the standard is finalized**.

## Disclaimer

All content in this repository is provided **as‑is** for discussion purposes only.  
Adoption prior to formal approval is at the adopter’s own risk.
