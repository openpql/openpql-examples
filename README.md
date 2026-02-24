# OpenPQL Examples

**Policy Query Language for AI-First Governance**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![PQL Version](https://img.shields.io/badge/PQL-v1.4-green.svg)](https://openpql.com)
[![Examples](https://img.shields.io/badge/Examples-50+-orange.svg)](./examples)

> **WYCIWYG™** - What You Compile Is What You Govern™

Founded in June 2025, OpenPQL is building the world's first governance compiler. This repository contains **PQL code examples and language documentation** - the compiler is proprietary technology protected by 57 USPTO filings.

---

## 🧠 The Seven Principles of AI-First Development

OpenPQL embodies a new paradigm for building AI-powered systems. These principles guided our architecture:

### **1. AI Intent Over Implementation**

Express *what you want*, not *how to build it*.

**Traditional Approach:**
```python
# Imperative: Tell the system HOW to do it
if customer.tier == "enterprise" and risk_score > 0.8:
    provider = AnthropicProvider()
    response = provider.complete(model="claude-sonnet-4", temp=0.3)
    log_decision(response)
    return response
```

**AI-First (PQL):**
```pql
# Declarative: Tell the system WHAT you want
WHEN customer.tier == "enterprise" AND risk_score > 0.8 THEN {
    provider: "anthropic",
    model: "claude-sonnet-4",
    explainability: "required",
    compliance_mode: "strict"
}
```

The runtime handles HOW. You specify WHAT.

### **2. Declarative AI Orchestration**

Orchestrate AI providers, models, and workflows through declarations, not code.

```pql
INTENT fraud_detection {
    triggers: ["transaction_analysis"],
    context: [transactions, customer_profiles, fraud_patterns],
    
    conditions: {
        # Ensemble for high-risk
        WHEN amount > 10000 AND location != customer.home THEN
            provider: "ensemble"
            models: ["claude-sonnet-4", "gpt-4-turbo"]
            consensus_required: true
        
        # Fast path for normal transactions
        DEFAULT
            provider: "anthropic"
            model: "claude-haiku"
    }
}
```

No SDK calls. No API wrappers. Pure business logic.

### **3. Adaptive State Synchronization**

The system adapts to changing conditions without code changes.

```pql
WHEN provider_latency > 2000ms THEN
    fallback: "faster_model"

WHEN cost_per_request > 0.05 THEN
    optimize: "cost_over_speed"

WHEN compliance_audit_active == true THEN
    logging: "comprehensive"
    explainability: "mandatory"
```

Conditions trigger adaptations. The runtime synchronizes state.

### **4. Prompt Inheritance and Composition**

Reuse governance patterns across regulations.

```pql
TEMPLATE RiskAssessment {
    WHEN risk_score > {{threshold}} THEN
        provider: "{{high_risk_provider}}"
        explainability: "detailed"
}

# Inherit for different use cases
INTENT credit_risk USES RiskAssessment {
    threshold: 0.9,
    high_risk_provider: "gpt-4-turbo"
}

INTENT fraud_risk USES RiskAssessment {
    threshold: 0.7,
    high_risk_provider: "claude-sonnet-4"
}
```

Write once. Compose everywhere.

### **5. Context-Aware AI Routing**

Route requests based on context, not hardcoded logic.

```pql
INTENT customer_service {
    context: [customer_profile, ticket_history, product_usage],
    
    conditions: {
        # VIP customers → premium model
        WHEN customer.lifetime_value > 100000 THEN
            provider: "anthropic"
            model: "claude-opus"
            sla: "1_minute"
        
        # Technical issues → specialized model
        WHEN ticket.category == "technical" THEN
            provider: "openai"
            model: "gpt-4-turbo"
            knowledge_base: "technical_docs"
        
        DEFAULT
            provider: "anthropic"
            model: "claude-haiku"
    }
}
```

Context drives decisions. No if/else pyramids.

### **6. Observable AI Operations**

Every AI decision is traceable, auditable, and explainable.

```pql
MONITOR ai_operations {
    metrics: [
        "response_time",
        "accuracy_score",
        "cost_per_request",
        "compliance_violations"
    ],
    
    alerts: {
        accuracy_score < 0.95: escalate("ai_team"),
        compliance_violations > 0: escalate("legal_team")
    },
    
    audit_trail: {
        every_request: true,
        retention: "7_years",
        immutable: "blockchain_anchored"
    }
}
```

Observability is declarative, not bolted on.

### **7. Progressive AI Enhancement**

Start simple. Add sophistication as needed.

```pql
# V1: Basic routing
INTENT analyze_contract {
    DEFAULT
        provider: "anthropic"
        model: "claude-haiku"
}

# V2: Add risk-based routing
INTENT analyze_contract {
    WHEN contract_value > 1000000 THEN
        provider: "anthropic"
        model: "claude-sonnet-4"
    DEFAULT
        provider: "anthropic"
        model: "claude-haiku"
}

# V3: Add ensemble for critical decisions
INTENT analyze_contract {
    WHEN contract_value > 1000000 THEN
        provider: "ensemble"
        models: ["claude-sonnet-4", "gpt-4-turbo"]
        consensus_required: true
    DEFAULT
        provider: "anthropic"
        model: "claude-haiku"
}
```

Each version is production-ready. No rewrites.

---

## 🎯 Why This Matters

**The industry lies about governance.**

Every GRC vendor promises "3-click compliance" and "configuration-based governance." But governance isn't easy. It's complex, precise work requiring mathematical correctness, cryptographic proof, and regulatory auditability.

That's why we built OpenPQL—**for teams who understand that governance is compiled, not configured.**

### **The TypeScript Parallel**

TypeScript published their language specification publicly while keeping the compiler proprietary initially. This strategy:
- ✅ Built massive developer adoption
- ✅ Established the language standard
- ✅ Protected core IP (compiler implementation)
- ✅ Enabled ecosystem growth

We're following the same playbook. PQL syntax is open. The 5-stage compilation pipeline (Lexer → Parser → Semantic → ExecIR → Artifacts) and Ω-SGK routing algorithms remain our moat.

---

## 📚 Documentation

- 🚀 **[Quick Start Guide](./docs/quick-start.md)** - Get started in 5 minutes
- 📖 **[Complete Language Reference](./docs/pql-language-reference.md)** - Enterprise user's guide (50+ pages)
- 🎓 **[PQL Syntax Guide](./docs/pql-syntax.md)** - Essential syntax patterns
- 🤝 **[Contributing](./CONTRIBUTING.md)** - Add your regulation examples

---

## 📚 Examples by Regulation

### **[EU AI Act](./examples/eu_ai_act/)** - Articles 5-85
- ✅ Prohibited Practices Detection (Article 6)
- ✅ Risk Management Systems (Article 9)
- ✅ Data Governance (Article 10)
- ✅ Transparency Requirements (Article 13)
- ✅ Human Oversight (Article 14)
- ✅ Robustness & Accuracy (Article 15)

### **[GDPR](./examples/gdpr/)** - All 99 Articles
- ✅ Consent Management (Article 6)
- ✅ Right to Erasure (Article 17)
- ✅ Data Portability (Article 20)
- ✅ Privacy by Design (Article 25)

### **[HIPAA](./examples/hipaa/)** - Privacy & Security Rules
- ✅ PHI Access Controls
- ✅ Minimum Necessary Rule
- ✅ Breach Notification Requirements

### **[Basel III / AML](./examples/aml/)** - Financial Compliance
- ✅ Customer Risk Assessment (CDD/KYC)
- ✅ Transaction Monitoring (AML-396)
- ✅ Sanctions Screening (OFAC)

---

## 🎯 Quick Start

### **Example: EU AI Act Article 6 - Prohibited Practices**

```pql
# Detect manipulation techniques in AI systems
INTENT detect_prohibited_practices {
    triggers: ["ai_system_execution"],
    context: [ai_output, user_profile],
    
    conditions: {
        # Article 6(1)(a) - Subliminal manipulation
        WHEN manipulation_score > 0.7 THEN {
            prohibited_practice_type: "subliminal_manipulation",
            article_reference: "6_1_a",
            risk_level: "critical",
            compliance_action: "block_immediately"
        }
        
        # Article 6(1)(b) - Exploitation of vulnerabilities
        WHEN user.age < 18 AND psychological_pressure_detected == true THEN {
            prohibited_practice_type: "child_exploitation",
            article_reference: "6_1_b",
            risk_level: "critical",
            compliance_action: "block_and_report"
        }
    }
}
```

**This PQL compiles to:**
- FastAPI governance microservice
- PostgreSQL audit schema
- Cryptographic evidence chains
- Real-time compliance dashboards

---

## 🔬 PQL Language Features

### **Declarative Compliance Logic**
```pql
WHEN customer.country IN sanctions_list THEN
    deny: "Sanctioned jurisdiction" WITH {
        regulation: "OFAC",
        severity: "blocking"
    }
```

### **Context-Aware Routing**
```pql
context: [customer_data, transaction_history, watchlist_screening]
```

### **Multi-Framework Orchestration**
```pql
requires: [gdpr_consent_check, hipaa_authorization, sox_audit_trail]
```

### **v1.4 Hybrid Syntax (Object Returns)**
```pql
WHEN risk_detected THEN {
    risk_type: "high_value_transfer",
    risk_score: 0.85,
    mitigation_required: true
}
```

---

## 📖 Documentation

- **[PQL Syntax Guide](./docs/pql-syntax.md)** - Complete language reference
- **[PQL Best Practices](./docs/best-practices.md)** - Production patterns
- **[Regulation Mapping](./docs/regulation-mapping.md)** - Law → PQL examples

---

## 🏗️ OpenPQL Platform Architecture

These examples compile via the **OpenPQL GovernFour™ Platform**:

- **⟨ / ⟩ GovernOr™** - Policy compilation engine (PQL → ExecIR)
- **⟨⚡⟩ GovernOps™** - Runtime execution with Ω-SGK routing
- **⟨👁⟩ GovernEye™** - Audit evidence generation (AEaaS)
- **⟨🦈⟩ GovernSHARK™** - Shift-left compliance validation

**Compilation Performance:**
- 0.6 seconds (PQL → production artifacts)
- ~80 artifacts generated per framework
- O(1) shard routing for million-transaction scale

---

## 🚀 Using These Examples

### **Option 1: Study the Syntax**
Read the examples to understand how to express compliance policies as code.

### **Option 2: Request Beta Access**
The OpenPQL compiler is in private beta. Contact us for access:
- 🌍 [Website](https://openpql.com)
- 🤖 [NISHKA AI Beta](https://nishka.ai) (AI-powered PQL generator)
- 📧 [Contact](mailto:nishanth.voduru@openpql.com)

### **Option 3: Enterprise Partnership**
For regulated enterprises (FinTech, HealthTech, AI platforms):
- Custom regulation libraries
- Dedicated compliance engineering
- On-premise deployment
- 24/7 support with SLAs

---

## 🎓 Educational Use

**These examples are provided for educational purposes to demonstrate:**
1. How compliance policies can be expressed as compilable code
2. The declarative nature of governance logic
3. Multi-regulation orchestration patterns

**They are NOT:**
- A substitute for legal advice
- Complete compliance implementations
- Ready for production without review

Always consult qualified legal counsel for compliance decisions.

---

## 🤝 Contributing

We welcome contributions of PQL examples for additional regulations:

1. Fork this repository
2. Add examples following our structure (see [CONTRIBUTING.md](./CONTRIBUTING.md))
3. Submit a pull request

**Note:** This repo contains examples only. The OpenPQL compiler is closed-source.

---

## 📜 License

Apache 2.0 License - See [LICENSE](./LICENSE)

**PQL Syntax:** Open specification  
**OpenPQL Compiler:** Proprietary (57 USPTO filings)

---

## 🌐 Resources

- 🌍 [OpenPQL Website](https://openpql.com)
- 🤖 [NISHKA AI](https://nishka.ai) - AI-powered compliance code generation
- 💼 [LinkedIn](https://linkedin.com/company/openpql)
- 🐦 [Twitter](https://twitter.com/openpql)
- 📧 [Contact](mailto:nishanth.voduru@openpql.com)

---

## ⭐ Star This Repo

If you find these examples useful, please star the repo to help others discover policy-as-code!

---

**Built with precision. Compiled with confidence. Governed with cryptographic proof.**

*© 2025-2026 OpenPQL, Inc. Protected by 57 USPTO filings. Cincinnati, Ohio.*
