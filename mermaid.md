Markdown
# Test Mermaid

```mermaid

---
config:
  layout: elk
---
flowchart LR
 subgraph CH["Customer Channels"]
        APP["Mobile App / Web"]
        CRM["Agent CRM / Call Center"]
        POS["Retail POS"]
        IVR["IVR USSD SMS"]
  end
 subgraph EDGE["Edge Services & Identity"]
        WAF["API Gateway WAF"]
        IDP["Identity & Consent EntraID CIAM CMP"]
        CDP["CDP Event SDK"]
  end
 subgraph DEC["Real-time Decisioning"]
        CTX["Context Builder\nSession + Profile + Intent"]
        FS_RT["Feature Store Online"]
        MSERV["Model Serving Scoring API\nML runtime low-latency"]
        RULES["Decisioning & Eligibility Engine\nBRMS ODM PEGA"]
        ARB["Arbitration & Offer Ranking"]
        OCAT["Offer Catalog Service\nTMF620 Product Catalog"]
  end
 subgraph DATA["Data, Analytics & MLOps"]
        KAFKA["Streaming Bus Kafka EDA"]
        DWH["Customer 360 Lakehouse DWH Lake"]
        FS_B["Feature Store Offline"]
        TRAIN["Model Training\nAutoML Notebooks Spark"]
        EXP["A B Testing & Experimentation"]
        ATTR["Attribution & MMM MTA"]
        MON["Model & Decision Monitoring\nDrift Bias Latency"]
        CATALOG["Data Catalog & Lineage"]
  end
 subgraph BSSOSS["BSS OSS & Core Systems"]
        CRM_SYS["CRM & Order Mgmt TMF629 622 621"]
        BILL["Billing Charging OCS"]
        CDR["Usage CDR Mediation"]
        NET["Network Analytics QoE"]
        CAMPAIGN["Outbound Campaign Mgr\nJourney Batch SMS Email Push"]
  end
 subgraph GOV["Security Governance & Compliance"]
        DLP["DLP PII Tokenization"]
        POL["Policy Data Access Governance"]
        AUD["Audit Consent Ledger"]
  end
    APP --> WAF
    CRM --> WAF
    POS --> WAF
    IVR --> WAF
    WAF --> IDP & CDP & APP & CRM & POS & IVR
    IDP --> CTX
    CTX --> FS_RT & MSERV
    FS_RT --> MSERV
    MSERV --> RULES & MON
    OCAT --> RULES
    RULES --> ARB & MON
    ARB --> WAF & CAMPAIGN
    APP -- click/view/purchase --> CDP
    CRM -- agent accept/decline --> CDP
    POS -- redemption --> CDP
    IVR -- response --> CDP
    CDP --> KAFKA
    CDR --> KAFKA
    CRM_SYS --> KAFKA
    BILL --> KAFKA
    NET --> KAFKA
    KAFKA --> DWH
    DWH --> FS_B & EXP & ATTR
    FS_B --> TRAIN & FS_RT
    TRAIN --> MSERV
    EXP --> ARB
    CAMPAIGN --> APP & IVR & POS
    DLP -.-> DATA
    POL -.-> DATA & DEC
    AUD -.-> IDP & CAMPAIGN
