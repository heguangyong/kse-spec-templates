---
name: Moqui Domain Extension
category: domain-modeling
description: Template for extending Moqui's existing data model and REST API services for industry-specific business domains. Leverages Moqui Entity Engine, generic CRUD API, and Service Invocation API as the foundation.
difficulty: intermediate
tags:
  - moqui
  - domain-extension
  - entity-engine
  - rest-api
  - data-model
  - business-process
  - industry-specific
applicable_scenarios:
  - Extending Moqui ERP for industry-specific needs (exhibition, manufacturing, logistics, etc.)
  - Building business features on top of Moqui's existing entity model
  - Reusing Moqui REST API services while adding domain-specific logic
  - Mapping industry requirements to Moqui WorkEffort, Party, Facility entities
author: FallingAKS
created_at: 2026-02-11
updated_at: 2026-02-11
version: 1.0.0
---

# Requirements Document: {{SPEC_NAME_TITLE}}

## Introduction

<!-- Describe the industry domain and what business capability you are building -->
<!-- Example: "This Spec extends Moqui's project management capabilities for the exhibition industry, covering exhibition project lifecycle, booth management, exhibitor registration, and event scheduling." -->

This Spec extends Moqui's existing data model and REST API services to support {{INDUSTRY_DOMAIN}} business requirements. The approach is **reuse-first**: leverage Moqui's proven entities (WorkEffort, Party, Facility, etc.) and generic REST APIs before creating any new components.

## Glossary

<!-- Define industry-specific terms AND map them to Moqui concepts -->
<!-- Example:
- **Exhibition Project**: An event management project → maps to Moqui `WorkEffort` (type: WetProject)
- **Booth**: A physical space allocated to exhibitors → maps to new entity `ExhibitionBooth` (extends Facility concept)
- **Exhibitor**: A company participating in an exhibition → maps to Moqui `Party` (type: PtOrganization) with role "Exhibitor"
- **Event Schedule**: Time slots within an exhibition → maps to Moqui `WorkEffort` (type: WetEvent) under project
-->

- **{{DOMAIN_TERM_1}}**: {{Definition}} → maps to Moqui `{{ENTITY_OR_NEW}}`
- **{{DOMAIN_TERM_2}}**: {{Definition}} → maps to Moqui `{{ENTITY_OR_NEW}}`
- **{{DOMAIN_TERM_3}}**: {{Definition}} → maps to Moqui `{{ENTITY_OR_NEW}}`

## Pre-Analysis: Moqui Asset Discovery

<!-- CRITICAL: Before defining requirements, discover what Moqui already provides -->
<!-- Run these commands and document the results: -->
<!-- kse scene discover -t entities → list relevant existing entities -->
<!-- kse scene discover -t services → list relevant existing services -->

### Existing Moqui Entities (Reusable)

<!-- Example:
| Moqui Entity | Package | Domain Mapping | Reuse Strategy |
|--------------|---------|----------------|----------------|
| WorkEffort | mantle.work.effort | Project, Task, Milestone, Event | Direct reuse with type enum filtering |
| Party | mantle.party | Exhibitor, Organizer, Vendor | Direct reuse with role assignment |
| Facility | mantle.facility | Venue, Hall | Direct reuse |
| WorkEffortParty | mantle.work.effort | Team assignment | Direct reuse |
| WorkEffortContent | mantle.work.effort | Project documents | Direct reuse |
| ContactMech | mantle.party.contact | Exhibitor contact info | Direct reuse |
-->

| Moqui Entity | Package | Domain Mapping | Reuse Strategy |
|--------------|---------|----------------|----------------|
| {{ENTITY}} | {{PACKAGE}} | {{DOMAIN_CONCEPT}} | {{STRATEGY}} |

### Existing Moqui Services (Reusable)

<!-- Example:
| Service Name | Description | Domain Usage | Reuse Strategy |
|-------------|-------------|--------------|----------------|
| mantle.work.WorkEffortServices.create#WorkEffort | Create work effort | Create project/task/event | Direct invoke via /api/v1/services/ |
| mantle.work.WorkEffortServices.update#WorkEffort | Update work effort | Update project status | Direct invoke via /api/v1/services/ |
| mantle.party.PartyServices.create#Organization | Create organization | Register exhibitor | Direct invoke via /api/v1/services/ |
-->

