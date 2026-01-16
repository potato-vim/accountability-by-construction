# accountability-by-construction

## Norm ⇒ System Duality: A Formal Report

> Political position statement through formal structure
> This document intentionally avoids ideology, analogy, and metaphor,
> and instead presents a minimal mathematical structure for public systems.

---

## 0. Executive Summary

This repository presents a formal framework describing the relationship between:

- **Norm**: rules, rights, obligations, and justifications
- **System**: implementations, procedures, and observable operations

The core claim is that their relationship is **not a one-way translation**, but a
**dual constraint structure**, formalized using order-theoretic duality.

No historical mathematical theory names are required to understand or apply this framework.

```mermaid
flowchart LR
    subgraph Norm["Norm (Normative Domain)"]
        N1[Person]
        N2[Rights]
        N3[Obligations]
    end

    subgraph System["System (Operational Domain)"]
        S1[Identifiers]
        S2[Credentials]
        S3[Audit Logs]
    end

    Norm <-->|"η : Dual Connection"| System
```

---

## 1. Norm (Normative Domain)

### Objects
Units that can demand justification.

- Person
- Data subject
- Right bundle
- Obligation bundle
- Institutional procedure

### Morphisms
Justification-preserving transformations.

- consent
- revocation
- mandate
- audit request
- remedy request

---

## 2. System (Operational Domain)

### Objects
Operational entities.

- Identifiers
- Credentials
- Encrypted data
- Access policies
- Audit logs
- Recovery procedures

### Morphisms
Executable operations.

- grant / revoke
- encrypt / decrypt
- sign / verify
- log / audit
- recover

---

## 3. Dual Constraint Structure

Let:

- **P** be a partially ordered set of disclosure policies
- **A** be a partially ordered set of observational capabilities

with order representing *strength*.

Define monotone maps:

- F : P → A
- G : A → P

such that:

    F(p) ≤ a  ⇔  p ≤ G(a)

This structure is called a **dual connection**.

```mermaid
flowchart TB
    subgraph P["P: Disclosure Policies"]
        p1["p (policy)"]
    end

    subgraph A["A: Observational Capabilities"]
        a1["a (capability)"]
    end

    p1 -->|"F"| a1
    a1 -->|"G"| p1

    p1 -.->|"c = G ∘ F"| p1
    a1 -.->|"k = F ∘ G"| a1
```

---

## 4. Stabilization Operator

Define:

- c = G ∘ F

Then c is an **idempotent, monotone stabilization operator**.

Interpretation:
> c(p) is the maximum disclosure condition that remains normatively acceptable.

This operator represents the concrete decision process for η.

```mermaid
flowchart LR
    Policy["Policy p"] --> F["F: Policy → Capability"]
    F --> Capability["Capability a"]
    Capability --> G["G: Capability → Policy"]
    G --> Stabilized["Stabilized Policy c(p)"]

    Stabilized -.->|"idempotent: c(c(p)) = c(p)"| Stabilized
```

---

## 5. η Determination = Selection of Stabilization Operator

The determination of η is formulated as:
- Fix a substructure H ⊂ G
- L^H represents "permissible System observations"

```mermaid
flowchart TB
    L["System (Full)"]
    H1["Subgroup H1"]
    H2["Subgroup H2"]
    K["Norm"]

    L -->|"Fixed by H1"| H1
    L -->|"Fixed by H2"| H2
    H1 -->|"Correspondence"| K
    H2 -->|"Correspondence"| K
```

---

## 6. Observability and Structure Preservation

Only properties preserved under admissible structural equivalences
are considered observable.

This ensures:

- auditability
- recoverability
- non-arbitrary disclosure boundaries

```mermaid
flowchart LR
    subgraph Observable["Observable Properties"]
        Audit[Auditability]
        Recover[Recoverability]
        Boundary[Non-arbitrary Boundaries]
    end

    Structure["Structural Equivalence"] --> Observable
```

---

## 7. Applied Examples (Illustrative)

### Medical Data
- Policy order: anonymization strength
- Capability order: re-identification power

Stabilization yields conditionally usable datasets.

```mermaid
flowchart LR
    Raw["Raw Medical Data"] --> Anon["Anonymization Policy"]
    Anon --> Stable["Stabilized: Statistical Structure"]
    Stable --> Use["Research Use"]

    Attack["Re-identification Capability"] -.->|"bounded by"| Stable
```

### Administrative Identity
- Policy order: pseudonymity vs traceability
- Capability order: authority of inspection

Stabilization yields traceable-but-non-identifying identifiers.

```mermaid
flowchart LR
    ID["Full Identity"] --> Pseudo["Pseudonymization Policy"]
    Pseudo --> Stable["Stabilized: Traceable Pseudonym"]

    Normal["Normal Use"] --> Stable
    Judicial["Judicial Order"] -.->|"decrypt"| ID
```

### Contracts
- Policy order: disclosure scope
- Capability order: dispute resolution power

Stabilization yields verifiable outcomes without revealing full terms.

```mermaid
flowchart LR
    Contract["Full Contract Terms"] --> Scope["Disclosure Scope Policy"]
    Scope --> Stable["Stabilized: Verifiable Outcome"]

    Market["Market"] --> Stable
    Dispute["Dispute Resolution"] -.->|"access"| Contract
```

---

## 8. Economic Interpretation

- Stabilization cost corresponds to operational and legal risk
- Smaller observable sets reduce exposure but increase friction
- Verification becomes a measurable service

### Value Generation Points

| Category | Examples |
|----------|----------|
| Intermediate Structure Monetization | Norm-compliant API, Conditional disclosure design |
| η Verification Business | Audit, Certification, Insurance |
| Risk Quantification | Pricing of structural breach, Usage fees, Deposits, Premiums |

```mermaid
flowchart TB
    subgraph Value["Economic Value Sources"]
        V1["Norm-compliant API"]
        V2["Audit Services"]
        V3["Risk Pricing"]
    end

    Intermediate["Intermediate Structure<br/>(Stabilized Observable)"] --> Value
```

---

## 9. Conclusion

This framework does not advocate transparency or secrecy.

It asserts:

> Trust is not a moral property.
> Trust is a structural consequence.

### Summary

- The failure of cryptographic adoption is not technical—it is the absence of η
- η can be organized as "fixing structural equivalences" through dual connection
- The design of intermediate structures is the core that connects institution, technology, and economy

```mermaid
flowchart TB
    Problem["Crypto Adoption Failure"] --> Cause["Absence of η"]
    Cause --> Solution["Dual Connection Framework"]
    Solution --> Design["Intermediate Structure Design"]
    Design --> Integration["Institution + Technology + Economy"]
```

---

## 日本語版 / Japanese Version

### 概要

本フレームワークは暗号技術普及のボトルネックを以下のように捉える：

- **規範の圏 Norm**: 権利・義務・正当化を要求できる単位
- **実装の圏 System**: 実行可能な操作・手続き

両者の関係は**一方向の翻訳ではなく、双対的制約構造**である。

### 核心的主張

- η の決定は「どの構造的同値（権限）を固定するか」という設計問題
- その結果生じる**中間体（部分公開・条件付き公開）**が経済的価値・インセンティブの源泉

### 例示

| 領域 | 固定条件 | 中間体 |
|------|----------|--------|
| 医療データ | 研究者は匿名統計のみ | 個人性を失った統計構造 |
| 行政ID | 通常は仮名、司法命令で復号 | 行為追跡可能・人格不可視 |
| 契約・署名 | 市場には履行結果のみ | 信用のみ可視 |

### 結論

> 信頼は道徳的属性ではない。
> 信頼は構造的帰結である。
