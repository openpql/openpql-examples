# OpenPQL Code Examples

**Learn Policy Query Language (PQL) through production-ready compliance examples.**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![PQL Version](https://img.shields.io/badge/PQL-v1.4-green.svg)](https://openpql.com)
[![Examples](https://img.shields.io/badge/Examples-50+-orange.svg)](./examples)

> **WYCIWYG™** - What You Compile Is What You Govern™

OpenPQL is the world's first governance compiler. This repository contains **code examples only** - the OpenPQL compiler is proprietary technology protected by 57 USPTO filings.

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
