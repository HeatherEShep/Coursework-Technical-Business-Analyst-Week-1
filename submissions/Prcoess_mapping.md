## Pain points

- Duplicate status checks: Status must be verified across multiple sources; there is no single source of truth

    Stakeholder Quotes:
    "The biggest win will be when representatives stop checking whether work was already done." — Sylvia Turner, Operations Analyst (SN-038)

    "A case marked 'resolved' in one system might be 'in progress' in another." — Compliance Liaison (SN-015)
    "I cannot tell which customers have already been contacted this month without manually checking three different sheets." — Mr Martyn Akhtar, Operations Analyst (SN-063)
    Source Dataset Evidence:
    2,858 activities (28.90% of all activity volume) in recovery activity tracker are consumed purely by status cross-checks: 1,400 status_check tasks and 1,458 spreadsheet_reconcile tasks.
    2,020 activities (20.42%) in recovery activity tracker are explicitly flagged with duplicate_check_flag = 'Y'.
    Activities are split almost evenly across 4 separate repositories without a unified system of record: phone (2,495), spreadsheet (2,492), legacy_db (2,453), and email (2,450).
    Operational Observation: Representatives cannot trust system indicators and are forced to perform pre-contact cross-checks across multiple spreadsheets and databases before dialing or emailing a debtor.

- Repeated customer contact attempts: Representatives cannot see whether others have already contacted the customer; duplicate outreach is common

    Stakeholder Quotes:
    "The collections database does not sync with the email tracker, so representatives often re-contact customers who were already promised callbacks." — Christopher Richards, Collections Rep (SN-011)
    "Customers go through the contact process multiple times because we have no way to prevent re-contact." — Diana White, Collections Rep (SN-028)
    Source Dataset Evidence:
    4,204 direct contact events were recorded in recovery activity tracker across 3,214 accounts (1,425 SMS, 1,397 calls, 1,382 emails).
    Out of 2,450 contacted accounts in Delinquent accounts, 1,234 accounts (50.37% of contacted accounts) suffered multiple contact attempts (up to 7 calls/emails/texts per account).
    An average of 3.08 activities per active account are performed in the logged window.
    Operational Observation: Lack of shared real-time outreach status leads to uncoordinated, overlapping touchpoints from different agents on different shifts, causing customer harassment complaints.

- Spreadsheet version/ownership conflicts: multiple spreadsheet versions in circulation; unclear ownership and inconsistent updates

    Stakeholder Quotes:
    "The spreadsheet is now two hundred sheets thick and no one knows what half of them do." — Dr Lynda Smith, Operations Analyst (SN-025)
    "Every new tool we add makes the job harder because it adds another place where data can get out of sync." — Simon Burns, Compliance Liaison (SN-062)
    "New representatives take two weeks longer to reach productivity because they have to learn the spreadsheet system." — Ronald Rees, Collections Rep (SN-020)
    Source Dataset Evidence:
    2,492 activities (25.20% of recovery activity tracker) cite source_system = 'spreadsheet' as the primary workspace.
    58 unique representatives (representative_1 through representative_58) concurrently update offline sheets without row-level locking or centralized master ownership.
    1,233 activities (12.47%) produced an outcome of updated_row, reflecting manual line-by-line spreadsheet maintenance.
    Operational Observation: Frontline teams create private copies and ad-hoc sheets with custom formulas to bypass legacy tools, fragmenting data history and leaving no audit trail.

- Missed next action due to manual tracking: Next actions rely on individual memory and manual entries; high risk of missed follow ups

    Stakeholder Quotes:
    "We have cases sitting in 'awaiting callback' status for months because the promised date was never recorded." — Lawrence Bennett, Finance Analyst (SN-007)
    "Cases get stuck in 'pending callback' status indefinitely because the callback date is never enforced." — Dr Louis Sinclair (SN-053), Service Design Lead & Amina Rahman (SN-118)
    "We lose at least 20% of follow-ups because they fall between shifts and no one owns the handoff." — Catherine Frost, Data Analyst (SN-040) & Lawrence Bennett (SN-105)
    Source Dataset Evidence:
    1,465 activity records (14.81% of recovery activity tracker) have a completely blank/missing next_follow_up_date.
    2,508 activities (25.36%) ended in limbo with next_action_unclear (1,275) or awaiting_review (1,233).
    1,059 activities (10.71%) recorded a follow-up date set on or before the activity date itself, rendering follow-up prompts immediately defunct.
    Operational Observation: Without system-enforced task scheduling, callbacks exist only as freeform notes. When agents change shifts or take leave, accounts lapse into unmanaged operational blind spots.

- Multiple Customer Contacts for Simple Inquiries: The customer has to be contacted multiple times for simple things like balance confirmations or repayment plan setups.

    Stakeholder Quotes:
    "Customers call back three times because they do not remember what they were told on the first call." — Daniel Okoye, Finance Business Partner (SN-002)
    "Most customers do not even know they can pay online; they think they have to call." — Eleanor Clark, Service Design Lead (SN-017)
    "Customers would pay more readily if they understood exactly what they owe and could see options." — Dr Lynda Smith, Operations Analyst (SN-065)
    Source Dataset Evidence:
    2,516 accounts (77.51% of Delinquent accounts) are classified as self_service_candidate = 'Y'.
    Despite being prime self-service candidates, 1,903 of these accounts (75.64%) required manual representative contact (948 received 2 or more manual contacts).
    Operational Observation: Routine balance inquiries and standard 3–12 month installment setups consume frontline phone capacity because debtors lack self-service balance transparency and digital payment sliders.

