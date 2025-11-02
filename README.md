# AI Infused SDLC
---
### Agenda

| **#**   	| **Phase**         | **Objective**                        	|
| ----------| ----------------- | ------------------------------------- |
| 1         | Intro             | Set Context & Scope                  	|
| 2         | Requirements      | Convert Vision → Backlog            	| 
| 3         | Design            | Create Architecture & API contracts  	|
| 4         | Implementation    | Build APIs & UI                      	|
| 5         | Testing           | Unit + Regression Automation         	|
| 6         | Maintenance       | Bug Fixes, Q&A, Refactoring           |

**Mock Screens**

![Tenant Registration](https://raw.githubusercontent.com/technocratt/copilot-demo/refs/heads/main/Tenant%20Registration.png)

![Publish Patient Health Details](https://raw.githubusercontent.com/technocratt/copilot-demo/refs/heads/main/Publish%20Patient%20Health%20Details.png)

---

### 1. Intro

### About: Multi Tenant Healthcare App

This app is a **multi-tenant healthcare platform** that allows hospitals and clinics to register and manage patient health data.

**Tenant Registration:**
- Each hospital or clinic registers as a tenant and receives a unique API key.
- This key allows secure submission of health data.

**Medical Information Submission:**
- Tenants use the key to post patient health records via APIs or the Blazor web interface.

**Data Model:**

| **Category**              | **Fields**                                                                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Patient Basic Details** | Name, Patient ID, Gender, Date of Birth                                                                                                  |
| **General Stats**         | Height (cm), Weight (kg), BMI (auto-calculated)                                                                                          |
| **Vitals**                | Pulse (bpm), Blood Pressure (systolic/diastolic), SPO₂ (%), Body Temperature (°C), Respiratory Rate (breaths/min), Blood Glucose (mg/dL) |

**Scope:**

| **Component**       | **Description**                                  | **Technology**                         |
| ------------------- | ------------------------------------------------ | -------------------------------------- |
| **Tenant API**      | Handles registration & API key generation        | .NET 9 Web API                         |
| **Health Data API** | Accepts patient records, validates & stores data | .NET 9 Web API, EF Core, SQL Server    |
| **Database**        | Stores tenants, patients, and vitals             | Microsoft SQL Server                   |
| **Web UI**          | Tenant dashboard to manage and post data         | Blazor Server (MAUI?)                  |
| **Testing Suite**   | Regression & unit tests                          | WebDriverIO, xUnit                     |

---

### 2. Requirements: Vision to Backlog
### 2.1 Vision to Epics

**🧭 Prompt: Generate Epics for Healthcare App**

Context:
We are building a multi-tenant healthcare application using .NET 9, C#, SQL Server, and Blazor Server.
Each tenant (hospital or clinic) can register in the system and receives a unique API key.
Using this key, the tenant can post and manage patient medical information such as basic details (Name, ID, Gender, DOB), general stats (height, weight, BMI), and vital signs (pulse, BP, SPO₂, body temperature, respiratory rate, blood glucose).

The application will expose RESTful APIs for tenant registration and patient data management, and provide a Blazor web interface for viewing and submitting this information.

Our goal is to define high-level "Epics" that represent major deliverables in the software development backlog.

Expectations:
- Identify 4–6 major Epics that logically cover the system’s end-to-end functionality.
- Each Epic should include:
-- Epic Name
-- Epic Description (2–3 lines) — what business or technical capability it delivers
-- Business Value — why it matters to the tenant or system
- Keep the language clear, professional, and aligned with agile SDLC conventions.
- Do not break down into user stories or tasks yet, just provide Epics.

**🧭 Prompt: Generate User Stories from a Given Epic**

Context:
We are building a multi-tenant healthcare application using .NET 9, C#, SQL Server, and Blazor Server.
Each tenant (hospital or clinic) can register in the system and receives a unique API key.
Using this key, the tenant can post and manage patient medical information such as basic details (Name, ID, Gender, DOB), general stats (height, weight, BMI), and vital signs (pulse, BP, SPO₂, body temperature, respiratory rate, blood glucose).

The application will expose RESTful APIs for tenant registration and patient data management, and provide a Blazor web interface for viewing and submitting this information.

Each Epic represents a major feature area in this system, such as tenant registration, data submission, authentication, or analytics. Your task is to create detailed "User Stories" for the Epic provided below.

Epic Provided:

Epic 1: Tenant Onboarding & API Key Management
Description: Self-service tenant registration, verification, and automated issuance/rotation of unique API keys. Includes tenant profile management and admin controls for approval, suspension, and quota assignment.
Business Value: Enables rapid, secure onboarding of hospitals/clinics and ensures each tenant is uniquely identifiable and manageable.

Expectations:

- Generate 4–6 User Stories for this Epic.
- Each story should follow this format:
-- Story ID (e.g., US1.1, US1.2, etc.)
-- Title: Short and clear.
-- As a [role], I want [goal], so that [benefit].
-- Acceptance Criteria: List 3–5 bullet points using Gherkin-style or bullet format (“Given-When-Then” or plain statements).
- Keep language clear, customer-focused, and aligned with Agile conventions.
- Avoid technical implementation details; focus on user-facing or functional intent.
- Output should be in markdown format for easy readability.

---
### 3. Design: Create Architecture & API contracts
**🧭 Prompt: Generate API Contract Document – Tenant Registration**

Context:
We are building a multi-tenant healthcare application using .NET 9, C#, SQL Server, and Blazor Server.
Each tenant (hospital or clinic) can register in the system and receives a unique API key.
Using this key, the tenant can post and manage patient medical information such as basic details (Name, ID, Gender, DOB), general stats (height, weight, BMI), and vital signs (pulse, BP, SPO₂, body temperature, respiratory rate, blood glucose).

The application will expose RESTful APIs for tenant registration and patient data management, and provide a Blazor web interface for viewing and submitting this information.

Your task is to generate a formal API contract document for the Tenant Registration module. Create the document in a markdown file named "TenantRegistrationAPI.md".

Functional Description:
- Tenants can register with organization details (name, contact person, email, phone number).
- System should validate the input and ensure no duplicate tenants exist.
- Upon successful registration, the system will generate and return:
-- A unique Tenant ID (GUID).
-- A unique API Key (string).
Registration timestamp and status.
- API should support both creation (POST) and retrieval (GET) of tenant information.
- Response and error messages must be structured and standardized (HTTP status codes, messages, etc.).

Expectations:
- Generate a complete API Contract Document in Markdown format.
- Include the following sections clearly:
-- API Overview (Purpose and high-level behavior)
-- Base URL (with placeholder, e.g., /api/tenants)
-- Endpoints Table (list of all relevant endpoints and methods)
-- Detailed Endpoint Specifications:
    - Endpoint path and HTTP method
    - Request headers (e.g., Content-Type, Authorization if needed)
    - Request body schema (with field names, types, required/optional)
    - Example request payload (JSON)
    - Response schema (success and error)
    - Example success and error responses (with status codes)
    - Validation Rules (business-level and data-level validations)
    - Error Handling & Standard Response Format
- Keep the tone developer-friendly and precise, similar to a real API specification used in enterprise documentation.
- Format the final output neatly using Markdown code blocks for JSON payloads.

---
### 4. Implementation: Build APIs & UI
**🧭 Prompt: Generate Backend API Solution from API Documentation**

The Markdown file (TenantRegistrationAPI.md) contains the detailed API contract for the Tenant Registration module — including endpoints, request/response schemas, and validation rules.

Your task is to read and interpret that document, and implementing them in the current code base. Use best practices and standards as applicable.

---

### 5. Testing: Unit + Regression automation
**🧭 Prompt: Generate xUnit Tests for TenantController**

- Write xUnit test cases for the TenantController.
- Install dependencies as required (xunit, moq etc).
- Include test methods for all success and failure (validations) scenarios.

---

### 6. Maintenance: Bug Fixes, Q&A, Refactoring
Ad-hoc demos

---
