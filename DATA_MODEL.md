# MoPhones Repeatable Reporting Data Model (Sketch)

Below is a lightweight **ERD + analytics DAG sketch** for reliable credit-risk and customer-experience reporting.

---

## 1) Logical ERD (source-aligned warehouse model)

```mermaid
erDiagram
    DIM_CUSTOMER ||--o{ DIM_ACCOUNT : owns
    DIM_ACCOUNT ||--o{ FACT_ACCOUNT_SNAPSHOT : has_snapshot
    DIM_ACCOUNT ||--o{ FACT_PAYMENT : receives
    DIM_ACCOUNT ||--o{ FACT_NPS_RESPONSE : receives
    DIM_DATE ||--o{ FACT_ACCOUNT_SNAPSHOT : snapshot_date_key
    DIM_DATE ||--o{ FACT_PAYMENT : payment_date_key
    DIM_DATE ||--o{ FACT_NPS_RESPONSE : submitted_date_key

    DIM_CUSTOMER {
      string customer_key PK
      string source_customer_id
      date dob
      string gender
      string region
      decimal verified_monthly_income
      datetime created_at
      datetime updated_at
    }

    DIM_ACCOUNT {
      string account_key PK
      string source_loan_id UK
      string customer_key FK
      date sale_date
      date contract_start_date
      date contract_end_date
      int contract_duration_weeks
      decimal weekly_rate
      decimal deposit_amount
      decimal initial_pay_amount
      string product_model
      string credit_check_result
      datetime created_at
      datetime updated_at
    }

    FACT_ACCOUNT_SNAPSHOT {
      string account_snapshot_key PK
      string account_key FK
      int snapshot_date_key FK
      decimal balance
      decimal closing_balance
      decimal total_due_today
      decimal total_paid_to_date
      decimal arrears
      int days_past_due
      string account_status_l1
      string account_status_l2
      boolean is_par30
      boolean is_default_proxy
      datetime ingested_at
    }

    FACT_PAYMENT {
      string payment_key PK
      string account_key FK
      int payment_date_key FK
      datetime payment_ts
      decimal expected_amount
      decimal paid_amount
      decimal adjustment_amount
      decimal prepayment_amount
      decimal overpayment_amount
      string payment_channel
      string payment_status
      datetime ingested_at
    }

    FACT_NPS_RESPONSE {
      string nps_response_key PK
      string account_key FK
      int submitted_date_key FK
      datetime submitted_ts
      int nps_score
      string nps_bucket
      string main_reason
      string improve_suggestion
      string service_support_rating
      string device_quality_rating
      datetime ingested_at
    }

    DIM_DATE {
      int date_key PK
      date full_date
      int year
      int quarter
      int month
      int week
      boolean is_month_end
      boolean is_quarter_end
    }
```

### Why this works
- **Customer → Account → Snapshot/Payment/NPS** enables both lifecycle and point-in-time reporting.
- Separate facts prevent duplication and allow clean metric definitions:
  - delinquency from `fact_account_snapshot`
  - cashflow/consistency from `fact_payment`
  - customer sentiment from `fact_nps_response`
- `dim_date` standardizes time-series logic across all marts.

---

## 2) dbt-style DAG (reporting layer)

```mermaid
flowchart LR
    A[(stg_credit_snapshot)] --> C[(int_account_snapshot_enriched)]
    B[(stg_nps_response)] --> F[(int_nps_enriched)]
    D[(stg_payment_txn)] --> E[(int_payment_enriched)]
    G[(stg_customer)] --> H[(dim_customer)]
    I[(stg_account)] --> J[(dim_account)]
    K[(dim_date)] --> C
    K --> E
    K --> F
    H --> C
    J --> C
    J --> E
    J --> F

    C --> M[(fct_account_snapshot)]
    E --> N[(fct_payment)]
    F --> O[(fct_nps_response)]

    M --> P[(mart_portfolio_health)]
    N --> P
    M --> Q[(mart_collections_rollrate)]
    N --> Q
    M --> R[(mart_credit_x_nps)]
    O --> R

    P --> S[(exec_dashboard_credit)]
    Q --> S
    R --> S
```

### Brief annotations
- `stg_*`: source cleaning, type casting, column normalization, de-duplication.
- `int_*`: business-rule application (default proxy, PAR flags, tenure bands, nps buckets).
- `fct_*`: conformed atomic facts with surrogate keys.
- `mart_*`: KPI-ready reporting tables for portfolio, collections, and credit×experience views.

---

## 3) Minimum governance for repeatability
- **Metric contracts**: centrally define PAR30, default, repayment rate, active/closed ratio.
- **Status dictionary**: controlled mappings for `account_status_l1/l2`.
- **Freshness tests**: snapshot timeliness and row-count anomaly checks.
- **Key integrity tests**: `source_loan_id` uniqueness, FK coverage from facts to dimensions.

