# Mortgage Forbearance Control Analysis

A self-directed Technical Business Analyst case study exploring how a mortgage forbearance decision could be assessed, approved and carried through to execution with a clearer record of the evidence, rules and controls used.

The scenario and case data are synthetic. This repository contains business and system analysis, process models and proposed test scenarios. It does not represent a deployed system or completed implementation.

## Business Problem

In the modelled process, a customer contacts a lender because they are experiencing repayment difficulty. Information is gathered, an appropriate forbearance option is assessed, an authorised person approves the outcome, and mortgage servicing applies the agreed arrangement.

Across this process, the supporting evidence, decision rationale, approval and final implementation may sit across different stages or systems.

The central control question explored in this case study is:

**Was the arrangement applied to the customer's mortgage the exact version that was reviewed and approved?**

The analysis therefore focuses not only on reaching a decision, but on maintaining a clear relationship between:

* customer evidence
* policy and business rules
* assessment outcome
* approval
* subsequent changes
* execution
* audit history

## Scenario

TraceLogic is used in this case study as the name of a **proposed decision-governance layer** around the mortgage forbearance workflow.

The proposed design introduces additional controls around evidence validation, policy evaluation, independent approval, decision versioning and execution.

The diagrams represent an intended design for analysis purposes. They are not a verified description of any lender's current operating model and do not represent a deployed TraceLogic implementation.

## Scope and My Role

I performed the analysis as an independent Technical Business Analyst portfolio project.

The work covers:

* current-state process modelling
* proposed future-state process design
* role and system-boundary analysis
* high-level data movement
* approval and segregation-of-duties controls
* exception handling
* decision-version control
* execution-result handling
* proposed functional test scenarios

The analysis focuses on the control path from initial case intake through assessment, approval and execution.

Detailed mortgage affordability calculations and the internal design of a mortgage servicing platform are outside the documented scope.

No client engagement, stakeholder workshops, production-system access or live customer data were used in this project.

## Analysis Approach

The case study follows the mortgage forbearance decision from initial customer contact through to implementation.

The analysis considers:

1. how information enters the process
2. where evidence must be checked
3. how policy and business rules affect the decision
4. where independent approval should occur
5. what happens when a case changes after approval
6. how the approved decision is passed for execution
7. how execution failures and mismatches should be handled
8. what information should remain available for later review

The current-state model is used to identify potential handoff and control weaknesses.

The proposed future-state model then introduces explicit control points and exception paths to address those weaknesses.

## Key Deliverables

| Deliverable | What it demonstrates |
| --- | --- |
| [Business Problem and Scope](analysis/TL-E01-business-problem-and-scope.pdf) | Defines the modelled business problem, scope boundaries, stakeholders, assumptions, success measures and open questions for the mortgage-forbearance case study. |
| [Requirements, Rules and NFR Catalogue](analysis/TL-E02-requirements-rules-and-nfr-catalogue.pdf) | Defines the business requirements, functional requirements, business rules, exception rules and non-functional requirements used across the analysis. |
| [Prioritised User Stories and Acceptance Criteria](analysis/TL-E03-prioritised-user-stories-and-acceptance-criteria.pdf) | Shows how requirements were translated into eight prioritised Jira user stories with acceptance criteria and requirements traceability. |
| [Jira User Story Evidence](jira/jira-mortgage-forbearance-user-stories.xlsx) | Consolidates the Jira delivery items from SCRUM-1 through SCRUM-8, including story details, priorities, acceptance criteria and activity history. |
| [Current-state process](diagrams/current-state-mortgage-forbearance.png) · [editable source](diagrams/current-state-mortgage-forbearance.drawio) | Models the current process handoffs and the potential evidence and control gaps used as assumptions for the analysis. |
| [Future-state process](diagrams/future-state-mortgage-forbearance.png) · [editable source](diagrams/future-state-mortgage-forbearance.drawio) | Models the proposed governance gates from controlled case creation through assessment, approval, execution and outcome recording. |
| [System context](diagrams/system-context.drawio) | Shows the proposed actors, policy source, TraceLogic governance boundary and mortgage-servicing interaction. |
| [Data flow](diagrams/data-flow.drawio) | Shows the conceptual movement of case information, policy inputs, approval information and execution results. |
| [Decision and exception flow](diagrams/decision-and-exception-flow.drawio) | Models control paths for missing evidence, policy exceptions, approval, version mismatch and execution failure. |
| [Test scenarios and traceability workbook](testing/mortgage-forbearance-test-scenarios.xlsx) | Contains thirteen proposed functional, control and exception test scenarios, together with requirements, rules, NFRs, open issues and traceability. All scenarios remain **Not Run**. |

The editable diagrams can be opened using diagrams.net / draw.io.

PNG previews are included for the current-state and future-state process maps so the main workflow can be reviewed directly from GitHub.

## Key Analysis Observations

### Evidence and decision information can become separated

The modelled current process contains multiple handoffs between information collection, assessment, approval and implementation.