- Poor visibility of promise-to-pay fulfillment: No automated tracking; fulfillment status is unclear until manually checked and reconciled

    Stakeholder Quotes:
    "The current system treats payment promises the same as payment confirmations, which creates confusion." — Veronica Cole, Compliance Officer (SN-112) & Christopher Richards (SN-126)
    "If a customer pays even a small amount, the whole case gets reclassified and we lose months of history." — Robert Quinn (SN-044) & Kimberley Richards-Stokes (SN-104)
    Source Dataset Evidence:
    1,195 activities across 1,007 unique accounts in recovery activity tracker resulted in promise_to_pay.
    In Delinquent accounts, these 1,007 accounts remain scattered across contradictory status codes rather than an automated pipeline:
    awaiting_follow_up: 212 accounts (20.76%)
    legal_watch: 111 accounts (10.87%)
    plan_requested: 106 accounts (10.38%)
    promise_due: 106 accounts (10.38%)
    specialist_review: 101 accounts (9.89%)
    manual_follow_up: 94 accounts (9.21%)
    Operational Observation: When a debtor agrees to pay, the system cannot verify if funds cleared. Agents must manually check bank feeds or ledger lines days later to determine whether the promise was honored or broken.

- Everything is logged manually: risk of human error, hard to track contact attempts and follow ups

    Stakeholder Quotes:
    "Every status update in the old system requires manual re-keying into the spreadsheet." — Daniel Okoye, Finance & Compliance Director (SN-111)
    "We are paying representatives to hunt for information that should already be on the screen." — Mr Dale Jackson, Collections Rep (SN-087)
    "Representatives spend time proving what they did rather than doing more work." — Karl Lewis-Warren, Operations Analyst (SN-027)
    Source Dataset Evidence:
    Total manual operational time logged across 9,890 activities is 69,226 minutes (1,153.8 hours).
    Pure administrative record-keeping (spreadsheet_reconcile, status_check, and manual_plan_note) consumes 30,024 minutes (500.4 hours) — 43.37% of all representative effort.
    Manual plan notes average 7.51 minutes each (1,405 tasks), and status lookups average 4.53 minutes each (1,400 tasks).
    Operational Observation: Frontline staff spend more than 40% of their working hours manually typing notes, updating cell colors, and re-keying account numbers between legacy green-screens and desktop sheets.


- The Endless "Contact Loop" & Lapsed Follow-Ups: If customers do not pay on time or respond, it relies on repeated follow-ups. Follow-ups are often forgotten.

    Stakeholder Quotes:
    "The contact strategy is reactive—we contact people only when collections escalates them." — Amina Rahman, Operations Head (SN-045)
    "We reach out to customers in a random order rather than any strategic sequence." — Clare Willis (SN-077), Priya Nair (SN-078), Mr Dale Jackson (SN-119)
    "We have more accounts in the system than our representatives can possibly contact in a reasonable timeframe." — Dr Louis Sinclair, Service Design Lead (SN-023)
    Source Dataset Evidence:
    8,276 activity records (83.68% of recovery activity tracker) feature a next_follow_up_date that expired prior to the dataset end date (2026-03-07).
    2,979 accounts (92.69% of all 3,214 active accounts in recovery activity tracker) have their latest scheduled follow-up in the past.
    Out of 1,397 call attempts, 255.2 total hours were spent dialing, yet 1,234 accounts remained trapped in recurring 2-to-7 touchpoint loops.
    Operational Observation: Queues lack cadence intelligence. Agents dial from unsorted lists, miss expired follow-ups, and restart contact sequences from scratch without context.

- Manager reporting based on reconciliation rather than live status: Reporting depends on manual reconciliation of spreadsheets and database entries; no real time visibility

    Stakeholder Quotes:
    "Every month the finance team has to reconcile our activity count with the database, and they never match." — Christopher Richards, Collections Rep (SN-123)
    "The finance team cannot forecast recovery revenue because they do not trust the activity data." — Daniel Farmer, Finance Analyst (SN-070)
    "Reporting takes so long that by the time we see the numbers, they are already out of date." — Daniel Farmer, Finance Analyst (SN-048)
    "The data quality is so poor that we stopped running management reports altogether." — Ms Andrea Lamb, Collections Rep (SN-012)
    Source Dataset Evidence:
    1,458 dedicated spreadsheet_reconcile tasks are logged in recovery activity tracker (14.74% of all activity).
    Manual reconciliation consumes 13,123 minutes (218.7 hours) of staff labor, averaging 9.00 minutes per reconciliation event.
    Operational Observation: Management lacks live dashboards. Finance and operations leads must spend the final week of each month stitching together mismatched exports, resulting in stale steering data and blind decision-making.

