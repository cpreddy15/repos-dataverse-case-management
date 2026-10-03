# Data Model — Column Design

Publisher prefix: `cm_`

## Case (`cm_case`) — Ownership: User/Team
| Display name | Schema name | Type | Notes |
|---|---|---|---|
| Case Number | cm_casenumber | Autonumber | `CASE-{SEQNUM:5}`, primary name |
| Title | cm_title | Text (200) | Required |
| Description | cm_description | Multiline text | |
| Requester | cm_requester | Lookup → Contact | Required |
| Category | cm_category | Lookup → Case Category | Required |
| Priority | cm_priority | Choice | Low / Medium / High / Critical |
| Status | cm_status | Choice | New / In Progress / On Hold / Resolved / Closed |
| Assignment Group | cm_assignmentgroup | Lookup → Assignment Group | |
| Due Date | cm_duedate | Date and time | Set from SLA policy |
| Resolution Code | cm_resolutioncode | Lookup → Resolution Code | Required when Resolved |
| Resolved On | cm_resolvedon | Date and time | |

## Case Category (`cm_casecategory`) — Ownership: Organization
| Display name | Schema name | Type |
|---|---|---|
| Name | cm_name | Text |
| SLA Policy | cm_slapolicy | Lookup → SLA Policy |
| Default Group | cm_defaultgroup | Lookup → Assignment Group |

## SLA Policy (`cm_slapolicy`) — Ownership: Organization
| Display name | Schema name | Type |
|---|---|---|
| Name | cm_name | Text |
| Response Hours | cm_responsehours | Whole number |
| Resolution Hours | cm_resolutionhours | Whole number |

## Case Comment (`cm_casecomment`)
| Display name | Schema name | Type |
|---|---|---|
| Case | cm_case | Lookup → Case (Parental, cascade delete) |
| Comment | cm_comment | Multiline text |
| Internal Only | cm_internalonly | Yes/No |

## Case Task (`cm_casetask`)
| Display name | Schema name | Type |
|---|---|---|
| Case | cm_case | Lookup → Case (Parental) |
| Task Name | cm_name | Text |
| Assigned To | ownerid | Owner |
| Task Status | cm_taskstatus | Choice |

## Escalation (`cm_escalation`)
| Display name | Schema name | Type |
|---|---|---|
| Case | cm_case | Lookup → Case (Parental) |
| Level | cm_level | Choice (L1, L2, L3) |
| Reason | cm_reason | Multiline text |

## Assignment Group, Group Member, Department, Resolution Code
Reference tables with Organization ownership. Group Member links a `systemuser` to an Assignment Group (many-to-many modeled as an intersect table so membership can carry extra data like *Lead* flag).

## Relationship behaviors
- Case → Comment / Task / Escalation: **Parental** (delete and assign cascade)
- Category → Case: **Referential, Restrict Delete** (can't delete a category in use)
