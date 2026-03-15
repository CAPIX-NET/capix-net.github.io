Web-enabled treasury application project.

CAPIX is a well-established vendor of treasury software, with customers in eight countries.

Our main customers are corporate treasury operations, and we also have customers in the funds management and commodities trading sectors.

The CAPIX software consisits of several modules, including foreign exchange (FX), money market (MM) and banking (BK).

The CAPIX Treasury Manager (CTM) software is a 64bit Windows desktop application that is based on a Mirosoft technology stack. This includes Microsoft Access, Microsoft Visual C++ Dlls and a Microsofr SQL Server database.

The Microsoft Access application is very large, with around 200 Forms, 400 Queries 200 VBA Code Modules and 150 local Tables. The Microsoft SQL Server database has around 200 tables.

We want to offer a version of CTM as a web SAAS.

The new produce should run in a Desktop browser, mobile browser and possibly a Mobile app.

Our design priorities are to reuse as much existing code as possible and to also continue with a Microsoft technology platform running in th eAzure Cloud.

  Architecture & Codebase

  1. VC++ DLLs — What do they handle? (e.g., calculations/pricing, market data feeds, encryption, integrations?) How many DLLs and roughly how much code?
  There are 4 .DLL files that do calculations for pricing, encryption, maths-intensive functions.

  2. VBA module breakdown — Of the 200 VBA modules, roughly what percentage is business logic vs. UI logic vs. data access? This is the biggest factor in determining the reuse strategy.
  The VBA modules are mainly for business logic.

  3. 400 Queries — Are these primarily Access (JET SQL) queries or SQL Server stored procedures/views? How much business logic lives in the queries?
  Yes, these are local Jet SQL queries that access both the local Access tables and the remote SQL Server tables via ODBC "Linked Tables".

  4. Local vs. SQL Server tables — What role do the 150 local Access tables play? (temp/working data, user preferences, lookup/reference data?)
Local tables are used for temporary storage Eg. processing transactions before being written to SQL SErver. SQL Server tables are the main and persistance storage.

  Operational

  5. Integrations — Does CTM integrate with external systems (SWIFT, Bloomberg/Reuters, banking APIs, market data feeds, ERP systems)?
  Yes, CTM integrates with banking feeds, including SWIFT etc, pricing feeds such as Reuters and ERP systems like SAP and Oracle. Increasingly we are inegrating with Microsoft Dynamics 365.

  6. Users per site — How many concurrent users typically at a customer site? This drives architecture choices (e.g., Blazor Server vs. WebAssembly).
  Typically there are no more than 3 or 4 concurreny users per site.

  7. Authentication — Currently Windows/AD authentication? Customers would expect Azure AD/Entra ID for SaaS?
  Yes.

  8. Reporting — What reporting is currently used? (Access Reports, SSRS, Crystal, Excel exports?)
Currently using Microsoft Access Reports.

  SaaS & Deployment

  9. Multi-tenancy — Separate database per customer, or shared multi-tenant database?
Not decided yet.

  10. Current deployment — On-premises at each client site today? Any customers already hosted?
All current deployments are on-premises for each client.

  11. Phased approach — Is it acceptable to migrate module-by-module (e.g., BK first, then MM, then FX), or does it need to go live as a complete product?
Needs to go live as a complete product.

  12. Offline/local requirements — Do users need any offline capability, or is always-connected acceptable for SaaS?
Always-connected for SaaS is acceptable.

  The answers to #1, #2, and #3 especially will determine whether the best path is Blazor (maximizes C#/.NET reuse), Power Apps (low-code, leverages
  Access/SQL Server knowledge), or a more conventional ASP.NET Core + React/Angular approach.

