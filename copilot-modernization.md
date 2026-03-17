# Using Microsoft Copilot for Application Modernization

Microsoft has positioned GitHub Copilot as a central tool for modernizing legacy applications, including the migration of desktop and on-premises software to modern web-based, cloud-hosted architectures. This document explores how Copilot can be used to accelerate the modernization of CAPIX applications — particularly the migration of CTM from Microsoft Access to a modern .NET web application aligned with Dynamics 365.

## What Is GitHub Copilot App Modernization?

GitHub Copilot app modernization is a Copilot agent that upgrades .NET projects to newer versions and migrates applications to Azure. It is available across Visual Studio, Visual Studio Code, GitHub Copilot CLI, and GitHub.com.

https://learn.microsoft.com/en-us/dotnet/core/porting/github-copilot-app-modernization/overview

The agent guides developers through a structured **Assess → Plan → Execute** workflow:

1. **Assessment** — Copilot examines the project structure, dependencies, and code patterns. It produces an `assessment.md` file listing breaking changes, API compatibility problems, deprecated patterns, and the scope of work.
2. **Planning** — Copilot converts the assessment into a detailed `plan.md` specification explaining how to resolve every identified issue, including upgrade strategies, refactoring approaches, dependency paths, and risk mitigations.
3. **Execution** — Copilot breaks the plan into sequential, concrete tasks (`tasks.md`), each with validation criteria. It then applies the changes automatically, creating a Git commit for every step so progress can be reviewed and rolled back if needed.

Each stage produces a Markdown file under `.github/upgrades` in the repository, so the developer can review and modify the plan before proceeding.

Microsoft claims this tooling can **reduce migration effort by up to 70%** and **cut upgrade time in half** through automated code transformations and intelligent remediation.

## Key Capabilities

### .NET Project Upgrades

The modernization agent supports upgrading C# projects of the following types:

- ASP.NET Core (MVC, Razor Pages, Web API)
- Blazor
- Azure Functions
- Windows Presentation Foundation (WPF)
- Windows Forms
- Class libraries
- Console applications

It handles upgrades from older .NET versions to the latest, and from .NET Framework to modern .NET — including the modernization of legacy code patterns to current equivalents.

### Azure Migration

Copilot provides predefined migration tasks that cover common Azure migration scenarios:

- **Database migration** — Migrate from on-premises SQL Server (or DB2, Oracle) to Azure SQL Database, Azure SQL Managed Instance, or Azure PostgreSQL, using secure managed identity authentication.
- **Authentication** — Transition from Windows Active Directory to Microsoft Entra ID (Azure AD) for modern identity management.
- **Secrets management** — Replace plaintext credentials in configuration or code with Azure Key Vault and managed identities.
- **File storage** — Move local file I/O to Azure Blob Storage or Azure File Storage.
- **Messaging** — Migrate from MSMQ or RabbitMQ to Azure Service Bus.
- **Email** — Replace direct SMTP with Azure Communication Services.
- **Event streaming** — Transition from on-premises Kafka to Azure Event Hubs or Confluent Cloud.
- **Observability** — Migrate from log4net, Serilog, or Windows Event Log to OpenTelemetry on Azure.
- **Caching** — Replace local Redis with Azure Cache for Redis using managed identity.

### Security Scanning

During execution, Copilot automatically identifies and addresses Common Vulnerabilities and Exposures (CVEs), ensuring the modernized application meets current security standards.

### Containerisation and Deployment

Copilot supports containerisation workflows and deployment to Azure, taking code from development to production as part of the migration process.

## VBA and Access Modernization with Copilot

While the formal Copilot modernization agent targets .NET projects, GitHub Copilot (the general AI coding assistant) has proven highly effective for modernizing Microsoft Access applications — directly relevant to the CTM migration.

### VBA to Modern Code Translation

Copilot can translate VBA business logic into modern language equivalents. In a documented case study by Microsoft's Azure Architecture team, Copilot successfully:

- Translated VBA business logic methods into modern service code.
- Generated unit tests for each translated method — a quality assurance layer that did not exist in the original Access application.
- Applied meaningful naming conventions and automated documentation to the migrated codebase.

https://techcommunity.microsoft.com/blog/azurearchitectureblog/how-to-modernise-a-microsoft-access-database-forms--vba-to-node-js-openapi-and-s/4473504

### Screenshot-Based Form Recreation

One of the most innovative uses of Copilot for Access modernization is its image recognition capability. Developers can capture screenshots of existing Access forms and use them as prompts. Copilot then generates modern web UI views that closely mirror the original application layout while incorporating modern accessibility features.

This approach is particularly valuable for CTM because:

- CTM has approximately 200 Access forms, and manually specifying each form's layout for recreation would be extremely time-consuming.
- Users are familiar with the existing form layouts, so preserving them minimises retraining.
- Copilot can apply modern accessibility standards (WCAG) during recreation, which Access forms do not support.

### Database Assistance

In the same case study, Copilot assisted with database modernization by batch-renaming confusing foreign key constraints and generating API layer code using repository patterns — tasks that would be relevant when migrating CTM's ~200 SQL Server tables to Azure SQL Database.

