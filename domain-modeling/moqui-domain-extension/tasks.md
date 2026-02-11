---
name: Moqui Domain Extension
category: domain-modeling
description: Template for extending Moqui's existing data model and REST API services for industry-specific business domains.
difficulty: intermediate
tags:
  - moqui
  - domain-extension
  - entity-engine
  - rest-api
  - data-model
author: FallingAKS
created_at: 2026-02-11
updated_at: 2026-02-11
version: 1.0.0
---

# Implementation Tasks: {{SPEC_NAME_TITLE}}

## Overview

This task list implements the Moqui domain extension. The approach is reuse-first: verify existing APIs work for domain needs, then add only what's missing.

**Key principle:** Every new entity XML definition is automatically accessible via the generic CRUD API — no controller/service code needed for basic CRUD.

## Phase 1: Discovery and Verification

- [ ] 1. Verify Moqui asset reusability
  - [ ] 1.1 Run `kse scene discover -t entities` and document entities relevant to {{DOMAIN}}
  - [ ] 1.2 Run `kse scene discover -t services` and document services relevant to {{DOMAIN}}
  - [ ] 1.3 Test generic CRUD API for reused entities (e.g., `GET /api/v1/entities/WorkEffort?workEffortTypeEnumId=WetProject`)
  - [ ] 1.4 Test generic Service API for reused services (e.g., `POST /api/v1/services/mantle.work.WorkEffortServices.create#WorkEffort`)
  - [ ] 1.5 Document gaps: what domain needs are NOT covered by existing entities/services

## Phase 2: New Entity Definitions (XML Only)

- [ ] 2. Create Moqui component structure
  - [ ] 2.1 Create component directory: `backend/runtime/component/{{COMPONENT_NAME}}/`
  - [ ] 2.2 Create `entity/{{Domain}}Entities.xml` with new entity definitions
  - [ ] 2.3 Create `data/{{Domain}}SetupData.xml` with seed data (enum types, status types, status transitions)
  - [ ] 2.4 Register component in Moqui configuration (if needed)

- [ ] 3. Verify new entities work via generic API
  - [ ] 3.1 Restart backend and verify new entities are loaded by Entity Engine
  - [ ] 3.2 Test `GET /api/v1/entities/{{NewEntity}}` — list works
  - [ ] 3.3 Test `POST /api/v1/entities/{{NewEntity}}` — create works
  - [ ] 3.4 Test `GET /api/v1/entities/{{NewEntity}}/{id}` — get by ID works
  - [ ] 3.5 Test `PUT /api/v1/entities/{{NewEntity}}/{id}` — update works
  - [ ] 3.6 Test `DELETE /api/v1/entities/{{NewEntity}}/{id}` — delete works
  - [ ] 3.7 Test `GET /api/v1/entities/{{NewEntity}}/{id}/related/{relationship}` — related entities work
  - [ ] 3.8 Verify new entities appear in `kse scene discover -t entities`

## Phase 3: Domain Business Logic (Only If Needed)

- [ ] 4. Implement domain-specific services
  - [ ] 4.1 Create Java service class for {{BUSINESS_OPERATION_1}} (complex logic beyond CRUD)
  - [ ] 4.2 Create service XML definition in `service/{{Domain}}Services.xml`
  - [ ] 4.3 Test service invocation via `POST /api/v1/services/{{serviceName}}`
  - [ ] 4.4 Verify new services appear in `kse scene discover -t services`

- [ ] 5. Implement business rules
  - [ ] 5.1 Create EECA rules in `entity/{{Domain}}.eecas.xml` for automatic validations
  - [ ] 5.2 Implement status transition validation rules
  - [ ] 5.3 Implement cross-entity constraint rules
  - [ ] 5.4 Test business rules are enforced via API calls

## Phase 4: Domain Workflow Endpoints (Only If Needed)

- [ ]* 6. Create domain-specific controller endpoints (optional — only for complex orchestration)
  - [ ]* 6.1 Create {{Domain}}Controller with domain workflow endpoints
  - [ ]* 6.2 Register routes in Router
  - [ ]* 6.3 Test new endpoints

## Phase 5: Testing and Validation

- [ ] 7. Integration tests
  - [ ] 7.1 Test full CRUD lifecycle for each new entity via generic API
  - [ ] 7.2 Test reused Moqui entity operations with domain-specific filters
  - [ ] 7.3 Test service invocations for both reused and new services
  - [ ] 7.4 Test referential integrity between new entities and Moqui entities

- [ ] 8. Property-based tests
  - [ ] 8.1 Property: Status flow validity — all transitions follow defined rules
  - [ ] 8.2 Property: Generic API compatibility — new entities support all CRUD operations
  - [ ] 8.3 Property: Business rule consistency — rules hold across random valid inputs

- [ ] 9. Discovery verification
  - [ ] 9.1 Run `kse scene discover -t entities` and verify all new entities appear
  - [ ] 9.2 Run `kse scene discover -t services` and verify all new services appear

## Phase 6: Documentation and Seed Data

- [ ] 10. Documentation and data
  - [ ] 10.1 Create seed data for development/testing in `data/{{Domain}}DemoData.xml`
  - [ ] 10.2 Update API documentation with domain-specific usage examples
  - [ ] 10.3 Document entity-to-domain mapping table for future reference
