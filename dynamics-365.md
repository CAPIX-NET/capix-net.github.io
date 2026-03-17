The CAPIX software is sold into modern corporate treasury environments, where Microsoft technology is the standard.

We have always built our CAPIX applications using Microsoft technology to boost acceptance in the corporate technology sphere.

Over recent years Microsoft Dynamics 365 has become an increasingly popular Enterprise Resource Planning (ERP) and Accounting solution.

https://www.microsoft.com/en-us/dynamics-365

We are keen to make our application look, feel, operate and integrate with Dynamics 365.

## Dynamics 365 Technology Stack

Dynamics 365 is built on a modern Microsoft technology stack that spans cloud infrastructure, data management, development frameworks, and AI services.

### Cloud Platform — Microsoft Azure

Dynamics 365 runs entirely on Azure. All ERP workloads, application servers, integrations, and AI services are hosted on Azure, providing enterprise-grade scalability, security, and global availability.

### Data Layer — Dataverse

Dataverse (formerly Common Data Service) is the underlying data platform for Dynamics 365. It provides a standardised data model, role-based security, and a unified API surface. All Dynamics 365 business data — accounts, transactions, entities — lives in Dataverse, backed by Azure SQL Database.

### Development Languages and Frameworks

- **C# / .NET Framework (4.6.2+):** The primary language for all server-side development including plugins, custom APIs, custom workflow activities, and Azure Functions. C# is deeply integrated with the Microsoft ecosystem and is the standard for extending Dynamics 365 business logic.
- **JavaScript / TypeScript:** Used for client-side UI customisation including form scripts, web resources, and PowerApps Component Framework (PCF) controls. TypeScript is increasingly preferred for its type safety.
- **X++:** The proprietary language used specifically in Dynamics 365 Finance and Supply Chain Management (F&SCM) for ERP customisation and extensions.
- **Python:** Commonly used for writing Azure Functions that integrate with Dynamics 365, particularly for data processing and AI/ML workloads.

### Development Tools

- **Visual Studio:** The primary IDE for building managed code — plugins, custom workflow activities, and .NET integrations.
- **Visual Studio Code:** Used for web resources, JavaScript/TypeScript development, and lighter-weight scripting tasks.
- **Dynamics 365 SDK:** The official software development kit providing assemblies, code libraries, and tools for building custom extensions and integrations.
- **Power Platform CLI (pac):** Command-line tooling for solution management, component packaging, and deployment automation.

### Power Platform Integration

Dynamics 365 is tightly integrated with the Microsoft Power Platform:

- **Power BI:** Interactive dashboards and visual analytics built from live Dynamics 365 business data.
- **Power Automate:** Workflow automation and approval processes across Dynamics 365 and connected systems.
- **Power Apps:** Low-code application development powered by Dataverse, enabling citizen developers to build business applications alongside professional developers.
- **Copilot / AI Builder:** AI capabilities embedded across Dynamics 365 for predictive forecasting, intelligent recommendations, and automated responses.

### APIs and Integration

- **Web API (OData RESTful):** The primary integration interface for non-.NET applications and cross-platform communication.
- **SDK Assemblies:** For .NET-based integrations, plugins, and custom workflow activities.
- **Azure Service Bus / Event Grid:** For event-driven and asynchronous integration patterns.
- **Dual-write:** Real-time synchronisation between Dynamics 365 Finance/SCM and Dataverse.

## Moving CAPIX Closer to Dynamics 365

Given this technology landscape, there are several strategic directions CAPIX can pursue to align more closely with Dynamics 365:

### Look and Feel

