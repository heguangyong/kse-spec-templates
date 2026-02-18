# Template Usage Guide

This guide explains how to use scene-capability-engine-templates to quickly create well-structured feature specifications.

## Table of Contents

- [Getting Started](#getting-started)
- [Listing Templates](#listing-templates)
- [Searching Templates](#searching-templates)
- [Viewing Template Details](#viewing-template-details)
- [Creating Spec from Template](#creating-spec-from-template)
- [Customizing Templates](#customizing-templates)
- [Updating Templates](#updating-templates)
- [Best Practices](#best-practices)

## Getting Started

### Prerequisites

- scene-capability-engine (sce) installed: `npm install -g scene-capability-engine`
- Git installed on your system
- Internet connection (for first-time template download)

### First-Time Setup

Templates are automatically downloaded when you first use them. No manual setup required!

```bash
# List available templates (downloads on first use)
sce templates list

# Or create a Spec directly (downloads automatically)
sce spec create my-feature --template web-features/rest-api
```

## Listing Templates

View all available templates grouped by category:

```bash
sce templates list
```

**Output Example**:
```
📁 web-features
  ├─ rest-api (intermediate) - RESTful API endpoints with validation
  └─ graphql-api (intermediate) - GraphQL API with schema and resolvers

📁 backend-features
  └─ database-integration (intermediate) - Database with schema and migrations
```

### Filter by Category

```bash
sce templates list --category web-features
```

### Filter by Source

```bash
sce templates list --source official
```

## Searching Templates

Find templates by keyword:

```bash
# Search for API-related templates
sce templates search "api"

# Search for database templates
sce templates search "database"

# Search by tag
sce templates search "graphql"
```

The search looks through template names, descriptions, and tags.

## Viewing Template Details

Get detailed information about a specific template:

```bash
sce templates show web-features/rest-api
```

**Output includes**:
- Template name and description
- Difficulty level
- Tags
- Applicable scenarios
- Author and dates
- File list

## Creating Spec from Template

### Basic Usage

```bash
sce spec create my-feature --template web-features/rest-api
```

This creates a new Spec at `.kiro/specs/my-feature/` with:
- `requirements.md` - Feature requirements
- `design.md` - Technical design
- `tasks.md` - Implementation tasks

### What Happens

1. **Template Download**: If not cached, downloads template from repository
2. **Variable Substitution**: Replaces placeholders with actual values:
   - `{{SPEC_NAME}}` → `my-feature`
   - `{{SPEC_NAME_TITLE}}` → `My Feature`
   - `{{DATE}}` → Current date (2025-01-31)
   - `{{YEAR}}` → Current year (2025)
   - `{{AUTHOR}}` → Your Git username
   - `{{PROJECT_NAME}}` → Project name from package.json
3. **Frontmatter Removal**: Removes YAML frontmatter from template files
4. **File Creation**: Creates Spec files in `.kiro/specs/my-feature/`

### Force Overwrite

If Spec already exists, use `--force` to overwrite:

```bash
sce spec create my-feature --template web-features/rest-api --force
```

## Customizing Templates

After creating a Spec from a template, customize it for your needs:

### 1. Review Requirements

Open `requirements.md` and:
- Replace placeholder text with your specific requirements
- Add or remove requirements as needed
- Update acceptance criteria
- Define your glossary terms

### 2. Update Design

Open `design.md` and:
- Choose specific technologies (framework, database, etc.)
- Update architecture diagrams
- Define your data models
- Specify error handling approach

### 3. Adjust Tasks

Open `tasks.md` and:
- Add project-specific tasks
- Remove irrelevant tasks
- Adjust task order if needed
- Add dependencies between tasks

## Updating Templates

Keep your local template cache up to date:

```bash
# Update all template sources
sce templates update

# Update specific source
sce templates update --source official

# Update to specific version
sce templates update --version v1.2.0
```

**Change Detection**: The update command shows:
- ✅ New templates added
- 📝 Templates modified
- ❌ Templates removed

## Best Practices

### Choosing the Right Template

1. **Match Your Use Case**: Review "Applicable Scenarios" in template details
2. **Consider Difficulty**: Start with beginner templates if new to the domain
3. **Check Tags**: Use tags to find templates with specific technologies

### After Creating from Template

1. **Don't Skip Customization**: Templates are starting points, not final solutions
2. **Remove Guidance Comments**: Delete `<!-- -->` comments after filling sections
3. **Update Regularly**: Keep requirements and design in sync as you implement
4. **Follow the Workflow**: Requirements → Design → Tasks → Implementation

### Working with Templates

1. **Read the Whole Template**: Understand the structure before customizing
2. **Keep What's Useful**: Don't feel obligated to use every section
3. **Add Your Context**: Include project-specific details and constraints
4. **Maintain Traceability**: Keep requirement references in design and tasks

### Template Maintenance

1. **Update Regularly**: Run `sce templates update` weekly
2. **Clear Cache if Needed**: `sce templates cache --clear` to force re-download
3. **Check Cache Status**: `sce templates cache` to see what's cached

## Troubleshooting

### Template Not Found

```bash
# List all templates to verify the ID
sce templates list

# Update templates to get latest
sce templates update
```

### Download Fails

```bash
# Check internet connection
# Clear cache and retry
sce templates cache --clear
sce templates update
```

### Variables Not Replaced

Ensure you're using the correct placeholder format:
- ✅ `{{SPEC_NAME}}` (double curly braces)
- ❌ `{SPEC_NAME}` (single curly braces)

### Spec Already Exists

Use `--force` flag to overwrite:
```bash
sce spec create my-feature --template web-features/rest-api --force
```

## Advanced Usage

### Using Custom Template Sources

Add your own template repository:

```bash
sce templates add-source my-templates https://github.com/myorg/my-templates.git
```

### Offline Mode

Once templates are cached, you can work offline:

```bash
# Templates are cached at ~/.kse/templates/
# All operations work without internet after initial download
sce templates list
sce spec create my-feature --template web-features/rest-api
```

### Multiple Sources

When templates from different sources have the same name:

```bash
# Use source prefix
sce spec create my-feature --template official:web-features/rest-api
sce spec create my-feature --template my-templates:web-features/rest-api
```

## Getting Help

- **Command Help**: `sce templates --help`
- **Template Guide**: `sce templates guide`
- **Report Issues**: https://github.com/heguangyong/scene-capability-engine-templates/issues
- **Contribute**: See [CONTRIBUTING.md](../CONTRIBUTING.md)

---

**Last Updated**: 2025-01-31  
**Version**: 1.0.0