In the corporate works Microsoft is universal, so we can't stray too far from Microsoft technology. a preference is to has a service with a similar look and feel to Microsoft Dynamics 365.

 Critical for the Architecture

  1. C++ DLL source code — Do you have the source code for the 4 VC++ DLLs? Could they be rewritten in C#, or do they need to be wrapped/called as-is?
  We have all of the source code for the .DLLs, they could be rewritten in C#, but would prefer to stick with C++. The DLLs are only used for calculations and have no UI or DB code.

  2. Team skills — What does your development team look like? Primarily VBA/Access developers, or do you also have C#/.NET experience? This affects how aggressive the migration approach can be.
  Team are mainly VBA developers.

  3. Dynamics 365 look-and-feel — When you say similar to D365, do you mean specifically the UI style (Fluent UI, navigation, grid layouts), or also the platform model (model-driven apps, Dataverse)?
  Open to suggestions.

  Practical Constraints

  4. Timeline — Any target timeframe? (e.g., MVP in 6 months, full product in 18 months?)
  No decided.

  5. Existing customers — Will on-prem customers migrate to SaaS, or will you maintain both on-prem and SaaS versions in parallel?
  Existing customers will migrate to SaaS.

  6. Regulatory/compliance — Any specific data residency or audit requirements for treasury data? (This affects multi-tenancy and Azure region decisions.)
  Existing database design and business logic cover audit requirements. We want to retain the existing transaction processing model and Database design where practical.


## Recommended Architecture

### Technology Stack

| Layer | Technology | Notes |
|---|---|---|
| Frontend (UI) | Blazor Server + Microsoft Fluent UI Blazor | C# required for .razor files; D365 look-and-feel |
| Business Logic | VB.NET Class Libraries | Migrated from VBA — closest syntax match, fastest migration path |
| Calculations | Existing C++ DLLs via P/Invoke | Recompiled for 64-bit Windows server, called from VB.NET |
| Data Access | Entity Framework Core (VB.NET) | Replaces JET SQL queries and ODBC linked tables |
| Database | Azure SQL Database (per tenant) | Retain existing schema; Elastic Pools for cost management |
| Auth | Microsoft Entra ID (Azure AD) | Replaces Windows/AD authentication |
| Reporting | SSRS + Power BI Embedded | SSRS for transactional reports; Power BI for analytics |
| Hosting | Azure App Service (Windows) | Windows required for C++ DLL P/Invoke |
| Integrations | Azure Service Bus + Azure Functions | SWIFT, Reuters, SAP, Oracle, Dynamics 365 connectors |

### Hybrid Language Approach

- **VB.NET** for business logic class libraries (200 VBA modules migrate with minimal syntax changes)
- **C#** for Blazor UI layer only (.razor components — mostly HTML markup with thin event handlers)
- **C++** DLLs retained as-is, called via P/Invoke wrapper classes from VB.NET
- VB.NET and C# interoperate seamlessly in the same .NET solution — zero performance difference

### Multi-Tenancy: Database-per-Tenant

- Preserves existing DB design per customer
- Each on-prem SQL Server database migrates directly to Azure SQL
- Strong data isolation for financial/treasury data
- Azure SQL Elastic Pools manage cost across multiple small databases

### Reporting Strategy

- **SSRS** for transactional/print-ready reports (deal confirmations, settlement instructions, statements)
- **Power BI Embedded** for interactive analytical reports (position reports, P&L, exposure analysis)

#### Power BI vs Access Reports Comparison

These serve different purposes and are not direct substitutes for each other.

**Where Access Reports excel (and Power BI does not):**

| Capability | Access Reports | Power BI |
|---|---|---|
| Pixel-perfect layout | Precise control over every element | No — layout is responsive/fluid |
| Print-ready output | Designed for printing — page breaks, headers/footers | Weak — PDF export exists but layout control is limited |
| Banded reports | Group header/footer bands with running totals | No banding concept |
| Subreports | Embed related detail reports easily | No equivalent — use drill-through pages |
| Transactional documents | Deal confirmations, SWIFT messages, statements | Not designed for this |
| Page numbering / breaks | Full control | Basic at best |

