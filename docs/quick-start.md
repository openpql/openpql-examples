# PQL Quick Start Guide

**Get started with Policy Query Language in 5 minutes**

---

## What is PQL?

Policy Query Language (PQL) is a declarative language for expressing compliance policies as compilable code. Instead of writing procedural logic, you declare **what you want** and let the OpenPQL compiler handle **how to execute it**.

**Think of it as:** SQL for governance, but for AI-powered systems.

---

## Your First PQL Program

Let's build a simple GDPR consent checker:

```pql
# Define your data
DATASET consent_records {
    source: "consent_database",
    schema: {
        user_id: "integer",
        consent_given: "boolean",
        consent_timestamp: "timestamp",
        consent_purpose: "string"
    }
}

# Define your governance logic
INTENT validate_consent {
    triggers: ["data_processing_request"],
    context: [consent_records],
    
    conditions: {
        # No consent recorded
        WHEN consent_given == false THEN
            deny: "Consent not provided" WITH {
                regulation: "GDPR Article 6(1)(a)",
                action_required: "obtain_consent"
            }
        
        # Consent expired (older than 2 years)
        WHEN consent_timestamp < current_date - 730_days THEN
            deny: "Consent expired" WITH {
                regulation: "GDPR Article 7(3)",
                action_required: "renew_consent"
            }
        
        # Valid consent
        DEFAULT
            authorize: "Processing allowed" WITH {
                audit_level: "standard"
            }
    }
}
```

**That's it!** This PQL compiles to:
- FastAPI microservice
- PostgreSQL audit tables
- Cryptographic evidence chains
- Real-time compliance dashboards

---

## The Three Core Constructs

### **1. DATASET** - Your Data Foundation

Declare what data your governance logic needs:

```pql
DATASET customer_profiles {
    source: "customer_db",
    schema: {
        id: "integer",
        name: "string",
        email: "string",
        age: "integer",
        country: "string"
    }
}
```

### **2. INTENT** - Your Governance Logic

Express compliance rules as conditions:

```pql
INTENT age_verification {
    triggers: ["user_signup"],
    context: [customer_profiles],
    
    conditions: {
        WHEN age < 18 THEN
            deny: "Must be 18 or older" WITH {
                regulation: "COPPA",
                severity: "blocking"
            }
        
        DEFAULT
            authorize: "Age verified" WITH {
                audit_level: "standard"
            }
    }
}
```

### **3. FRAMEWORK** - Your Regulatory Context

Identify which regulation you're implementing:

```pql
FRAMEWORK GDPR_Article_6 {
    version: "2018.05.25"
}
```

---

## Common Patterns

### **Pattern 1: Simple Allow/Deny**

```pql
WHEN user.verified == false THEN
    deny: "Email verification required" WITH {
        severity: "blocking"
    }
```

### **Pattern 2: Multi-Condition Logic**

```pql
WHEN amount > 10000 AND location != customer.home_country THEN {
    risk_level: "high",
    compliance_action: "enhanced_due_diligence",
    manual_review_required: true
}
```

### **Pattern 3: Set Membership**

```pql
WHEN country IN ["US", "CA", "UK"] THEN
    authorize: "Approved jurisdiction" WITH {
        compliance_framework: "GDPR"
    }
```

### **Pattern 4: Range Checks**

```pql
WHEN age BETWEEN 13 AND 17 THEN {
    protection_level: "parental_consent_required",
    regulation: "COPPA Article 8"
}
```

---

## Next Steps

### **Explore Examples**

Browse real-world examples in the [`/examples`](../examples/) directory:
- **[EU AI Act](../examples/eu_ai_act/)** - Prohibited practices detection
- **[GDPR](../examples/gdpr/)** - Consent management
- **[HIPAA](../examples/hipaa/)** - PHI access controls
- **[AML](../examples/aml/)** - Customer risk assessment

### **Read the Language Reference**

Deep dive into PQL with the [Complete Language Reference](./pql-language-reference.md) - a comprehensive 50+ page enterprise guide covering:
- All six core constructs (DATASET, INTENT, WORKFLOW, MONITOR, COMPLIANCE, PROVIDERS)
- Advanced patterns (templates, error handling, optimization)
- Real-world use cases (financial services, healthcare, analytics)

### **Study the Syntax Guide**

Master essential patterns with the [PQL Syntax Guide](./pql-syntax.md):
- Data types and operators
- Conditional routing
- v1.4 features (object return syntax)
- Best practices

---

## Try OpenPQL

**The PQL examples are open.** The OpenPQL compiler is in private beta.

### **Option 1: NISHKA AI Beta**

Generate PQL automatically from plain English descriptions:
- 🤖 [NISHKA AI Beta](https://nishka.ai)
- Current accuracy: 60% GDPR, 60% HIPAA, 20% SOX (improving weekly)
- Target: 90%+ by Q1 2026

### **Option 2: Request Enterprise Beta Access**

For regulated enterprises (FinTech, HealthTech, AI platforms):
- 📧 Email: nishanth.voduru@openpql.com
- 🌐 Website: https://openpql.com

---

## Philosophy: AI-First Development

PQL embodies seven principles for building AI-powered governance systems:

1. **AI Intent Over Implementation** - Declare what, not how
2. **Declarative AI Orchestration** - Compose AI providers through declarations
3. **Adaptive State Synchronization** - Systems adapt without code changes
4. **Prompt Inheritance** - Reuse governance patterns
5. **Context-Aware Routing** - Route based on context, not logic
6. **Observable Operations** - Every decision is traceable
7. **Progressive Enhancement** - Start simple, add sophistication

Read more: [Seven Principles of AI-First Development](../README.md#-the-seven-principles-of-ai-first-development)

---

## Get Help

- 💬 [GitHub Discussions](https://github.com/openpql/openpql-examples/discussions)
- 📧 [Email](mailto:nishanth.voduru@openpql.com)
- 🐦 [Twitter](https://twitter.com/openpql)
- 💼 [LinkedIn](https://linkedin.com/company/openpql)

---

**Ready to compile governance?** Start with the [examples](../examples/) and work your way up! 🚀

*© 2025-2026 OpenPQL, Inc. | Founded June 2025*
