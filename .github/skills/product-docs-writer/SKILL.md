---
name: product-docs-writer
description: "Use when: creating Product Documentation (Product Overview, Technical Docs, API Docs, Release Notes) — select appropriate template, gather context, generate structured documentation."
compatibility: vscode
metadata:
  tools: mcp-atlassian, semantic_search, confluence_search, jira_search
  workflow: product-management
  related_skills: atlassian-ops, prd-writer
license: MIT
---

# Product Documentation Writer Skill

Automated workflow untuk membuat Product Documentation yang comprehensive dan professional dengan 4 jenis: Product Overview, Technical Documentation, API Documentation, dan Release Notes.

## What I do

- Identify documentation type based on user request
- Search existing documentation untuk understand patterns
- Select appropriate template dari `/templates`
- Generate documentation draft dengan struktur yang konsisten
- Validate completeness dengan checklist
- Save draft to `/output` folder (READ-ONLY mode)

## When to use me

Invoke skill ini ketika user meminta:

**Product Overview:**
- "Bikin product overview untuk [service]"
- "Generate product documentation untuk [feature]"
- "Draft product overview: [description]"
- "Dokumentasi produk untuk [initiative]"

**Technical Documentation:**
- "Bikin technical docs untuk [service]"
- "Generate architecture documentation untuk [system]"
- "Draft technical documentation: [description]"
- "Dokumentasi teknis untuk [infrastructure]"

**API Documentation:**
- "Bikin API docs untuk [endpoint]"
- "Generate API documentation untuk [service]"
- "Draft API reference: [description]"
- "Dokumentasi API untuk [integration]"

**Release Notes:**
- "Bikin release notes untuk v[version]"
- "Generate changelog untuk [release]"
- "Draft release notes: [version] [description]"
- "Dokumentasi rilis untuk [version]"

## Workflow

### 1. **Discovery & Documentation Type Identification**

**Objective**: Understand documentation type dan gather relevant context

**Steps**:
```
a. Identify documentation type from user request
   - Product Overview: High-level product description, use cases, business impact
   - Technical Documentation: Architecture, infrastructure, data flow
   - API Documentation: Endpoints, schemas, authentication
   - Release Notes: Version history, changelog, migration guide

b. Search existing documentation (optional)
   - Use confluence_search untuk find similar docs
   - Analyze structure dan detail level
   - Extract common patterns
   
c. Ask clarifying questions (if needed)
   - Product/Service name
   - Target audience (users, developers, stakeholders)
   - Key features/changes to document
   - Version number (for release notes)
```

**Tools**: `confluence_search`, `jira_search`, `vscode_askQuestions`

---

### 2. **Template Selection**

**Objective**: Select appropriate template based on documentation type

**Template Mapping**:

| Documentation Type | Template File | Use Case |
|---|---|---|
| **Product Overview** | `templates/product-overview-template.md` | What product does, who uses it, business impact |
| **Technical Documentation** | `templates/technical-documentation-template.md` | Architecture, data flow, infrastructure details |
| **API Documentation** | `templates/api-documentation-template.md` | API endpoints, schemas, authentication, SLA |
| **Release Notes** | `templates/release-notes-template.md` | Version history, changelog, migration guide |

**Selection Logic**:
- Keywords "product", "overview", "use case" → Product Overview
- Keywords "architecture", "technical", "infrastructure" → Technical Documentation
- Keywords "API", "endpoint", "schema", "authentication" → API Documentation
- Keywords "release", "version", "changelog" → Release Notes

---

### 3. **Content Generation**

**Objective**: Generate documentation draft using template structure

### Product Overview Generation

**Template**: `templates/product-overview-template.md`

**Key Sections to Fill**:

1. **Document Information**:
   - Product Name
   - Version
   - Owner
   - Status (Draft/Published)

2. **What It Does** (Section 1):
   - Product Summary: 2-3 sentences
   - Key Capabilities: 3-5 main features
   - Value Proposition: Problem solved + value delivered

3. **Who Uses It** (Section 2):
   - Primary Users table (User Type, Role, Use Case, Frequency)
   - User Personas (Goals, Pain Points, How This Helps)

4. **Business Impact** (Section 3):
   - Key Metrics table (Metric, Current, Target, Impact)
   - Business Outcomes (Revenue, Cost Savings, Strategic Value)

