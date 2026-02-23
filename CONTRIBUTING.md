# Contributing to OpenPQL Examples

Thank you for your interest in contributing PQL examples!

## What We Accept

We welcome contributions of:
- **New regulation examples** (SOX, PCI-DSS, CCPA, etc.)
- **Improved documentation** (clearer explanations, better comments)
- **Bug fixes** (syntax errors, incorrect regulation citations)
- **Additional use cases** (industry-specific patterns)

## What We Don't Accept

- Compiler modifications (compiler is closed-source)
- Breaking changes to existing examples without discussion
- Examples without proper regulation citations

## How to Contribute

### 1. Fork & Clone

```bash
git clone https://github.com/openpql/openpql-examples.git
cd openpql-examples
```

### 2. Create Branch

```bash
git checkout -b add-sox-examples
```

### 3. Add Your Examples

Follow the structure:
```
examples/
  your_regulation/
    example_1.pql
    example_2.pql
    README.md
```

### 4. Example Template

```pql
# [Regulation Name] - [Article/Section]: [Title]
# Brief description of what this example demonstrates

FRAMEWORK Regulation_Name {
    version: "YYYY.MM.DD"
}

INTENT intent_name {
    triggers: ["event_trigger"],
    context: [data_sources],
    
    description: "Detailed explanation citing specific article/section"
    
    conditions: {
        WHEN condition THEN {
            field: "value",
            regulation_reference: "Article X",
            compliance_action: "action_name"
        }
    }
}
```

### 5. Add Documentation

Create `examples/your_regulation/README.md`:

```markdown
# [Regulation Name] Examples

## Overview
Brief explanation of the regulation

## Examples

1. **[example_1.pql](./example_1.pql)** - Description
2. **[example_2.pql](./example_2.pql)** - Description

## Regulation References

- [Official source](https://link-to-official-regulation)
```

### 6. Submit Pull Request

- Describe what your examples demonstrate
- Include regulation citations
- Explain any complex logic

## Code Quality Standards

### ✅ Good Example

```pql
# GDPR Article 17 - Right to Erasure
FRAMEWORK GDPR_Article_17 {
    version: "2018.05.25"
}

INTENT process_erasure_request {
    triggers: ["erasure_request_received"],
    context: [user_data, processing_records, legal_basis],
    
    description: "Article 17(1) - Process right to erasure requests when 
                  conditions are met"
    
    conditions: {
        # Personal data no longer necessary
        WHEN data_retention_period_expired == true AND
             no_legal_obligation_to_retain == true THEN {
            erasure_action: "delete_all_personal_data",
            article_reference: "17_1_a",
            completion_deadline_days: 30,
            user_confirmation_required: true
        }
    }
}
```

### ❌ Bad Example

```pql
# Generic data deletion
INTENT delete_stuff {
    triggers: ["delete"],
    
    conditions: {
        WHEN x == y THEN deny: "no" WITH {}
    }
}
```

**Problems:**
- No regulation citation
- Vague intent name
- No description
- Missing context
- Unclear conditions
- No compliance metadata

## Regulation Citation Guidelines

Always include:
1. **Specific article/section numbers**
2. **Official regulation name** (with year if applicable)
3. **Direct quotes** for key requirements (in description)
4. **Links to official sources** (in README)

Example:
```pql
description: "Article 6(1)(a) GDPR - Processing is lawful only if data subject 
              has given consent for one or more specific purposes"
```

## Testing Your Examples

Before submitting:
1. **Verify syntax** - Ensure PQL is valid
2. **Check citations** - Confirm regulation references are accurate
3. **Test readability** - Can a compliance officer understand it?
4. **Add comments** - Explain non-obvious logic

## Questions?

- 📧 Email: nishanth.voduru@openpql.com
- 💬 [GitHub Discussions](https://github.com/openpql/openpql-examples/discussions)
- 🌐 [OpenPQL Website](https://openpql.com)

---

**Thank you for helping build the policy-as-code community!**

*© 2025-2026 OpenPQL, Inc.*
