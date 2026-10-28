# Intent: Results-ready notification (PRD N-17)

Sources: `inputs/01-approved-prd.md` (PRD N-17, approved 2026-09-18), `inputs/02-current-meeting.md`
(discovery notes, 2026-09-20). `inputs/03-superseded-request.md` (2026-08-02) is superseded by PRD N-17;
it is historical context only and approves nothing in this intent.

## Problem

- **I-1** The fictional clinic receives avoidable calls from patients checking whether their results
  are ready. (PRD, Problem and outcome)

## Proposed outcome

- **I-2** The patient is notified when a result is ready for their review in the existing authenticated
  portal. (PRD, Problem and outcome)
- **I-3** "Ready" means a doctor has reviewed **and** released the result. Only then is a notification
  eligible; a completed laboratory upload alone never triggers one. (PRD, Approved constraints;
  discovery notes, product owner)

**How success will be observed**

- **I-4** Reduction in status-only calls ("are my results ready?"), counted separately from clinical
  questions and compared against a measured baseline. (PRD, Problem and outcome; discovery notes,
  support lead)
- **I-5** Delivery failures of notifications are measured. (PRD, Problem and outcome)
- **I-6** No baseline or numerical target is approved yet; both will be agreed during discovery. This
  intent sets no target. (PRD, Problem and outcome)

## Affected users and systems

- **Patients**: the only approved recipients of the notification. (PRD, Problem and outcome)
- **Doctors**: review and release results; their release is the notification gate. (PRD, Approved constraints)
- **Clinic support staff**: receive the status calls and own the call counting. (Discovery notes, support lead)
- **Existing authenticated patient portal and its existing result route**: where the notification
  directs the patient; engineering considers it adequate. (PRD, Scope; discovery notes, engineering lead)
- **Notification delivery and its logs**: must carry no clinical content. (PRD, Approved constraints)

## Out of scope

- **I-7** Portal redesign. (PRD, Scope)
- **I-8** A new or rebuilt patient dashboard: a separate project. (Discovery notes, engineering lead)
- **I-9** Appointment scheduling. (PRD, Scope)
- **I-10** Clinical interpretation of results. (PRD, Scope)
- **I-11** Notifying third parties. (PRD, Scope) The referring doctor is not approved either; it is
  tracked separately as OPEN-2.
- **I-12** Everything else from the superseded request is excluded: sending results as soon as the lab
  uploads them, including the test result in an SMS, copying the referring doctor, rebuilding the
  patient dashboard and the 90%-in-one-week call reduction target. (Superseded request; PRD N-17)

## Constraints

- **C-1** A doctor must review and release the result before any notification is eligible. (PRD, Approved constraints)
- **C-2** The message says only that an update is available and directs the patient to the existing
  authenticated portal. No diagnosis, test result, clinical measurement or treatment detail goes in the
  message or in notification and operational logs. (PRD, Approved constraints; discovery notes, privacy owner)
- **C-3** Access is authenticated in the existing portal. No results are attached and no public result
  link is introduced. (PRD, Approved constraints)
- **C-4** No duplicate notifications for the same released result version. (PRD, Approved constraints)
- **C-5** Delivery failures are handled without sending the patient duplicate messages. (PRD, Approved constraints)
- **C-6** Use the existing portal result route. (PRD, Scope)

## Open questions and owners

- **OPEN-1 Channel** (SMS, email or portal push): not decided. Owners: **product owner** and **privacy
  owner**, after the consent and delivery review. (PRD, Unresolved decisions; discovery notes, privacy owner)
- **OPEN-2 Referring-doctor notification**: not approved; recipient authorization to be decided. Owners:
  **clinical owner** and **privacy owner**. Approval must not be inferred from the superseded request.
  (PRD, Unresolved decisions; discovery notes, clinical owner)

## Decision record

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
