# CLAUDE.md - AI Assistant Guide for mental_models Repository

## Repository Overview

This repository contains a comprehensive, structured collection of **mental models** — frameworks, heuristics, and thinking patterns from diverse domains including philosophy, psychology, economics, systems theory, decision science, negotiation, learning theory, and more.

### Purpose

The mental models in this repository are designed to:
- Provide reusable reasoning frameworks for complex decision-making
- Support AI-assisted analysis and problem-solving
- Enable contextual application across domains (with special emphasis on CRNA/clinical systems)
- Serve as a knowledge base for reasoning engines and decision support systems

### Key Characteristics

- **Domain-agnostic foundation**: Models span philosophy, psychology, economics, operations, human factors, etc.
- **Clinical overlay**: Many models include CRNA (Certified Registered Nurse Anesthetist) clinical applications
- **Structured format**: All entries follow a strict JSON schema for consistency
- **Cross-referencing**: Models link to related/counterbalance models for deeper analysis

---

## Repository Structure

```
mental_models/
├── README.md                      # Minimal project title
├── mental_models.json             # Main collection (186 models)
├── models/
│   └── mental_models.json         # Duplicate of main collection
└── schemas/
    └── mental_models.schema       # JSON Schema definition
```

### File Descriptions

| File | Purpose | Lines | Notes |
|------|---------|-------|-------|
| `mental_models.json` | Primary data source | 186 | One mental model per line (JSONL format) |
| `models/mental_models.json` | Duplicate collection | 186 | Mirror of root file |
| `schemas/mental_models.schema` | JSON Schema | 92 | Defines structure & validation rules |
| `README.md` | Project title | 1 | Minimal documentation |

---

## Data Model & Schema

### MentalModelEntry Structure

Each mental model follows this schema (defined in `schemas/mental_models.schema`):

#### Required Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `model_id` | string | Unique identifier (uppercase, underscores) | `"MM_OCCAM_S_RAZOR"` |
| `name` | string | Human-readable name | `"Occam's Razor"` |
| `category` | string | Primary classification | `"philosophy"` |
| `definition` | string | Core principle/concept | `"Prefer the simplest explanation..."` |
| `domains` | array[string] | Applicable fields | `["philosophy", "science", "medicine"]` |
| `tags` | array[string] | Searchable keywords | `["simplicity", "inference"]` |
| `use_cases` | array[string] | Practical applications | `["diagnosis", "debugging"]` |
| `version` | string | Semantic version | `"1.0.0"` |

#### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `positive_example` | string | When/how the model works well |
| `negative_example` | string | Limitations or failure modes |
| `triggers` | array[string] | When to activate this model |
| `disqualifiers` | array[string] | When NOT to use this model |
| `application_steps` | array[string] | How to apply the model |
| `counterbalance_models` | array[string] | Models that offset this one's biases |
| `related_models` | array[string] | Complementary or similar models |
| `crna_clinical_overlay` | string | Clinical application notes (CRNA-specific) |

### model_id Convention

- Format: `MM_<NAME_IN_CAPS>`
- Pattern: `^[A-Z0-9_]+$`
- Examples:
  - `MM_OCCAM_S_RAZOR`
  - `MM_PARETO_PRINCIPLE`
  - `MM_SWISS_CHEESE_MODEL`
  - `MM_BATNA`

### Category Taxonomy

The repository uses these primary categories:

- `philosophy` - Fundamental reasoning principles
- `psychology` - Cognitive patterns and biases
- `economics` - Resource allocation, trade-offs
- `systems_theory` - Complex systems and feedback
- `decision_science_&_statistics` - Probabilistic reasoning
- `operations_&_flow` - Process optimization
- `human_factors_&_safety` - Error prevention, reliability
- `behavioral_decision-making` - Heuristics and biases
- `epistemology_&_scientific_thinking` - Knowledge and truth
- `negotiation_&_communication` - Influence and conflict
- `learning_models` - Skill acquisition and retention
- `incentives_&_game_theory` - Strategic interaction
- `strategic_thinking` - Planning and analysis