5. **Core Features** (Section 4):
   - Feature 1-3: What it does, who uses it, business value

6. **How It Works** (Section 5):
   - High-level user journey
   - Integration points

7. **Success Stories** (Section 6):
   - Use cases with challenge/solution/result

8. **Roadmap** (Section 7):
   - Current status
   - Upcoming features (3-6 months)
   - Long-term vision (6-12 months)

**Example Output**:
```markdown
# Product Overview – Ferret Catalog Management

## 1. What It Does

### Product Summary
Ferret Catalog Management is an internal service that manages product catalog data for the Kredivo ecosystem. It provides a centralized API for creating, updating, and querying product information across all Kredivo platforms.

### Key Capabilities
- **Catalog CRUD Operations:** Create, read, update, delete product information
- **Real-time Sync:** Synchronize product data across multiple services
- **Advanced Search:** Filter and search products by category, price, attributes
- **Bulk Operations:** Import/export large product datasets via CSV
- **Version Control:** Track product data changes with full audit history

### Value Proposition
Solves the problem of scattered product data across multiple databases by providing a single source of truth for all product information, reducing data inconsistency and improving time-to-market for new products by 40%.

## 2. Who Uses It

### Primary Users

| User Type | Role | Use Case | Frequency |
|---|---|---|---|
| Product Managers | Catalog Owner | Manage product listings, update prices, configure attributes | Daily |
| Developers | Integration Engineer | Integrate catalog API with frontend/backend services | Weekly |
| Data Analysts | Data Consumer | Query product data for reports and analysis | Daily |
| Operations | Support Staff | Troubleshoot catalog issues, verify product data | Weekly |

### User Personas

**Persona 1: Product Manager**
- **Goals:** Quickly add new products, bulk update prices, ensure data accuracy
- **Pain Points:** Manual data entry, inconsistent data across platforms, slow updates
- **How This Helps:** Centralized dashboard for bulk operations, automated validation, real-time sync

**Persona 2: Backend Developer**
- **Goals:** Integrate catalog API with services, reliable data access, good performance
- **Pain Points:** API downtime, slow queries, unclear documentation
- **How This Helps:** 99.9% uptime SLA, optimized queries, comprehensive API docs
```

---

### Technical Documentation Generation

**Template**: `templates/technical-documentation-template.md`

**Key Sections to Fill**:

1. **Architecture Overview**:
   - System Context diagram
   - High-level description
   - Design principles

2. **Architecture Components**:
   - Component diagram
   - Components description (Technology, Responsibility, Hosted)

3. **Data Flow**:
   - Request flow diagram
   - Data processing pipeline

4. **Infrastructure**:
   - Deployment architecture
   - Technology stack
   - Scaling strategy

5. **Database Schema**:
   - ERD
   - Key tables with SQL
   - Indexes
   - Migration strategy

6. **Security**:
   - Authentication & Authorization
   - Data security
   - Compliance

7. **Performance & SLA**:
   - SLO table
   - Performance benchmarks
   - Monitoring & Alerts

8. **Disaster Recovery**:
   - Backup strategy
   - DR plan
   - High availability

---

### API Documentation Generation

**Template**: `templates/api-documentation-template.md`

**Key Sections to Fill**:

1. **Overview**:
   - What API does
   - Key features
   - Use cases

2. **Getting Started**:
   - Prerequisites
   - Quick start example with curl

3. **Authentication**:
   - Authentication methods
   - Getting API key
   - Token lifecycle

4. **Rate Limiting**:
   - Limits table by plan
   - Rate limit headers
   - Handling rate limits

5. **API Endpoints**:
   - Base URL
   - For each endpoint:
     - HTTP method and path
     - Path parameters
     - Headers
     - Request body (if applicable)
     - Response (success and errors)

6. **Data Schemas**:
   - JSON schema for each object type

7. **Error Handling**:
   - Error response format
   - HTTP status codes table
   - Common error codes

8. **SLA & Service Guarantees**:
   - Availability table
   - Support SLA table

---

### Release Notes Generation

**Template**: `templates/release-notes-template.md`

**Key Sections to Fill**:

1. **Version Header**:
   - Version number (X.Y.Z)
   - Release name (optional)
   - Release date