| Service Name | Description | Domain Usage | Reuse Strategy |
|-------------|-------------|--------------|----------------|
| {{SERVICE}} | {{DESCRIPTION}} | {{DOMAIN_USAGE}} | {{STRATEGY}} |

### Existing REST API Endpoints (Reusable)

<!-- These generic endpoints already work for ANY Moqui entity: -->
<!-- 
| Endpoint | Method | Description |
|----------|--------|-------------|
| /api/v1/entities/{entityName} | GET | List entities with filtering, pagination, sorting |
| /api/v1/entities/{entityName}/{id} | GET | Get single entity by ID |
| /api/v1/entities/{entityName} | POST | Create entity |
| /api/v1/entities/{entityName}/{id} | PUT | Update entity |
| /api/v1/entities/{entityName}/{id} | DELETE | Delete entity |
| /api/v1/entities/{entityName}/{id}/related/{relationship} | GET | List related entities |
| /api/v1/entities/{entityName}/batch | POST | Batch CRUD operations |
| /api/v1/services/{serviceName} | POST | Invoke any Moqui service |
-->

### Gap Analysis: What Moqui Does NOT Provide

<!-- After discovering existing assets, identify what's missing for your domain -->
<!-- Example:
| Gap | Description | Solution |
|-----|-------------|----------|
| Exhibition-specific entity | No entity for booth layout/allocation | New entity: ExhibitionBooth |
| Booth allocation rules | No service for booth assignment with conflict detection | New service: ExhibitionBoothService |
| Exhibition dashboard | No aggregation API for exhibition KPIs | New controller endpoint |
| Exhibitor registration workflow | No multi-step registration with approval | New service with state machine |
-->

| Gap | Description | Solution |
|-----|-------------|----------|
| {{GAP}} | {{DESCRIPTION}} | {{SOLUTION}} |

## Requirements

### Requirement 1: Reuse Moqui Entities for Core Domain

**User Story:** As a {{ROLE}}, I want to use Moqui's existing entities to represent core {{DOMAIN}} concepts, so that I benefit from the proven data model and existing CRUD APIs without reimplementation.

#### Acceptance Criteria

<!-- Define how existing entities map to domain concepts -->
<!-- Example:
1. THE system SHALL use WorkEffort (type=WetProject) to represent Exhibition Projects
2. THE system SHALL use WorkEffort (type=WetTask) to represent Project Tasks
3. THE system SHALL use WorkEffort (type=WetMilestone) to represent Project Milestones
4. THE system SHALL use WorkEffort (type=WetEvent) to represent Exhibition Events/Schedules
5. THE system SHALL use Party (type=PtOrganization, role=Exhibitor) to represent Exhibitors
6. THE system SHALL use Facility to represent Exhibition Venues
7. THE system SHALL use WorkEffortParty to represent team member assignments
8. ALL existing CRUD operations via /api/v1/entities/ SHALL work for these mapped entities without modification
-->

1. THE system SHALL use {{MOQUI_ENTITY}} to represent {{DOMAIN_CONCEPT}}
2. ALL existing CRUD operations via `/api/v1/entities/` SHALL work for mapped entities without modification

### Requirement 2: Reuse Moqui Services for Business Operations

**User Story:** As a {{ROLE}}, I want to invoke Moqui's existing services for standard business operations, so that I reuse proven business logic.

#### Acceptance Criteria

<!-- Define which existing services to reuse -->
<!-- Example:
1. THE system SHALL invoke mantle.work.WorkEffortServices.create#WorkEffort via /api/v1/services/ to create projects
2. THE system SHALL invoke mantle.work.WorkEffortServices.update#WorkEffort via /api/v1/services/ to update project status
3. THE system SHALL use Moqui's built-in status flow transitions for WorkEffort lifecycle management
4. THE system SHALL invoke mantle.party.PartyServices.create#Organization via /api/v1/services/ to register exhibitors
-->

1. THE system SHALL invoke {{SERVICE_NAME}} via `/api/v1/services/` to {{OPERATION}}
2. THE system SHALL use Moqui's built-in status flow transitions for {{ENTITY}} lifecycle management

### Requirement 3: New Domain-Specific Entities

**User Story:** As a {{ROLE}}, I want domain-specific entities for concepts that Moqui does not natively support, so that the system accurately models {{DOMAIN}} business requirements.

#### Acceptance Criteria

