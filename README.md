# kse-spec-templates

Official template library for [kiro-spec-engine (kse)](https://github.com/heguangyong/kiro-spec-engine).

This repository contains high-quality, community-contributed Spec templates to help you quickly create well-structured feature specifications.

## 🚀 Quick Start

```bash
# Update your local template cache
kse templates update

# List all templates (grouped by category)
kse templates list

# Filter by category
kse templates list --category backend-features

# Search by keyword (matches name, description, tags)
kse templates search "rest"
kse templates search "quality"

# View template details and applicable scenarios
kse templates show backend-features/pure-restful-backend

# Create a new Spec from a template
kse spec create my-feature --template backend-features/pure-restful-backend
```

## 📁 Template Categories

| Category | Description | Templates |
|----------|-------------|-----------|
| **web-features/** | Frontend and web application features | 2 |
| **backend-features/** | Backend services and APIs | 2 |
| **architecture/** | System architecture and design patterns | 1 |
| **quality/** | Quality assurance and technical debt | 1 |
| **domain-modeling/** | Business domain analysis and data modeling | 2 |

## 🎯 Available Templates

| Template ID | Name | Difficulty | Tags | Use When... |
|-------------|------|------------|------|-------------|
| `web-features/rest-api` | REST API Feature | intermediate | api, rest, http, validation | Creating RESTful API endpoints, CRUD operations, microservices |
| `web-features/graphql-api` | GraphQL API Feature | intermediate | api, graphql, schema, resolvers | Building GraphQL APIs, flexible data queries, real-time apps |
| `backend-features/database-integration` | Database Integration | intermediate | database, schema, migrations, orm | Setting up database, data persistence layer, migrations |
| `backend-features/pure-restful-backend` | Pure RESTful Backend | advanced | rest, jetty, java, modular-architecture | Building REST backend from scratch, modernizing legacy backend, embedded Jetty microservices |
| `architecture/architecture-design` | Architecture Design | advanced | architecture, system-design, components, data-flow | Designing new system architecture, restructuring apps, microservices decomposition |
| `quality/phase2-quality-debt-closure` | Quality Debt Closure | intermediate | quality, testing, coverage, technical-debt | Improving test coverage, closing technical debt, quality improvement sprints |
| `domain-modeling/domain-analysis` |
| `domain-modeling/moqui-domain-extension` | Moqui Domain Extension | intermediate | moqui, entity-engine, rest-api, domain-extension | Extending Moqui ERP for industry-specific needs, reusing existing entities and REST APIs | Domain Analysis | intermediate | domain-modeling, data-model, entity-relationship, state-machine | Analyzing business domains, building data models, designing entity relationships and lifecycles |

### How to Choose

- **Starting a new business domain?** → `domain-modeling/domain-analysis` (start here — define entities, relationships, rules first)
- **Extending Moqui for your industry?**  `domain-modeling/moqui-domain-extension` (reuse Moqui entities + REST APIs)
- **Extending Moqui for your industry?**  `domain-modeling/moqui-domain-extension` (reuse Moqui entities + REST APIs, add only what's missing)
- **Building a new API?** → `web-features/rest-api` (simple) or `backend-features/pure-restful-backend` (full stack)
- **Need GraphQL?** → `web-features/graphql-api`
- **Adding a database?** → `backend-features/database-integration`
- **Designing system architecture?** → `architecture/architecture-design`
- **Improving code quality?** → `quality/phase2-quality-debt-closure`

### Recommended Template Chain (Full Project)

For a complete business application, use templates in this order:

```
1. domain-modeling/domain-analysis        → Define what to build (entities, rules, processes)
2. architecture/architecture-design       → Define how to build it (architecture, tech stack)
3. backend-features/pure-restful-backend  → Build the backend (REST API, services, data layer)
4. quality/phase2-quality-debt-closure    → Ensure quality (test coverage, debt closure)
```

## 📝 Template Format

Each template consists of three files with YAML frontmatter:

```
template-name/
├── requirements.md    # Feature requirements and acceptance criteria
├── design.md          # Technical design and architecture
└── tasks.md           # Implementation tasks breakdown
```

### Example Frontmatter

```yaml
---
name: REST API Feature
category: web-features
description: Template for creating RESTful API endpoints
difficulty: intermediate
tags:
  - api
  - rest
  - backend
applicable_scenarios:
  - Creating new API endpoints
  - Implementing CRUD operations
  - Building microservices
author: kse-team
created_at: 2025-01-30
updated_at: 2025-01-30
version: 1.0.0
---
```

## 🤝 Contributing

We welcome high-quality template contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Quick Contribution Steps

1. Fork this repository
2. Create a new template in the appropriate category
3. Follow the [template structure guidelines](CONTRIBUTING.md#template-structure)
4. Submit a pull request with the validation checklist

## 📊 Template Quality Standards

All templates must:
- ✅ Include complete frameworks for requirements, design, and tasks
- ✅ Contain clear comments and filling instructions
- ✅ Include example content demonstrating best practices
- ✅ Be validated against real projects
- ✅ Pass all validation checks

## 📖 Documentation

- [Template Usage Guide](docs/template-usage-guide.md)
- [Template Creation Guide](docs/template-creation-guide.md)
- [Contributing Guidelines](CONTRIBUTING.md)

## 📜 License

MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

Thanks to all contributors who have shared their templates with the community!

---

**Version**: 1.3.0  
**Last Updated**: 2026-02-11  
**Templates**: 8  
**Maintained by**: [kse-team](https://github.com/heguangyong/kiro-spec-engine)