- Vulnerability Detection & Regulatory Exposure: Vulnerable customers and hardship cases are handled in the same batch as routine debtors, creating direct compliance and Consumer Duty exposure.

    Stakeholder Quote: "Cases involving vulnerable customers are not flagged differently from routine cases." — Stewart Howell, Operations Analyst (SN-069)
    Source Dataset Evidence:
    In Delinquent accounts, 519 accounts (15.99%) carry risk_flag = 'Y', accounting for £492,049.16 in overdue debt.
    These high-risk accounts undergo standard automated SMS and call cadences rather than being protected by an immediate hold or assigned to a specialist.

- High Financial Value Trapped in Unmanaged Delinquency: Inefficient contact sequencing allows early delinquent debt to age into costly, low-recovery late stages.
    Stakeholder Quote: "We lose customers because the recovery process is so slow they lose faith we will ever resolve it." — Daniel Farmer, Finance Analyst (SN-032)
    Source Dataset Evidence:
    The portfolio in Delinquent accounts carries £3,052,004.20 in overdue balances across a £26,559,358.36 total balance.
    1,504 accounts (46.34%) have progressed into Mid Delinquency (987 accounts, 30.41%) or Late Delinquency (517 accounts, 15.93%), where recovery odds decline significantly.

- Escalation Queue Bottlenecks: Escalations are used as an administrative holding pen rather than an exception flow.

    Stakeholder Quote: "Straightforward cases get delayed because they are queued behind complex ones with no priority logic." — Barry Skinner, Operations Analyst (SN-029)
    Source Dataset Evidence:
    1,423 activities (14.39% of recovery activity tracker) are classified as escalation, consuming 12,025 minutes (200.4 hours) of senior team capacity (averaging 8.45 minutes per task).

- Customer Handover Friction & Transfer Fatigue: Inability to access previous customer notes forces customers to recount their situation each time they interact with a new representative.

    Stakeholder Quote: "Customers get transferred between departments and have to repeat their entire situation each time." — Robert Quinn, Process Improvement Lead (SN-036)
    Source Dataset Evidence:
    58 different representatives handle touchpoints across 4 different platforms with 1,405 separate manual_plan_note entries, none of which synchronize into an complete, visible timeline.

## How the current process feels

### Customer

The process feels slow, repetitive, and confusing. Customers are contacted multiple times by different representatives, asked to repeat information, and often wait for updates because follow ups aren't triggered consistently. They don't have a clear way to check their balances or next steps themselves, so simple issues turn into long, drawn out interactions. 

### Collections representatives

The process feels fragmented and mentally exhausting. Representatives spend more time checking spreadsheets, email trails, and database entries than actually helping customers. They worry about missing next actions because everything is tracked manually, and they often duplicate work because they can't see what colleagues have already done. Much of their is spent recording information rather than using judgement on the accounts that need it. 

### Team Leader

The process feels unclear and unreliable. Managers don't have rea time visibility of what's happening across over 100,000 delinquent accounts, so reporting becomes a manual reconciliation task rather than a live operational view. They struggle to spot missed follow ups, fulfillment of promises to pay, or emerging risks because the data is scattered across spreadsheets and inconsistent updates. Their confidence in the process is low because the system can't scale with demand. 

## Best self-service/automation candidates

1. Balance confirmation and account status lookup

- Current step: Representative checks legacy account status
- Reasons:
    - High volume
    - Purely data retrieval 
    - No judgement required
    - Customers frequently call just to confirm balance, due dates, or status

Automation opportunity: 
    A customer portal showing balance, missed installments, amount owed, age of debt, next payment date, and any open actions.

2. Reviewing past contact attempts/communication history

- Current step: Representative cross checks spreadsheet and email history
- Reasons:
    - Highly repetitive
    - Rules driven
    - Causes duplicate outreach

Automation opportunity: 
    A unified timeline showing all contact attempts, visible to both customers and representatives. 

3. Capturing simple outcomes

- Current step: Representative manually records outcome
- Reasons:
    - High volume
    - Standardised outcomes
    - No judgement required for many simple cases

Automation opportunity:
    Self-service outcome capture (customer selects reason, conforms next step).

4. Promise to pay creation and tracking

- Current step: Representative manually tracks promise to pay
- Reasons:
    - Rules driven
    - High risk of manual error
    - High operational volume 

Automation opportunity:
    Customers set their own promise to pay date through a portal, system auto tracks fulfillment. 

5. Scheduling follow ups for non-responsive customers

- Current step: Representative manually schedules follow up
- Reasons:
    - Purely administrative
    - Triggered by simple rules (no response, follow up in X days)

Automation opportunity: 
    Automated follow up scheduling based on configurable rules.

6. Customer self-resolution of straightforward cases

- Current step: Representative contacts customer to discuss plan and logs the next actions
- Reasons:
    - Many cases require no human judgement
    - Customers often just need to:
        - Confirm balance
        - Choose a payment option
        - Request time
        - Make a payment

Automation opportunity:
    Self serve portal allowing customers to resolve low complexity cases without waiting for a representative. 


