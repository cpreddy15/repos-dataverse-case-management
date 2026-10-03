# Security Model

## Principles
- **Least privilege**: agents only edit what they own; managers see their business unit.
- **Teams over users**: assignment groups are backed by Dataverse owner teams, so cases can be owned by a team queue.
- **Reference data locked down**: only Case Admin can change categories, SLAs and resolution codes.

## Roles
| Role | Who | Summary |
|---|---|---|
| Case Agent | Support staff | Create/edit own cases, read BU cases, add comments/tasks |
| Case Manager | Team leads | Full access within BU, reassign cases, view dashboards |
| Case Admin | App owners | Organization-wide access, manage reference tables |
| Auditor | Compliance | Read-only organization-wide |

## Column security
`cm_internalonly` comments are hidden from requesters via a column security profile assigned only to agent/manager roles.