**Where Power BI excels (and Access Reports do not):**

| Capability | Access Reports | Power BI |
|---|---|---|
| Interactive drill-down | Static once rendered | Click to filter, drill into details |
| Cross-filtering | Not possible | Click one chart, all others filter |
| Dashboards | Not a concept | Core strength — multiple visuals on one page |
| Real-time refresh | Must rerun the report | Scheduled or real-time data refresh |
| Sharing / collaboration | Print or export | Share links, embed in apps, comment |
| Mobile | Not supported | Native mobile app with responsive layout |
| DAX calculations | N/A | Time intelligence, rolling averages, etc. |
| Natural language queries | N/A | Users can type questions like "show FX exposure by currency" |

#### Report Migration Plan

| Report Category | Current | New | Benefit |
|---|---|---|---|
| Deal confirmations | Access Report | SSRS | Same paradigm, print-perfect, PDF/email delivery |
| Settlement instructions | Access Report | SSRS | Precise layout for counterparty-facing documents |
| Audit trails | Access Report | SSRS | Banded detail with grouping/totals |
| Position/exposure dashboards | Access Report (static) | Power BI Embedded | Interactive, drill-down, real-time — major upgrade |
| Cash flow forecasts | Access Report | Power BI Embedded | Time intelligence, scenario comparison |
| Ad-hoc analysis | Limited in Access | Power BI | Self-service, users build their own views |

SSRS replaces Access Reports for structured/transactional output. Power BI adds interactive analytics — a significant upgrade over current capabilities. Together they cover all reporting needs.

### Migration Work Streams