---

## Development Workflows

### Adding a New Mental Model

1. **Define the model** following the schema structure
2. **Assign a unique `model_id`** using the `MM_` prefix convention
3. **Validate** against `schemas/mental_models.schema`
4. **Add to `mental_models.json`** (append as new line in JSONL format)
5. **Sync to `models/mental_models.json`** (keep duplicate in sync)
6. **Commit** with descriptive message

Example commit message:
```
Add MM_SECOND_ORDER_THINKING mental model

- Category: strategic_thinking
- Domains: strategy, operations
- Includes clinical overlay for workflow evaluation
```

### Modifying an Existing Model

1. **Locate the model** by `model_id` in `mental_models.json`
2. **Update fields** as needed
3. **Increment `version`** if substantive change (follow semver)
4. **Sync changes** to `models/mental_models.json`
5. **Commit** with clear description of changes

Example commit message:
```
Update MM_OCCAM_S_RAZOR: Add application_steps

- Added structured application steps
- Enhanced clinical overlay with specific examples
- Bumped version to 1.1.0
```

### Validating Schema Compliance

When working with mental models, ensure:

- All **required fields** are present
- `model_id` matches pattern `^[A-Z0-9_]+$`
- Arrays (domains, tags, use_cases) are non-empty for required fields
- `version` follows semantic versioning (e.g., `"1.0.0"`)
- No extra fields beyond schema definition (`additionalProperties: false`)

---

## Key Conventions & Patterns

### 1. File Format

**JSONL (JSON Lines)**: Each mental model is a complete JSON object on a single line. This format:
- Enables line-based processing
- Simplifies version control diffs
- Allows streaming/partial reads

### 2. Versioning

- Use **semantic versioning**: `MAJOR.MINOR.PATCH`
- Increment `MAJOR` for breaking changes to model definition
- Increment `MINOR` for additions (new fields, enhanced examples)
- Increment `PATCH` for corrections (typos, clarifications)

### 3. Cross-References

When models reference each other:
- Use `related_models` for complementary frameworks
- Use `counterbalance_models` for offsetting biases
- Reference by `model_id` (e.g., `"MM_CONFIRMATION_BIAS"`)

### 4. Clinical Overlays

The `crna_clinical_overlay` field provides domain-specific applications:
- Keep focused on practical, actionable insights
- Use concrete scenarios when possible
- Balance specificity with general applicability

### 5. Examples

- `positive_example`: Focus on **when and why** the model succeeds
- `negative_example`: Highlight **failure modes and limitations**
- Use clear, concise language
- Provide context for application

---

## Working with Mental Models

### Searching for Models

**By domain:**
```bash
grep -i '"domains":.*"medicine"' mental_models.json
```

**By category:**
```bash
grep '"category": "psychology"' mental_models.json
```

**By tag:**
```bash
grep '"tags":.*"bias"' mental_models.json
```

**By model_id:**
```bash
grep '"model_id": "MM_OCCAM_S_RAZOR"' mental_models.json
```

### Extracting Specific Fields

Using `jq` (if available):
```bash
# List all model names
cat mental_models.json | jq -r '.name'

# Get all models in a category
cat mental_models.json | jq 'select(.category == "philosophy")'

# Extract clinical overlays
cat mental_models.json | jq -r 'select(.crna_clinical_overlay != null) | "\(.name): \(.crna_clinical_overlay)"'
```

### Validation

If you have a JSON schema validator:
```bash
# Example using ajv-cli
ajv validate -s schemas/mental_models.schema -d mental_models.json
```

---

## Git Conventions

### Branch Naming

This repository follows a `claude/` prefix convention for AI-generated branches:
- Format: `claude/<description>-<session-id>`
- Example: `claude/add-claude-documentation-WUig8`

### Commit Message Guidelines

Use clear, descriptive commit messages:

**Format:**
```
<action> <what>

- Detail 1
- Detail 2
- Detail 3
```