This creates the possibility that supporting evidence, approval rationale and implementation instructions could become separated.

This is a **scenario assumption used for analysis**, not a measured finding about a real lender.

### Approval alone does not guarantee correct execution

An approved decision can still create risk if the case changes after approval or if the version sent for execution differs from the version originally approved.

The proposed process therefore introduces a comparison between the approved decision version and the version submitted for execution.

### Exceptions require explicit control paths

The proposed flow treats exceptions as part of the process rather than as informal deviations.

Examples modelled include:

* incomplete or missing evidence
* policy exceptions
* attempted self-approval
* material case change following approval
* duplicate authorisation
* decision-version mismatch
* mortgage servicing execution failure

## Proposed Control Model

The future-state analysis introduces several control concepts.

### Evidence Validation

Required evidence should be present before the case progresses to decision and approval.

### Policy Evaluation

The proposed decision should be assessed against the relevant policy or business rules.

### Independent Approval

Where approval is required, the approving role should be independent from the person who performed the original assessment.

### Decision Version Control

Material changes after approval should invalidate or supersede the previous approval rather than allowing an outdated decision to proceed.

### Controlled Execution

The version submitted for execution should correspond to the version that was approved.

### Execution Result

The process should capture whether the servicing action succeeded, failed or requires further intervention.

### Audit History

Evidence, decision rationale, approvals, changes and execution results should remain linked so that the history of the case can later be reconstructed.

## Test Design

The repository includes thirteen proposed test scenarios covering normal processing, control failures, exception handling and traceability gaps identified during requirements reconciliation.

The scenarios include cases relating to:

* successful approval and execution
* missing evidence
* policy exceptions
* segregation of duties
* stale approval after a material change
* duplicate authorisation
* decision-version mismatch
* execution failure

The workbook records expected outcomes but does not contain executed test evidence.

All scenarios are therefore intentionally marked **Not Run**.

## Technical Scope

The technical component of this case study consists of conceptual system analysis, data-flow modelling, control logic and test design.

The repository does not claim an implemented integration, database solution, API, runnable application or executed testing.

The purpose of the project is to demonstrate how a Technical Business Analyst can translate an operational control problem into clearer process behaviour, system boundaries, exception handling and testable requirements.

## Traceability 

The repository now includes documented functional requirements, business rules, exception rules and non-functional requirements referenced by the proposed test scenarios.

A traceability matrix links requirements and rules to Jira user stories, acceptance criteria and proposed test scenarios.

The reconciliation identified several direct-test coverage gaps, which were addressed by adding scenarios for decision rationale, approval outcomes and controlled decision-version creation.

Traceability currently demonstrates design coverage only. The test scenarios have not been executed, so the matrix does not represent verified implementation behaviour.

## Project Status

### Completed

* current-state process model
* proposed future-state process
* system-context analysis
* conceptual data-flow analysis
* decision and exception modelling
* portfolio documentation and repository structure
* requirements register
* business-rules register
* exception-rules register
* non-functional requirements register
* requirements-to-test traceability matrix
* thirteen proposed functional and control test scenarios

### Outstanding

* execution of the proposed test scenarios

## Potential future extensions

* data dictionary, where it adds analytical value
* interface contract, where it adds analytical value
* additional test execution evidence if an appropriate implementation becomes available

## Tools

The project deliverables were created using:

- Confluence for business analysis documentation, requirements, rules, NFRs and traceability documentation
- Jira for prioritised user stories, acceptance criteria and delivery-item tracking
- diagrams.net / draw.io for process, system-context, data-flow and decision/exception modelling
- Microsoft Excel for test design, requirements registers, rules, open issues and traceability

No SQL analysis, Postman testing, live-system testing, production implementation or client work is claimed within this repository.

## Repository Structure

```text
mortgage-forbearance-control-analysis/
│
├── README.md
│
├── .gitignore
├── .gitattributes
│
├── analysis/
│   ├── TL-E01-business-problem-and-scope.pdf
│   ├── TL-E02-requirements-rules-and-nfr-catalogue.pdf
│   └── TL-E03-prioritised-user-stories-and-acceptance-criteria.pdf
│
├── jira/
│   └── jira-mortgage-forbearance-user-stories.xlsx
│
├── diagrams/
│   ├── current-state-mortgage-forbearance.png
│   ├── current-state-mortgage-forbearance.drawio
│   ├── future-state-mortgage-forbearance.png
│   ├── future-state-mortgage-forbearance.drawio
│   ├── system-context.drawio
│   ├── data-flow.drawio
│   └── decision-and-exception-flow.drawio
│
└── testing/
    └── mortgage-forbearance-test-scenarios.xlsx
```

## Disclaimer

This is a self-directed portfolio case study using a synthetic scenario and synthetic data. It is intended to demonstrate Technical Business Analyst analysis and documentation skills and should not be interpreted as a production implementation, a description of a specific lender's operating model, or evidence of client work.