<!-- Only define NEW entities for gaps identified in pre-analysis -->
<!-- Example:
1. THE system SHALL define a new ExhibitionBooth entity with: id, exhibitionId (FK→WorkEffort), boothNumber, size, location, price, status, exhibitorId (FK→Party)
2. THE system SHALL define a new ExhibitorRegistration entity with: id, exhibitionId (FK→WorkEffort), exhibitorId (FK→Party), status, applicationDate, approvalDate, contractId
3. New entities SHALL be defined as Moqui Entity XML definitions in runtime/component/
4. New entities SHALL be automatically accessible via /api/v1/entities/ generic CRUD API
-->

1. THE system SHALL define a new {{ENTITY}} entity with: {{FIELDS}}
2. New entities SHALL be defined as Moqui Entity XML definitions in `runtime/component/`
3. New entities SHALL be automatically accessible via `/api/v1/entities/` generic CRUD API

### Requirement 4: New Domain-Specific Services

**User Story:** As a {{ROLE}}, I want domain-specific business logic services for operations that go beyond simple CRUD, so that complex business rules are properly enforced.

#### Acceptance Criteria

<!-- Only define NEW services for business logic gaps -->
<!-- Example:
1. THE system SHALL provide a booth allocation service that checks availability, prevents conflicts, and assigns booths to exhibitors
2. THE system SHALL provide an exhibitor registration workflow service with states: SUBMITTED → REVIEWING → APPROVED/REJECTED
3. THE system SHALL provide an exhibition dashboard service that aggregates: booth utilization, exhibitor count, revenue, task completion
4. New services SHALL be implemented as Java service classes invokable via /api/v1/services/
-->

1. THE system SHALL provide a {{SERVICE}} that {{BUSINESS_LOGIC}}
2. New services SHALL be implemented as Java service classes invokable via `/api/v1/services/`

### Requirement 5: Domain-Specific Business Rules

**User Story:** As a {{ROLE}}, I want business rules specific to {{DOMAIN}} enforced by the system, so that data integrity and business constraints are maintained.

#### Acceptance Criteria

<!-- Example:
1. THE system SHALL NOT allow booth allocation when exhibition WorkEffort status is WeComplete or WeClosed
2. THE system SHALL enforce that booth count does not exceed venue Facility capacity
3. THE system SHALL prevent date overlap between exhibitions at the same Facility
4. THE system SHALL validate exhibitor registration only when exhibition status is WeInPlanning or WeApproved
-->

1. THE system SHALL {{BUSINESS_RULE}}
2. THE system SHALL NOT {{CONSTRAINT}}

## Non-Functional Requirements

### Same-Domain Language Consistency (同域语言一致性)
1. Within the same business domain, all backend services SHALL use the same implementation language as the project's existing technology stack
2. If the project is based on Moqui/Java, all domain extension services SHALL be implemented in Java
3. Cross-language service integration (e.g., Java + Python) SHALL only be used for completely independent business domains that communicate asynchronously (e.g., message queues) and do NOT require strong transactional consistency
4. The rationale: within a single process/language, database transactions provide native ACID guarantees; cross-language services require distributed transaction patterns (Saga, eventual consistency) which add significant complexity and risk
5. If the project requires AI/ML capabilities typically implemented in Python, those SHALL be isolated as independent microservices communicating via async messaging, NOT as part of the core business domain transaction flow

### Moqui Compatibility
1. All new entities SHALL follow Moqui Entity XML definition format
2. All new services SHALL be registered in Moqui's service definition files
3. New entities SHALL integrate with Moqui's Entity Engine (transactions, caching, audit)
4. New services SHALL use Moqui's ExecutionContext for security and transaction management

### API Consistency
1. New domain endpoints SHALL follow the same response format as existing generic APIs
2. New entities SHALL be discoverable via `kse scene discover -t entities`
3. New services SHALL be discoverable via `kse scene discover -t services`

### Data Integrity
1. Foreign keys to Moqui entities (WorkEffort, Party, Facility) SHALL enforce referential integrity
2. New enum types SHALL be registered in Moqui's Enumeration system

## Out of Scope

<!-- Example:
- Frontend UI implementation (separate Spec using frontend templates)
- Payment/billing integration (separate Spec)
- Email notification system (separate Spec)
- Mobile app (separate Spec)
-->

- {{OUT_OF_SCOPE_1}}
- {{OUT_OF_SCOPE_2}}