**Examples:**
```
Add mental model for Second-Order Thinking

- Category: strategic_thinking
- Includes application steps and clinical overlay
- References related models for systems thinking

Update MM_BAYESIAN_UPDATING definition

- Clarified mathematical notation
- Added practical clinical example
- Bumped version to 1.1.0

Delete mental_model.schema.json

- Consolidating schema files
- Retained schemas/mental_models.schema as canonical
```

### Push Protocol

- **Always** use: `git push -u origin <branch-name>`
- Branch names **must** start with `claude/` and end with session ID
- Retry network failures up to 4 times with exponential backoff (2s, 4s, 8s, 16s)

---

## Quality Standards

### Completeness

- All **required fields** must be populated
- Avoid empty strings or placeholder values
- Provide meaningful content for optional fields when relevant

### Clarity

- Definitions should be **concise** (1-2 sentences)
- Examples should be **concrete** and **actionable**
- Avoid jargon without explanation

### Consistency

- Maintain consistent terminology across related models
- Use standard domain language (e.g., "diagnosis" not "figuring out what's wrong")
- Follow existing patterns for formatting and structure

### Accuracy

- Verify definitions against authoritative sources
- Test examples for practical validity
- Cross-check related/counterbalance model references

---

## Common Tasks for AI Assistants

### Task: Add a New Mental Model

1. Read `schemas/mental_models.schema` to understand required structure
2. Create new model object with all required fields
3. Generate unique `model_id` following `MM_` convention
4. Add as new line to `mental_models.json`
5. Duplicate to `models/mental_models.json`
6. Commit changes with descriptive message

### Task: Find Models by Domain

1. Use `Grep` tool with pattern: `"domains":.*"<domain>"`
2. Parse results to extract relevant models
3. Present findings with model names and brief descriptions

### Task: Update Model Definition

1. Locate model by `model_id` in `mental_models.json`
2. Use `Read` tool to view current content
3. Use `Edit` tool to update specific fields
4. Increment `version` if substantive change
5. Sync changes to `models/mental_models.json`
6. Commit with clear change description

### Task: Validate Schema Compliance

1. Read the schema from `schemas/mental_models.schema`
2. Read sample entries from `mental_models.json`
3. Check for required fields, correct types, and pattern compliance
4. Report any validation errors with specific line/field references

### Task: Generate Model Summary

1. Read models from `mental_models.json` (use offset/limit for large files)
2. Extract key fields: name, category, definition
3. Group by category or domain as requested
4. Format as readable markdown table or list

---

## Integration Points

### For Reasoning Engines

Mental models in this repository can be:
- **Indexed** by domain, category, tags for contextual retrieval
- **Chained** using related_models for multi-model analysis
- **Balanced** using counterbalance_models to reduce bias
- **Applied** following application_steps for structured reasoning

### For Decision Support Systems

Models provide:
- **Triggers** for when to activate specific frameworks
- **Disqualifiers** to prevent misapplication
- **Use cases** for matching to problem types
- **Examples** (positive/negative) for training and validation

### For Clinical Applications

The CRNA clinical overlays enable:
- Domain-specific application in anesthesia/perioperative settings
- Integration with clinical decision support
- Training and education for medical professionals
- Safety analysis and risk management

---

## Maintenance Notes

### File Synchronization

The repository maintains duplicate files (`mental_models.json` and `models/mental_models.json`). When making changes:

1. **Primary edits** should go to `mental_models.json` (root)
2. **Sync to** `models/mental_models.json` immediately
3. **Verify** both files remain identical

Consider setting up a pre-commit hook or CI check to validate synchronization.

### Schema Evolution

If the schema needs to change:

1. Update `schemas/mental_models.schema`
2. Migrate **all** existing entries in `mental_models.json`
3. Update this documentation to reflect changes
4. Increment schema version or add migration notes
5. Test validation against all entries

### Categories and Tags

As the collection grows, consider:
- Standardizing tag vocabulary
- Creating a category hierarchy
- Building an index or lookup table
- Documenting category definitions