2. **What's New**:
   - Major Features
   - Improvements

3. **Bug Fixes**:
   - Fixed issues with impact and resolution

4. **Technical Changes**:
   - Dependency upgrades
   - Performance improvements

5. **Breaking Changes**:
   - What changed
   - Impact
   - Migration code examples

6. **Metrics & Impact**:
   - Table showing before/after metrics

7. **Deployment Information**:
   - Release date
   - Deployment type
   - Downtime
   - Rollback plan

8. **Migration Guide**:
   - For users
   - For developers

---

### 4. **Validation Checklist**

**Objective**: Ensure documentation completeness

### Product Overview Checklist:
```
[ ] Product name and version clearly stated
[ ] What It Does section explains core capabilities
[ ] Primary users and personas identified
[ ] Business impact with metrics (current vs target)
[ ] Core features documented (at least 3)
[ ] High-level flow diagram or description
[ ] Success stories or use cases included
[ ] Roadmap with upcoming features
[ ] Getting started guide provided
[ ] Contact and support information
```

### Technical Documentation Checklist:
```
[ ] Architecture diagram included
[ ] All components described with technology stack
[ ] Data flow documented
[ ] Infrastructure and deployment details
[ ] Database schema with ERD
[ ] Security measures documented
[ ] SLA/SLO with metrics
[ ] Disaster recovery plan
[ ] Monitoring and alerting setup
[ ] Troubleshooting guide
[ ] Development setup instructions
```

### API Documentation Checklist:
```
[ ] API overview explains purpose and use cases
[ ] Authentication method documented
[ ] Rate limiting clearly explained
[ ] All endpoints documented with examples
[ ] Request/response schemas defined
[ ] Error handling documented
[ ] HTTP status codes table
[ ] SLA and support information
[ ] SDKs or client libraries listed
[ ] Quick start guide with working code
```

### Release Notes Checklist:
```
[ ] Version number follows semantic versioning
[ ] Release date specified
[ ] New features listed and explained
[ ] Bug fixes documented
[ ] Breaking changes highlighted with migration guide
[ ] Metrics showing impact (before/after)
[ ] Deployment plan described
[ ] Migration instructions for users and developers
[ ] Known issues listed (if any)
[ ] Support contact information
```

---

### 5. **Output & Delivery**

**Objective**: Save documentation draft to local file (READ-ONLY mode)

**File Naming Convention**:
```
output/docs-[type]-[product-name]-[YYYYMMDD].md

Examples:
- output/docs-product-overview-ferret-catalog-20260406.md
- output/docs-technical-ferret-catalog-service-20260406.md
- output/docs-api-ferret-catalog-api-20260406.md
- output/docs-release-notes-v2.1.0-20260406.md
```

**Process**:
1. Generate complete documentation using template
2. Save to `/output` folder (NOT workspace root)
3. Show preview to user for review
4. If in READ-ONLY mode → provide instructions for manual Confluence publishing

**READ-ONLY Mode Behavior**:
```markdown
✅ Documentation generated: output/docs-product-overview-ferret-catalog-20260406.md

⚠️ **READ-ONLY MODE ACTIVE**
I cannot publish this documentation to Confluence directly.

**To publish manually:**
1. Open Confluence: https://finacceljira.atlassian.net/wiki
2. Navigate to appropriate space
3. Click "Create" button
4. Select "Blank page"
5. Copy-paste content from the draft file above
6. Click "Publish"

**Alternative:** If you want to enable write mode, see READ-ONLY-MODE.md
```

**If user asks to publish to Confluence**: Use **REFUSAL PROTOCOL** from senior-pm instructions.

---

## Integration with Other Tools

### Confluence Search (Context Gathering)

**Before generating**, search for existing documentation:

```bash
confluence_search(query="product overview ferret", limit=5)
confluence_search(query="technical documentation architecture", limit=3)
```

Use results to:
- Understand documentation patterns
- Reference similar docs
- Maintain consistent terminology
- Avoid duplicating existing content

### Jira Search (For Release Notes)

Search for completed issues in sprint/release:

```bash
jira_search(jql="project = DPT AND fixVersion = '2.1.0' AND status = Done", max_results=50)
```

Use to auto-populate:
- Bug fixes from Jira tickets
- Features completed in release
- Breaking changes from Epic/Story descriptions