- **Adopt the Fluent UI design system** (Microsoft's open-source UI framework) to give CAPIX a visual identity consistent with Dynamics 365 and the broader Microsoft 365 experience. This would make CAPIX feel native to users already working in the Microsoft ecosystem.
- **Build PCF (PowerApps Component Framework) controls** to embed CAPIX treasury views directly within Dynamics 365 forms and dashboards.

### Integration

- **Integrate with Dataverse** so that CAPIX treasury data (cash positions, forecasts, FX deals, settlements) can be read and written through Dynamics 365's standard data layer. This enables seamless data flow between CAPIX and Dynamics 365 Finance modules.
- **Expose CAPIX functionality as a Web API (OData)** to enable Power Platform tools — Power BI dashboards for treasury analytics, Power Automate flows for payment approvals, and Power Apps for mobile treasury operations.
- **Implement Azure Service Bus integration** for event-driven communication between CAPIX and Dynamics 365, enabling real-time updates for cash movements, settlement confirmations, and accounting postings.

### Architecture and Hosting

- **Migrate CAPIX workloads to Azure** if not already there, aligning with the same cloud infrastructure that Dynamics 365 customers rely on. This simplifies deployment, networking, and security for joint customers.
- **Adopt Azure Active Directory (Entra ID) for authentication**, enabling single sign-on (SSO) between CAPIX and Dynamics 365 so users move seamlessly between applications.
- **Leverage Azure Functions** for lightweight integration tasks such as data transformation, notification triggers, and scheduled reconciliation processes.

### AI and Analytics

- **Integrate with Microsoft Copilot capabilities** to bring AI-assisted treasury insights — such as cash flow predictions, anomaly detection, and natural language querying — into the CAPIX experience, consistent with the AI direction Microsoft is driving across Dynamics 365.
- **Publish CAPIX data to Power BI datasets** to allow treasury teams to build unified dashboards combining Dynamics 365 financial data with CAPIX treasury data.

### Development Practices

- **Standardise on C# / .NET for server-side extensions** and TypeScript for any client-side components, matching the Dynamics 365 development model and making it easier for Dynamics 365 developers to work with CAPIX integrations.
- **Package CAPIX integrations as Dataverse solutions** so they can be deployed and managed using the same lifecycle tools (Power Platform CLI, solution management) that Dynamics 365 administrators already use.

## Web-Enabling CTM and Aligning with Dynamics 365

CTM (CAPIX Treasury Manager) is currently a 64-bit Windows desktop application with a substantial Microsoft Access front-end (~200 forms, ~400 queries, ~200 VBA modules, ~150 local tables) backed by a Microsoft SQL Server database (~200 tables). It also relies on four C++ DLLs for pricing, encryption, and mathematical calculations. Modernising CTM into a web application while simultaneously aligning it with the Dynamics 365 ecosystem requires careful tool selection. The tools below address both goals together.

### Migration and Conversion Tools

#### GAPVelocity AI — Access AI Migrator

https://www.gapvelocity.ai/products/ms-access

GAPVelocity's Access AI Migrator converts Microsoft Access applications (forms, VBA code, queries) directly into C# / Blazor Server web applications. This is the most direct path to both web-enabling CTM and landing on the same technology stack as Dynamics 365.

- **VBA to C# conversion:** Automatically converts VBA modules to clean, idiomatic C# using a hybrid AI approach (agentic AI combined with deterministic semantic pattern matching).
- **Form conversion:** Transforms Access forms into Blazor Server components with modern UI.
- **Database migration:** Converts ADO/DAO data access to Entity Framework Core with optimised queries and proper connection management — ready for Azure SQL Database.
- **Assessment tool (ByteInsight):** Scans the entire VBA codebase to identify dependencies, patterns, and complexity, and produces a detailed migration roadmap with time and cost estimates. This would be a valuable first step to scope the CTM migration.
- **Timeline:** A medium-sized application (150–200K lines of code) can reach engineering-ready status within 3 weeks, with full production-ready in up to 2 months.
- **Dynamics 365 alignment:** The output is C# / Blazor / Entity Framework Core on .NET — exactly the stack used by Dynamics 365 developers, and directly deployable to Azure App Service.

#### fecher accessPORTER — Access to Wisej.NET

https://www.fecher.net/our-services/access-migration/

fecher's accessPORTER is a specialised tool that analyses Access application source code and converts it into a .NET web application using the Wisej.NET framework.

- **Form conversion:** Transforms Access forms into Wisej.NET web forms, preserving layout and behaviour in a browser-based application.
- **VBA to C# conversion:** Translates VBA code and macros to C#, with project-specific mapping rules. Access environment functions without direct .NET equivalents are supplemented via a supplied class library to keep migrated code readable.
- **Report conversion:** Converts Access Reports to DevExpress reporting components, providing a modern web-based reporting capability.
- **Fixed-price delivery:** fecher delivers a turnkey migration for a fixed price based on lines of code and third-party control usage, reducing commercial risk.
- **Dynamics 365 alignment:** The output is C# / .NET running in a browser — close to the Dynamics 365 development model, though Wisej.NET is a proprietary framework rather than the open Blazor standard.

#### Microsoft Power Apps + Dataverse — Built-in Access Migration

https://learn.microsoft.com/en-us/power-apps/maker/data-platform/migrate-access-to-dataverse

Microsoft provides a native, fully supported migration path from Access directly into the Dynamics 365 ecosystem via Power Apps and Dataverse.

- **Export to Dataverse wizard:** Built into Access under External Data, this tool connects to Dataverse and guides you through table selection, data validation, and export. CTM's ~150 local tables and SQL Server data could be migrated to Dataverse tables.
- **Power Apps front-end:** Once data is in Dataverse, Power Apps (canvas or model-driven) can replace Access forms with web and mobile interfaces. Model-driven apps in particular share the same look and feel as Dynamics 365.
- **Security and compliance:** Dataverse provides role-based security, audit logging, and Azure AD authentication — addressing the security limitations of Access (which stores passwords in plain text and lacks modern audit controls).
- **Dynamics 365 alignment:** This is the strongest alignment option because CTM data would live directly in Dataverse, the same data platform as Dynamics 365. Treasury data would be immediately accessible to Dynamics 365 Finance modules, Power BI, Power Automate, and Copilot.
- **Limitation:** Power Apps is a low-code platform. CTM's ~200 VBA modules of complex treasury business logic (deal capture, cash forecasting, pricing calculations) may exceed what Power Apps can handle natively, requiring supplementary C# plugins or Azure Functions for the heavy lifting.

### Recommended Development Frameworks

#### Blazor Server (.NET)

https://learn.microsoft.com/en-us/aspnet/core/blazor/

Blazor Server is the strongest candidate framework for rebuilding CTM's user interface, regardless of which migration tool is used.

- **C# end-to-end:** UI logic, business logic, and data access all written in C# — the same language as Dynamics 365 server-side development. No need for separate JavaScript expertise.
- **Fluent UI Blazor components:** Microsoft's open-source Fluent UI Blazor library provides components that match the Dynamics 365 visual style, giving CTM a native Microsoft look and feel.
- **SignalR real-time updates:** Blazor Server uses SignalR for real-time UI updates over a persistent connection — suitable for CTM's deal capture and live cash position screens.
- **C++ DLL interop:** Blazor Server runs on the server, so CTM's four C++ DLLs (pricing, encryption, maths) can be called via P/Invoke from the server-side .NET process. This preserves the existing calculation engines without rewriting them.
- **Azure App Service hosting:** Deploys directly to Azure App Service (Windows), aligning with Dynamics 365 infrastructure and enabling Entra ID (Azure AD) single sign-on.

#### Entity Framework Core + Azure SQL Database

CTM's SQL Server database (~200 tables) should be migrated to Azure SQL Database, accessed via Entity Framework Core.

- **Azure SQL Database** is the same database technology underlying Dataverse. Moving CTM's data to Azure SQL positions it for future Dataverse integration via virtual tables or dual-write synchronisation.
- **Entity Framework Core** replaces the ODBC linked tables and JET SQL queries currently used in Access, providing a modern, strongly-typed data access layer in C#.
- **Dynamics 365 alignment:** Azure SQL + EF Core is the standard data access pattern for .NET applications in the Dynamics 365 ecosystem.

### Reporting Replacements

CTM currently uses Microsoft Access Reports. Web-based replacements that align with the Dynamics 365 ecosystem include:

- **Power BI Embedded:** Embed interactive Power BI reports directly in the CTM web application. Power BI is the standard reporting tool across Dynamics 365.
- **SQL Server Reporting Services (SSRS):** For paginated, print-ready reports (deal confirmations, regulatory reports). SSRS integrates with Azure SQL and can be embedded in Blazor applications.
- **DevExpress Reporting for .NET:** A commercial option that closely mirrors the Access Reports development experience, making it a natural fit for migrated reports. This is the tool used by fecher's accessPORTER.

### Integration and Middleware Tools

To connect the web-enabled CTM with Dynamics 365 and external systems:

- **Azure Functions:** Serverless C# functions for lightweight integrations — SWIFT message processing, Reuters/Bloomberg pricing feeds, ERP data exchange, and scheduled reconciliation jobs.
- **Azure Service Bus:** Message queuing for reliable, asynchronous communication between CTM and Dynamics 365 — cash movements, settlement confirmations, and accounting postings.
- **Azure API Management:** Expose CTM treasury services as managed OData/REST APIs that Dynamics 365, Power Platform, and third-party systems can consume.
- **Power Automate connectors:** Build custom connectors so that CTM treasury operations (payment approvals, deal authorisations) can be triggered from Dynamics 365 workflows.

### AI-Assisted Migration Tools

#### GitHub Copilot App Modernization (Visual Studio)

Microsoft's GitHub Copilot now includes app modernization capabilities directly in Visual Studio, which can accelerate the CTM migration.

- **AI-powered code transformation:** Assists with converting VBA patterns to modern C# equivalents, reducing manual translation effort.
- **Azure migration guidance:** Provides automated remediation and containerisation support for deploying to Azure.
- **CVE scanning:** Identifies security vulnerabilities introduced during migration.
- **Microsoft claims** this tooling can reduce migration effort by up to 70% and cut upgrade time in half through automated code transformations.

#### Azure Migrate

https://learn.microsoft.com/en-us/azure/migrate/

Azure Migrate provides assessment and migration tooling for moving on-premises workloads (including SQL Server databases and .NET applications) to Azure, and would support the infrastructure side of the CTM migration.

### Suggested Approach

A practical path that achieves both web-enablement and Dynamics 365 alignment:

1. **Assess** — Run GAPVelocity ByteInsight against the CTM Access application to produce a detailed migration roadmap and effort estimate.
2. **Migrate the database** — Move the SQL Server database to Azure SQL Database using Azure Migrate. Redesign the ~150 local Access tables as server-side temporary/staging tables.
3. **Convert the front-end** — Use GAPVelocity Access AI Migrator or fecher accessPORTER to convert Access forms and VBA to C# / Blazor Server. Apply Fluent UI Blazor components for a Dynamics 365-consistent look and feel.
4. **Wrap the C++ DLLs** — Retain the four C++ DLLs and call them via P/Invoke from the Blazor Server process running on Azure App Service (Windows).
5. **Replace reports** — Migrate Access Reports to Power BI Embedded (interactive) and SSRS (paginated/print).
6. **Add Dynamics 365 integration** — Expose CTM data via OData APIs, implement Azure Service Bus for event-driven sync, and create Power Automate connectors and Power BI datasets for treasury data.
7. **Authenticate with Entra ID** — Replace Windows/AD authentication with Azure AD (Entra ID) for single sign-on across CTM and Dynamics 365.