### Demonstrated Results

The Microsoft case study reported that an Access application modernization completed in approximately **two weeks** versus an estimated **six to eight months** using traditional manual methods — a dramatic acceleration attributable to Copilot-assisted development.

## The Modernize CLI — Enterprise-Scale Modernization

For organisations modernizing multiple applications, Microsoft provides the Modernize CLI, a command-line tool that orchestrates modernization workflows at scale.

https://learn.microsoft.com/en-us/azure/developer/github-copilot-app-modernization/modernization-agent/overview

Key capabilities include:

- **Multi-repository assessment** — Assess multiple applications and repositories simultaneously, generating cloud readiness scores and dependency maps.
- **Batch operations** — Execute modernization workflows across an entire application portfolio in non-interactive mode.
- **CI/CD integration** — Embed modernization into automated delivery pipelines for headless execution.
- **Customisable skills** — Define organisation-specific migration patterns, internal library standards, and coding conventions as reusable skills that are applied consistently across all modernized applications.
- **Interactive and non-interactive modes** — Switch between hands-on interactive workflows (for complex, decision-intensive scenarios) and fully automated batch execution.

## How Copilot Could Accelerate the CTM Modernization

Applying Copilot to the CTM migration could address several of the most labour-intensive aspects of the project:

### 1. VBA Module Translation (~200 modules)

Copilot can assist with translating CTM's ~200 VBA code modules to C#. While automated migration tools like GAPVelocity and accessPORTER handle bulk conversion, Copilot adds value by:

- Refactoring converted code to use modern C# idioms and patterns rather than literal VBA translations.
- Generating unit tests for each translated module, creating a test suite that does not exist today.
- Identifying edge cases and undocumented business logic embedded in VBA workarounds.

### 2. Access Form Recreation (~200 forms)

Using Copilot's screenshot-based approach:

- Capture screenshots of each of CTM's ~200 Access forms.
- Prompt Copilot to generate Blazor Server components (with Fluent UI styling) that replicate the layout.
- Review and refine the generated components, connecting them to the migrated C# business logic and Entity Framework Core data access layer.

This approach preserves the user experience that treasury operators are accustomed to while delivering a modern, browser-based interface.

### 3. Query Migration (~400 queries)

CTM's ~400 JET SQL queries (accessing both local Access tables and remote SQL Server data via ODBC) need to be converted to Entity Framework Core LINQ queries or Azure SQL-compatible T-SQL. Copilot can:

- Translate JET SQL syntax to standard T-SQL, handling Access-specific functions and join patterns.
- Generate Entity Framework Core LINQ equivalents where appropriate.
- Identify queries that rely on Access-specific behaviour (such as local table joins to remote tables) and flag them for architectural redesign.

### 4. Azure Migration Tasks

Once CTM is running as a .NET application, the Copilot modernization agent's predefined Azure migration tasks directly apply:

- **SQL Server → Azure SQL Database** with managed identity authentication.
- **Windows AD → Entra ID** for single sign-on with Dynamics 365.
- **Plaintext credentials → Azure Key Vault** for secrets management.
- **Local file operations → Azure Blob Storage** for document storage.
- **MSMQ or direct integrations → Azure Service Bus** for messaging with Dynamics 365 and banking systems.
- **Logging → OpenTelemetry on Azure** for cloud-native observability.

### 5. Report Migration

Copilot can assist with translating Access Report definitions into Power BI report specifications or SSRS report definitions, generating the boilerplate layout and data binding code that would otherwise be created manually.

### 6. Test Generation

One of Copilot's strongest capabilities is automated test generation. CTM currently has no automated test suite. During migration, Copilot can generate:

- Unit tests for each translated VBA module / C# class.
- Integration tests for data access methods.
- UI tests for Blazor components based on the original Access form specifications.

This creates a safety net that validates the migration preserves existing behaviour — critical for a financial application where calculation accuracy is non-negotiable.

## Prerequisites and Licensing

To use GitHub Copilot modernization:

- **Visual Studio 2022 (17.14.16+) or Visual Studio 2026** — The modernization agent is built into the IDE.
- **Visual Studio Code** — Via the GitHub Copilot modernization for .NET extension.
- **GitHub Copilot subscription** — Required for all Copilot features. Business or Enterprise plans are recommended for commercial use.
- **Modernize CLI** — Available as a separate download for enterprise-scale and CI/CD scenarios.

Note: The legacy .NET Upgrade Assistant has been officially deprecated by Microsoft and replaced by GitHub Copilot app modernization.

## Summary

GitHub Copilot offers a practical, AI-accelerated path to modernizing CTM — from translating VBA to C#, recreating Access forms as Blazor components using screenshots, migrating queries, generating tests, and handling the Azure infrastructure migration. Combined with dedicated migration tools (GAPVelocity, fecher accessPORTER), Copilot can significantly reduce the time, risk, and manual effort involved in transforming CTM from a desktop Access application into a cloud-hosted, Dynamics 365-aligned web application.
