# PQL Syntax Guide

**Policy Query Language (PQL) v1.4 - Complete Reference**

---

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Structure](#basic-structure)
3. [FRAMEWORK Declaration](#framework-declaration)
4. [INTENT Blocks](#intent-blocks)
5. [Conditions & Rules](#conditions--rules)
6. [Actions](#actions)
7. [Data Types](#data-types)
8. [Operators](#operators)
9. [v1.4 Features](#v14-features)
10. [Best Practices](#best-practices)

---

## Introduction

PQL is a declarative language for expressing compliance policies as compilable code. It bridges the gap between legal requirements and executable governance logic.

**Design Principles:**
- **Readable by compliance officers** (not just engineers)
- **Unambiguous** (one interpretation only)
- **Compilable** (produces production artifacts)
- **Auditable** (every decision is traceable)

---

## Basic Structure

Every PQL file contains:

```pql
# 1. FRAMEWORK declaration (metadata)
FRAMEWORK Framework_Name {
    version: "YYYY.MM.DD"
}

# 2. One or more INTENT blocks (business logic)
INTENT intent_name {
    triggers: ["event1", "event2"],
    context: [data_source1, data_source2],
    
    conditions: {
        WHEN condition THEN action
    }
}
```

---

## FRAMEWORK Declaration

Identifies the regulatory framework or policy domain.

**Syntax:**
```pql
FRAMEWORK Framework_Name {
    version: "YYYY.MM.DD"
}
```

**Examples:**
```pql
FRAMEWORK GDPR_Article_6 {
    version: "2018.05.25"
}

FRAMEWORK HIPAA_Privacy {
    version: "2013.01.25"
}

FRAMEWORK EU_AI_Act_Article_6 {
    version: "2024.06.01"
}
```

---

## INTENT Blocks

An INTENT represents a discrete governance decision or policy enforcement.

**Syntax:**
```pql
INTENT intent_name {
    triggers: ["trigger1", "trigger2"],
    context: [data1, data2],
    description: "Human-readable explanation"
    
    conditions: {
        WHEN condition THEN action
    }
}
```

**Components:**

### `triggers` (required)
Events that activate this INTENT.

```pql
triggers: ["new_customer_onboarding"]
triggers: ["data_processing_request", "consent_check"]
triggers: ["ai_system_execution"]
```

### `context` (required)
Data sources needed for decision-making.

```pql
context: [customer_data]
context: [user_profile, consent_record, processing_purpose]
context: [ai_output, user_interaction_patterns, psychological_indicators]
```

### `description` (optional)
Human-readable explanation for auditors.

```pql
description: "Article 6(1)(a) - Detect AI systems using subliminal techniques"
```

### `conditions` (required)
The actual governance logic (see next section).

---

## Conditions & Rules

The heart of PQL - expressing "if this, then that" logic.

### Basic WHEN-THEN

```pql
conditions: {
    WHEN user.age < 18 THEN
        deny: "Must be 18 or older" WITH {
            regulation: "COPPA",
            severity: "blocking"
        }
}
```

### Multiple Conditions

```pql
conditions: {
    WHEN consent_timestamp == null THEN
        deny: "Missing consent" WITH {
            regulation: "GDPR Article 6"
        }
    
    WHEN consent_expired == true THEN
        deny: "Consent expired" WITH {
            regulation: "GDPR Article 6"
        }
}
```

### Complex Boolean Logic

```pql
WHEN customer.country IN sanctions_list AND
     enhanced_due_diligence_completed == false THEN {
    risk_level: "critical",
    compliance_action: "block_immediately"
}

WHEN user.age < 16 OR
     user.disability_status != null THEN {
    protection_level: "enhanced"
}
```

---

## Actions

What happens when a condition matches.

### v1.3 Actions (WITH syntax)

**deny:**
```pql
WHEN invalid_request THEN
    deny: "Reason for denial" WITH {
        regulation: "Regulation reference",
        severity: "blocking"
    }
```

**authorize:**
```pql
WHEN valid_request THEN
    authorize: "Allow with conditions" WITH {
        audit_level: "detailed"
    }
```

**route_to:**
```pql
WHEN complex_validation_needed THEN
    route_to: "validation_engine" WITH {
        check_type: "enhanced_screening"
    }
```

### v1.4 Actions (Object Return)

Return structured data directly:

```pql
WHEN manipulation_detected THEN {
    prohibited_practice_type: "subliminal_manipulation",
    article_reference: "6_1_a",
    risk_level: "critical",
    compliance_action: "block_immediately"
}
```

---

## Data Types

### Primitives

```pql
"string"
123          # integer
45.67        # float
true         # boolean
null         # null
```

### Lists

```pql
["item1", "item2", "item3"]
[1, 2, 3, 4, 5]
```

### Objects (v1.4)

```pql
{
    field1: "value1",
    field2: 123,
    field3: true
}
```

---

## Operators

### Comparison

```pql
==    # equals
!=    # not equals
>     # greater than
<     # less than
>=    # greater than or equal
<=    # less than or equal
```

### Membership

```pql
IN        # value in list
NOT IN    # value not in list

WHEN customer.country IN ["US", "CA", "GB"]
WHEN status NOT IN ["active", "pending"]
```

### Boolean

```pql
AND
OR
NOT

WHEN age > 18 AND consent_given == true
WHEN country == "US" OR country == "CA"
WHEN NOT (status == "blocked")
```

---

## v1.4 Features

### Object Return Syntax

Instead of:
```pql
WHEN condition THEN
    route_to: "handler" WITH {
        param1: "value1"
    }
```

Use:
```pql
WHEN condition THEN {
    param1: "value1",
    param2: "value2",
    action_type: "handler"
}
```

**Benefits:**
- More declarative (describe what, not how)
- Cleaner for data-heavy responses
- Easier AI generation

### Hybrid Syntax (Coming Soon)

Mix actions and data:
```pql
WHEN high_risk THEN {
    risk_score: 0.85,
    risk_factors: ["sanctioned_country", "pep_status"],
    route_to: "enhanced_screening" WITH {
        priority: "urgent"
    }
}
```

---

## Best Practices

### 1. Use Descriptive Names

❌ Bad:
```pql
INTENT check1 {
    triggers: ["evt"],
    ...
}
```

✅ Good:
```pql
INTENT validate_gdpr_consent {
    triggers: ["data_processing_request"],
    ...
}
```

### 2. Include Regulation References

Always cite the specific article/section:

```pql
THEN {
    violation_type: "missing_consent",
    article_reference: "GDPR Article 6(1)",
    regulation: "EU Regulation 2016/679"
}
```

### 3. Separate Concerns

One INTENT = one decision domain.

❌ Bad:
```pql
INTENT validate_everything {
    # Mixing consent, age, and payment validation
}
```

✅ Good:
```pql
INTENT validate_consent { ... }
INTENT validate_age_restriction { ... }
INTENT validate_payment_authorization { ... }
```

### 4. Use Context Wisely

Only include data sources you actually use:

```pql
INTENT validate_consent {
    context: [consent_record, user_profile],  # Both used in conditions
    ...
}
```

### 5. Provide Actionable Denials

❌ Bad:
```pql
deny: "Error" WITH { ... }
```

✅ Good:
```pql
deny: "Consent expired on 2026-01-15. Please renew to continue." WITH {
    regulation: "GDPR Article 6",
    user_action_required: "renew_consent",
    help_url: "https://example.com/renew-consent"
}
```

### 6. Audit Everything

```pql
WHEN sensitive_action THEN {
    action_taken: "sensitive_data_access",
    audit_level: "critical",
    notification_required: true,
    retention_years: 7
}
```

---

## Complete Example

```pql
# GDPR Article 6 - Lawful Basis for Processing
FRAMEWORK GDPR_Article_6 {
    version: "2018.05.25"
}

INTENT validate_lawful_basis {
    triggers: ["data_processing_request"],
    context: [consent_record, user_profile, processing_purpose],
    
    description: "Ensure lawful basis exists before processing personal data"
    
    conditions: {
        # Missing consent entirely
        WHEN consent_timestamp == null AND 
             lawful_basis_type == null THEN
            deny: "No lawful basis for processing" WITH {
                regulation: "GDPR Article 6(1)",
                severity: "blocking",
                user_action_required: "obtain_consent"
            }
        
        # Consent expired
        WHEN consent_timestamp != null AND
             consent_expired == true THEN
            deny: "Consent expired. Please renew to continue." WITH {
                regulation: "GDPR Article 6(1)(a)",
                severity: "blocking",
                user_action_required: "renew_consent",
                expiration_date: consent_expiration_date
            }
        
        # Valid consent exists
        WHEN consent_timestamp != null AND
             consent_expired == false THEN
            authorize: "Processing authorized based on consent" WITH {
                regulation: "GDPR Article 6(1)(a)",
                lawful_basis: "consent",
                audit_level: "standard",
                consent_id: consent_record.id
            }
    }
}
```

---

## Next Steps

- Read [PQL Best Practices](./best-practices.md)
- Explore [Regulation Mapping](./regulation-mapping.md)
- See [Examples](../examples/) for real-world usage

---

*PQL Syntax is an open specification. The OpenPQL compiler is proprietary technology.*

*© 2025-2026 OpenPQL, Inc.*