---

## Example Prompts

**Product Overview:**
```
"Bikin product overview untuk Ferret Catalog Management service"
→ Asks clarifying questions → Generates overview with capabilities, users, business impact

"Generate product documentation untuk new payment gateway integration"
→ Searches existing payment docs → Generates comprehensive overview
```

**Technical Documentation:**
```
"Bikin technical docs untuk Ferret Catalog service architecture"
→ Generates architecture diagrams, components, data flow, infrastructure details

"Draft technical documentation for microservices migration"
→ Includes before/after architecture, migration plan, rollback strategy
```

**API Documentation:**
```
"Bikin API docs untuk Ferret Catalog API endpoints"
→ Generates authentication, endpoints, schemas, error handling

"Generate API reference untuk /catalog API v2"
→ Documents all CRUD operations, pagination, filtering, rate limits
```

**Release Notes:**
```
"Bikin release notes untuk v2.1.0"
→ Searches Jira for completed tickets → Generates changelog with features, fixes, metrics

"Draft release notes untuk Q1 2026 major release"
→ Includes breaking changes, migration guide, deployment plan
```

---

## Error Handling & Fallbacks

**If template file not found**:
```
❌ Error: Template file not found: templates/product-overview-template.md
→ Fallback: Generate basic structure from memory
→ Log warning to check template files
```

**If user provides minimal info**:
```
→ Use vscode_askQuestions to gather required fields
→ Generate with [TBD] placeholders for unknown items
→ Show draft and ask user to fill missing details
```

**If unsure about documentation type**:
```
→ Ask: "What type of documentation? (Product Overview / Technical / API / Release Notes)"
→ Default to Product Overview if still unclear
```

---

## Quality Standards

**A good Product Overview has**:
✅ Clear product summary (2-3 sentences)
✅ 3-5 key capabilities listed
✅ User personas with goals and pain points
✅ Business impact with measurable metrics
✅ Core features explained (what, who, why)
✅ High-level flow or integration diagram
✅ Success stories with results
✅ Roadmap with upcoming features
✅ Getting started guide
✅ Contact and support info

**A good Technical Documentation has**:
✅ Architecture diagram (system context + components)
✅ All components described with tech stack
✅ Data flow with request/response cycles
✅ Infrastructure details (deployment, scaling)
✅ Database schema with ERD
✅ Security measures (auth, encryption, compliance)
✅ SLA/SLO with specific targets
✅ Disaster recovery plan
✅ Monitoring and alerting setup
✅ Troubleshooting guide
✅ Development setup instructions
✅ Runbook for operations

**A good API Documentation has**:
✅ Clear API purpose and use cases
✅ Authentication method with examples
✅ Rate limiting rules and headers
✅ All endpoints documented with curl examples
✅ Request/response schemas (JSON)
✅ Error handling with status codes
✅ Pagination, filtering, sorting explained
✅ SLA and support information
✅ SDKs/client libraries listed
✅ Quick start guide with working code
✅ Webhooks documented (if applicable)
✅ Versioning and deprecation policy

**A good Release Notes has**:
✅ Semantic version number (X.Y.Z)
✅ Release date and deployment window
✅ New features with descriptions and value
✅ Bug fixes with impact and tickets
✅ Breaking changes with migration code examples
✅ Metrics showing before/after impact
✅ Deployment plan (type, downtime, rollback)
✅ Migration guide for users and developers
✅ Known issues (if any)
✅ Support contact during release

---

## Notes

- Always reference templates from `/templates` folder
- Search for existing docs before generating (avoid duplicates)
- In READ-ONLY mode, always save to `/output` folder
- Use consistent language from existing documentation
- Include diagrams (ASCII art or links to visual diagrams)
- Link to related docs (PRD, API reference, user guides)
- Keep documentation up-to-date (version numbers, dates)

## Related Skills

- **atlassian-ops**: For Confluence search and operations
- **prd-writer**: Reference for comprehensive documentation patterns
- **jira-ticket-writer**: For linking Jira tickets in release notes

## Changelog

- **2026-04-06 v1.0**: Initial version
  - Support for 4 documentation types
  - Template-based generation
  - Comprehensive validation checklists
  - READ-ONLY mode support
  - Integration with Confluence/Jira search