1. **Infrastructure** — Azure App Service, Azure SQL, Entra ID, CI/CD pipelines
2. **Database** — Migrate SQL Server schema to Azure SQL; convert JET SQL queries to EF Core / T-SQL; replace local Access tables with SQL Server temp tables or in-memory caching
3. **Business Logic** — Convert 200 VBA modules to VB.NET class libraries (largest effort ~40%)
4. **C++ DLLs** — Recompile for 64-bit server, create P/Invoke wrapper classes
5. **UI** — Rebuild 200 Access Forms as Blazor pages/components using Fluent UI Blazor (C#)
6. **Reporting** — Migrate Access Reports to SSRS; build Power BI dashboards for analytics
7. **Integrations** — Azure Functions for SWIFT, Reuters, SAP, D365 connectors
8. **Auth & Tenancy** — Entra ID integration, tenant provisioning, database routing

### Migration Tools

#### VBA → VB.NET (Business Logic)

| Tool | Type | How It Helps |
|---|---|---|
| Claude / Claude Code | AI | Converts VBA modules to VB.NET interactively; handles Access-specific objects (DoCmd, Recordset, CurrentDb, etc.) and suggests .NET replacements |
| GitHub Copilot | AI | Inline conversion suggestions as you work in Visual Studio |
| Mobilize.Net (Visual Basic Upgrade Companion) | Commercial | Automated VB6/VBA to VB.NET conversion; handles common patterns at scale |

No tool fully handles Access-specific object model references automatically (e.g. CurrentDb.OpenRecordset, DoCmd.OpenForm, Me.Controls). These must be replaced with .NET equivalents (EF Core, Blazor navigation, etc.). AI tools are best at this — they understand the intent and suggest appropriate replacements.

#### JET SQL → T-SQL / EF Core (Queries)

| Tool | Type | How It Helps |
|---|---|---|
| SQL Server Migration Assistant (SSMA) for Access | Free (Microsoft) | Converts Access queries to T-SQL views/stored procedures; migrates local table schemas to SQL Server; handles JET-to-T-SQL syntax differences (IIf, Nz, Format, etc.) automatically |
| Claude / Copilot | AI | Converts JET SQL to LINQ (EF Core) or T-SQL on a query-by-query basis |

SSMA is the standout tool here — purpose-built for this migration. It can also migrate the 150 local Access tables into SQL Server in one pass.

#### Access Forms → Blazor (UI)

| Tool | Type | How It Helps |
|---|---|---|
| Claude / Copilot | AI | Describe an Access form's layout and behavior, get a Blazor component back; can process exported form definitions |
| Access SaveAsText export | Built-in Access | Application.SaveAsText exports form definitions to text files — these can be fed to AI for conversion |

No direct converter exists for this path. Practical approach: export Access form definitions using SaveAsText, then use AI to generate Blazor/Fluent UI component scaffolding. Manual refinement still needed, but AI significantly accelerates initial conversion.

#### Access Reports → SSRS

| Tool | Type | How It Helps |
|---|---|---|
| SSMA for Access | Free (Microsoft) | Limited report migration capability — converts some Access Reports to SSRS .rdl format |
| SQL Server Report Builder | Free (Microsoft) | Visual designer for SSRS reports — closest experience to the Access Report designer |
| Visual Studio (SSDT) | Free | Full SSRS report design environment with preview |
| Claude / Copilot | AI | Describe report layout/data source, get an SSRS report definition |

#### C++ DLLs → P/Invoke Wrappers

| Tool | Type | How It Helps |
|---|---|---|
| CppSharp / P/Invoke Interop Assistant | Free | Auto-generates VB.NET/C# P/Invoke declarations from C++ header files |
| Claude / Copilot | AI | Generate P/Invoke wrapper classes from C++ function signatures |

Straightforward since the DLLs are calculation-only with no UI or DB code.

#### Recommended Tool Workflow

1. **Start with SSMA** — run against the Access database to migrate local tables, convert queries to T-SQL, and get baseline SSRS report conversions (free, handles mechanical conversion)
2. **Use AI (Claude) for VBA → VB.NET** — process modules in batches, replacing Access object model references with .NET equivalents (largest value-add from AI)
3. **Use SaveAsText + AI for forms** — export all 200 form definitions, then use AI to generate Blazor component scaffolding
4. **Use P/Invoke Interop Assistant** for C++ DLL wrappers — quick, mechanical
5. **Build SSRS reports in Report Builder** — visual designer makes this relatively fast; concepts map directly from Access Reports

## Code Migration Plan

### Phase 0: Preparation & Extraction (Weeks 1–3)

**Goal:** Extract all code and artifacts from the Access application into text-based formats that can be version-controlled and processed by automation tools.

**Steps:**

1. **Bulk-export all Access objects using VBA automation script:**
   Run the following VBA macro inside the Access application to export every form, report, query, module, and table definition to text files:
   ```vba
   Sub ExportAllObjects()
       Dim db As Database
       Set db = CurrentDb
       Dim obj As Object
       Dim i As Integer
       Dim exportPath As String
       exportPath = "C:\CTM_Export\"

       ' Export Forms
       For i = 0 To db.Containers("Forms").Documents.Count - 1
           Application.SaveAsText acForm, db.Containers("Forms").Documents(i).Name, _
               exportPath & "Forms\" & db.Containers("Forms").Documents(i).Name & ".txt"
       Next i

       ' Export Reports
       For i = 0 To db.Containers("Reports").Documents.Count - 1
           Application.SaveAsText acReport, db.Containers("Reports").Documents(i).Name, _
               exportPath & "Reports\" & db.Containers("Reports").Documents(i).Name & ".txt"
       Next i

       ' Export Modules
       For i = 0 To db.Containers("Modules").Documents.Count - 1
           Application.SaveAsText acModule, db.Containers("Modules").Documents(i).Name, _
               exportPath & "Modules\" & db.Containers("Modules").Documents(i).Name & ".txt"
       Next i

       ' Export Queries
       For Each qdf In db.QueryDefs
           If Left(qdf.Name, 1) <> "~" Then
               Dim f As Integer
               f = FreeFile
               Open exportPath & "Queries\" & qdf.Name & ".sql" For Output As #f
               Print #f, qdf.SQL
               Close #f
           End If
       Next qdf

       ' Export Table schemas
       For Each tdf In db.TableDefs
           If Left(tdf.Name, 4) <> "MSys" Then
               Dim ft As Integer
               ft = FreeFile
               Open exportPath & "Tables\" & tdf.Name & ".txt" For Output As #ft
               Print #ft, "Table: " & tdf.Name
               Dim fld As Field
               For Each fld In tdf.Fields
                   Print #ft, fld.Name & " | " & fld.Type & " | Size: " & fld.Size
               Next fld
               Close #ft
           End If
       Next tdf
   End Sub
   ```

2. **Commit all exports to a Git repository** — this creates a baseline and enables tracking of conversion progress.

3. **Create an inventory spreadsheet** cataloguing every object with:
   - Object name, type (Form/Report/Module/Query/Table)
   - Module (FX, MM, BK, or shared)
   - Complexity estimate (Simple / Medium / Complex)
   - Dependencies (which queries, tables, and modules each form uses)
   - Conversion status (Not started / In progress / Converted / Tested)

4. **Run SSMA Assessment** against the Access database to generate a migration assessment report — identifies conversion issues before you start.

**Automation:** The export script above automates the entire extraction. The inventory can be partially automated by parsing the exported files for references (e.g., grep for query names, table names, DoCmd references).

---

### Phase 1: Database & Data Access (Weeks 2–6)

**Goal:** Migrate all data storage to Azure SQL and establish the EF Core data access layer.

**Steps:**

1. **Run SSMA to migrate local Access tables to SQL Server**
   - SSMA converts the 150 local table schemas automatically
   - Review and adjust data types (JET types → SQL Server types)
   - Merge into the existing SQL Server database or keep as separate schema

2. **Run SSMA to convert 400 JET SQL queries to T-SQL**
   - SSMA handles IIf→CASE, Nz→ISNULL, Format→FORMAT, etc.
   - Review each converted query for correctness
   - Decide per query: keep as T-SQL view/stored procedure, or convert to EF Core LINQ

3. **Create EF Core data model (VB.NET)**
   - Scaffold EF Core entities from the SQL Server database using `dotnet ef dbcontext scaffold`
   - This auto-generates VB.NET entity classes and DbContext from the existing schema
   - Preserves your existing database design exactly

4. **Replace local temp table patterns**
   - Access local tables used for transaction staging → replace with SQL Server temp tables (#tables), table-valued parameters, or in-memory collections
   - Design a VB.NET service layer pattern for transaction processing (stage → validate → commit)

5. **Deploy to Azure SQL**
   - Create Azure SQL Elastic Pool
   - Migrate one customer database as pilot
   - Validate all queries execute correctly

**Automation:**
- SSMA automates table migration and query conversion (handles ~80-90% automatically)
- `dotnet ef dbcontext scaffold` auto-generates the entire EF Core model from existing schema
- Write a PowerShell script to batch-run SSMA across all query exports and log conversion issues:
  ```powershell
  # Pseudocode — SSMA supports command-line execution
  foreach ($query in Get-ChildItem "C:\CTM_Export\Queries\*.sql") {
      # Convert and log results
      ssma-console.exe /convert $query.FullName /output "C:\CTM_Converted\Queries\"
  }
  ```

---

### Phase 2: Business Logic — VBA to VB.NET (Weeks 3–14)

**Goal:** Convert 200 VBA modules to VB.NET class libraries. This is the largest work stream.

**Steps:**

1. **Create the .NET solution structure:**
   ```
   CTM.sln
   ├── CTM.BusinessLogic/          (VB.NET class library — migrated VBA modules)
   ├── CTM.Calculations/           (VB.NET P/Invoke wrappers for C++ DLLs)
   ├── CTM.DataAccess/             (VB.NET — EF Core DbContext and repositories)
   ├── CTM.Shared/                 (VB.NET — shared models, enums, constants)
   └── CTM.Web/                    (C# Blazor Server — UI layer)
   ```

2. **Batch-convert VBA modules using the Claude API:**
   Build a PowerShell automation script that sends each exported VBA module to the Claude API for conversion:
   ```powershell
   $modules = Get-ChildItem "C:\CTM_Export\Modules\*.txt"
   $systemPrompt = @"
   You are converting VBA modules from a Microsoft Access treasury application to VB.NET class libraries.
   Rules:
   - Output valid VB.NET (.NET 8) code
   - Replace DAO/ADO Recordset with EF Core DbContext patterns
   - Replace DoCmd calls with comments indicating UI action needed
   - Replace CurrentDb references with injected DbContext
   - Replace MsgBox with method return values or exceptions
   - Add Imports statements for System, System.Collections.Generic, Microsoft.EntityFrameworkCore
   - Use dependency injection pattern (constructor injection for DbContext)
   - Preserve all business logic exactly
   - Flag anything that cannot be automatically converted with 'TODO: MANUAL REVIEW
   "@

   foreach ($module in $modules) {
       $vbaCode = Get-Content $module.FullName -Raw
       $response = Invoke-ClaudeAPI -System $systemPrompt -User "Convert this VBA module to VB.NET:`n`n$vbaCode"
       $outputPath = "C:\CTM_Converted\BusinessLogic\" + $module.BaseName + ".vb"
       Set-Content $outputPath $response
       Write-Host "Converted: $($module.Name) → $($module.BaseName).vb"
   }
   ```

3. **Review and fix AI-converted code:**
   - Each converted module needs manual review
   - Focus on: data access patterns, error handling, Access-specific object replacements
   - Items flagged with `TODO: MANUAL REVIEW` need human attention
   - Estimate ~60-70% of code converts cleanly; remainder needs manual adjustment

4. **Organise modules by functional area:**
   - Group into namespaces: CTM.BusinessLogic.FX, CTM.BusinessLogic.MM, CTM.BusinessLogic.BK, CTM.BusinessLogic.Common
   - Identify shared utilities and extract to CTM.Shared

5. **Build and resolve compilation errors iteratively**
   - After batch conversion, build the solution — expect compile errors
   - Use Claude Code interactively to fix remaining issues in each file

**Automation:**
- The Claude API batch script above automates the initial conversion of all 200 modules
- A CI pipeline can be set up to build after each batch of conversions, tracking compile-error count trending toward zero
- Write a script to scan converted files and report: total TODO count, compile errors, unconverted Access references (grep for "DoCmd", "CurrentDb", "Recordset", "MsgBox")

---

### Phase 3: C++ DLL Integration (Weeks 4–5)

**Goal:** Make the 4 existing C++ DLLs callable from VB.NET.

**Steps:**

1. **Extract function signatures** from C++ header files

2. **Auto-generate P/Invoke wrappers** using CppSharp or Claude:
   ```vbnet
   ' Example P/Invoke wrapper
   Imports System.Runtime.InteropServices

   Public Class PricingCalculations
       <DllImport("CTMPricing.dll", CallingConvention:=CallingConvention.Cdecl)>
       Public Shared Function CalculateFXForward(
           spotRate As Double, domesticRate As Double,
           foreignRate As Double, days As Integer) As Double
       End Function
   End Class
   ```

3. **Recompile DLLs for 64-bit Windows Server** if not already 64-bit

4. **Write unit tests** validating that P/Invoke results match existing Access-based results — use known test cases from production

**Automation:**
- CppSharp auto-generates P/Invoke declarations from headers
- Unit tests can be automated to run against a set of known input/output pairs exported from the current Access application

---

### Phase 4: UI — Access Forms to Blazor (Weeks 6–18)

**Goal:** Rebuild 200 Access Forms as Blazor Server pages using Fluent UI Blazor.

**Steps:**

1. **Build a base application shell first:**
   - Navigation (left sidebar matching D365 style)
   - Authentication (Entra ID)
   - Tenant context (database routing)
   - Shared layout components (page header, breadcrumbs, notification area)
   - Base CRUD page template

2. **Create reusable Blazor component patterns** that map to common Access form patterns:

   | Access Pattern | Blazor Equivalent |
   |---|---|
   | Continuous Form (data grid) | `<FluentDataGrid>` with inline editing |
   | Single-record Form | Blazor EditForm with `<FluentTextField>`, `<FluentSelect>`, etc. |
   | Tab Control | `<FluentTabs>` |
   | Subform | Child Blazor component with cascading parameter |
   | Combo Box (lookup) | `<FluentAutocomplete>` bound to lookup service |
   | Command buttons | `<FluentButton>` with @onclick handlers |
   | Popup / Dialog | `<FluentDialog>` or `<FluentDialogService>` |
   | List Box | `<FluentListbox>` |

3. **Batch-convert form definitions using Claude API:**
   Similar to the VBA conversion, feed exported form definitions to the Claude API:
   ```powershell
   $forms = Get-ChildItem "C:\CTM_Export\Forms\*.txt"
   $systemPrompt = @"
   You are converting Microsoft Access form definitions to Blazor Server components using Fluent UI Blazor.
   Rules:
   - Output a .razor file and a .razor.cs code-behind file
   - Map Access controls to Fluent UI Blazor components
   - Use EditForm with DataAnnotationsValidator for validation
   - Inject the appropriate business logic service (not DbContext directly)
   - Create cascading parameters for subform relationships
   - Preserve the form layout as closely as practical using CSS grid
   - Flag complex controls or custom ActiveX controls with TODO: MANUAL REVIEW
   "@

   foreach ($form in $forms) {
       $formDef = Get-Content $form.FullName -Raw
       $response = Invoke-ClaudeAPI -System $systemPrompt -User "Convert this Access form to Blazor:`n`n$formDef"
       # Split response into .razor and .razor.cs files
       $outputBase = "C:\CTM_Converted\Pages\" + $form.BaseName
       # ... save files
   }
   ```

4. **Prioritise form conversion by module:**
   - Convert shared/common forms first (login, main menu, user preferences)
   - Then by module: BK → MM → FX (or whichever has the simplest forms first)
   - Leave complex forms (e.g., deal entry with real-time pricing) for last

5. **Wire up to business logic layer:**
   - Create Blazor service classes that call the VB.NET business logic
   - Register services in DI container

**Automation:**
- Claude API batch script handles initial scaffolding of all 200 forms
- Create a PowerShell script to generate a progress dashboard: forms converted / total, compile status, TODO count per form
- Build a Blazor component template generator (dotnet new template) for standard CRUD pages — developers fill in entity-specific fields

---

### Phase 5: Reporting (Weeks 10–16)

**Goal:** Replace Access Reports with SSRS and Power BI.

**Steps:**

1. **Export Access Report definitions** (already done in Phase 0)

2. **Categorise reports** into transactional (→ SSRS) and analytical (→ Power BI)

3. **Convert transactional reports to SSRS:**
   - Use Report Builder visual designer
   - Map Access Report banding → SSRS Tablix grouping
   - Map Access subreports → SSRS subreports
   - Data source = Azure SQL stored procedures or views
   - Feed exported report definitions to Claude to generate initial .rdl XML

4. **Build Power BI analytical reports:**
   - Connect Power BI Desktop to Azure SQL
   - Build data model with DAX measures
   - Create dashboards: position/exposure, P&L, cash flow, risk
   - Publish to Power BI Service
   - Embed in Blazor using Power BI Embedded SDK

5. **Integrate report viewing into Blazor:**
   - SSRS: embed via `<iframe>` pointing to SSRS report server URL with parameters, or use a report viewer component
   - Power BI: use the `PowerBI.Api` SDK to embed reports in Blazor pages

**Automation:**
- Claude API can generate initial .rdl XML from exported Access Report definitions
- Power BI datasets can be deployed via Power BI REST API / Azure DevOps pipeline

---

### Phase 6: Integrations (Weeks 12–18)

**Goal:** Rebuild external system connectors as Azure-hosted services.

**Steps:**

1. **Audit existing integration code** in VBA — identify all external touchpoints
2. **Build Azure Functions** for each integration:
   - SWIFT message processing
   - Reuters/market data feed ingestion
   - SAP/Oracle ERP connectors
   - Dynamics 365 integration (use D365 SDK / Dataverse Web API)
3. **Use Azure Service Bus** for message queuing between integrations and the main application
4. **Implement Azure Key Vault** for storing API keys, certificates, and connection strings

**Automation:**
- Azure Functions CI/CD via Azure DevOps or GitHub Actions
- Integration tests using recorded message samples from production

---

### Phase 7: Testing & Validation (Weeks 14–22)

**Goal:** Verify the new application matches the existing system's behaviour.

**Steps:**

1. **Automated regression testing:**
   - Export test datasets from current Access/SQL Server system
   - Run same transactions through new system
   - Compare results at the database level (automated diff scripts)

2. **Calculation validation:**
   - Build a test harness that calls both the Access VBA functions and the new VB.NET equivalents with identical inputs
   - Compare outputs — must match exactly for financial calculations

3. **Report comparison:**
   - Generate same reports from both systems with identical data
   - Visual comparison of output (PDF diff tools)

4. **User acceptance testing (UAT):**
   - Select pilot customer
   - Run parallel with existing Access system
   - Sign-off per module

**Automation:**
- Write a PowerShell/Python script that runs a suite of transactions through both systems and compares database state
- Automated PDF comparison for reports (tools like diff-pdf)
- CI pipeline runs full regression suite on every deployment

---

### Phase 8: Deployment & Customer Migration (Weeks 20–26)

**Goal:** Deploy to Azure and migrate existing customers.

**Steps:**

1. **Set up Azure production environment** — App Service, SQL Elastic Pool, Entra ID tenant
2. **Per-customer migration:**
   - Provision Azure SQL database from customer's on-prem SQL Server backup
   - Create Entra ID user accounts
   - Configure tenant routing
   - Parallel run period (2–4 weeks per customer)
   - Cut over
3. **Decommission on-prem** after validation

**Automation:**
- Write ARM/Bicep templates or Terraform for repeatable Azure environment provisioning
- PowerShell script for per-customer database migration and tenant provisioning
- Azure DevOps release pipeline for zero-downtime deployments

---

### Summary: Automation Impact

| Migration Task | Manual Effort Without Automation | With Automation |
|---|---|---|
| Export Access objects | Days (error-prone) | Minutes (VBA script) |
| 400 JET SQL queries → T-SQL | Weeks | Days (SSMA) |
| 150 local table migration | Days | Minutes (SSMA) |
| EF Core model generation | Days | Minutes (scaffold command) |
| 200 VBA modules → VB.NET | Months | Weeks (Claude API batch + manual review) |
| 200 Access Forms → Blazor | Months | Weeks (Claude API batch + manual refinement) |
| 4 C++ DLL wrappers | Days | Hours (CppSharp) |
| Access Reports → SSRS | Weeks | Days (Claude API + Report Builder) |
| Customer DB provisioning | Hours per customer | Minutes (scripted) |

The combination of SSMA, Claude API batch processing, and EF Core scaffolding reduces the overall migration effort significantly. The largest remaining manual effort is reviewing and refining AI-converted code, which requires domain knowledge of the treasury business logic.