---

## Examples

### Complete Mental Model Entry

```json
{
  "model_id": "MM_OCCAM_S_RAZOR",
  "name": "Occam's Razor",
  "category": "philosophy",
  "definition": "Prefer the simplest explanation that adequately fits the data.",
  "domains": ["philosophy", "science", "medicine"],
  "tags": ["simplicity", "inference", "diagnostics"],
  "use_cases": ["diagnosis", "root_cause_analysis", "debugging"],
  "positive_example": "Simplifying a differential diagnosis to the fewest likely causes improves speed and accuracy.",
  "negative_example": "Oversimplifying can miss rare but critical conditions.",
  "triggers": [],
  "disqualifiers": [],
  "application_steps": [],
  "counterbalance_models": [],
  "related_models": [],
  "crna_clinical_overlay": "Favor the simplest explanation for hypotension (e.g., depth of anesthesia) before chasing rare causes, while staying vigilant for red flags.",
  "version": "1.0.0"
}
```

### Minimal Valid Entry

```json
{
  "model_id": "MM_EXAMPLE_MODEL",
  "name": "Example Model",
  "category": "philosophy",
  "definition": "A clear, concise definition of the mental model.",
  "domains": ["philosophy"],
  "tags": ["example"],
  "use_cases": ["demonstration"],
  "version": "1.0.0"
}
```

---

## Troubleshooting

### Issue: Schema Validation Fails

**Solution:**
1. Check that all required fields are present
2. Verify `model_id` matches pattern `^[A-Z0-9_]+$`
3. Ensure arrays are not empty for required array fields
4. Check for typos in field names
5. Validate JSON syntax (proper quotes, commas, brackets)

### Issue: Files Out of Sync

**Solution:**
1. Determine which file has the correct content
2. Copy correct file to the other location:
   ```bash
   cp mental_models.json models/mental_models.json
   # or
   cp models/mental_models.json mental_models.json
   ```
3. Verify with `diff`:
   ```bash
   diff mental_models.json models/mental_models.json
   ```

### Issue: Cannot Find a Model

**Solution:**
1. Search by multiple criteria (name, id, tags, domain)
2. Check for typos in `model_id` (case-sensitive, underscore placement)
3. Verify the model exists in the current branch
4. Use `grep -i` for case-insensitive search

---

## Future Enhancements

Potential improvements to consider:

1. **Automated validation** - CI pipeline to check schema compliance
2. **Index generation** - Create searchable index by category/domain/tag
3. **Relationship visualization** - Graph of model connections
4. **Version history** - Track model evolution over time
5. **Examples library** - Expand positive/negative examples
6. **Translation layer** - Multi-language support
7. **API wrapper** - Programmatic access to mental models
8. **Documentation site** - Web interface for browsing models

---

## Quick Reference

### Essential Commands

```bash
# Count total models
wc -l mental_models.json

# List all categories
grep -o '"category": "[^"]*"' mental_models.json | sort -u

# Find models by domain
grep '"domains":.*"medicine"' mental_models.json

# Validate files are in sync
diff mental_models.json models/mental_models.json

# Search for specific model
grep '"model_id": "MM_OCCAM_S_RAZOR"' mental_models.json
```

### File Paths

- Main collection: `/home/user/mental_models/mental_models.json`
- Duplicate: `/home/user/mental_models/models/mental_models.json`
- Schema: `/home/user/mental_models/schemas/mental_models.schema`

### Key Patterns

- Model ID: `MM_<NAME_IN_CAPS>`
- Version: Semantic versioning (e.g., `1.0.0`)
- Format: JSONL (one model per line)
- Encoding: UTF-8

---

## Resources

- **JSON Schema Spec**: https://json-schema.org/draft-07/schema
- **Semantic Versioning**: https://semver.org/
- **JSONL Format**: https://jsonlines.org/

---

*Last Updated: 2026-01-01*
*Repository: jurgey/mental_models*
*Branch: claude/add-claude-documentation-WUig8*
