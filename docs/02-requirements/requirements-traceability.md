# Traceability matrix

This is the master index; detailed IDs are defined in the catalogs. Acceptance criteria (CA) are in `09-acceptance-criteria/acceptance-criteria.md`; stories are in `04-user-stories/stories.md`.

| RF | Related RN | Story | CA | Process |
|---|---|---|---|---|
| RF-001..002 | RN-001..005 | US-001..002 | CA-001..002 | PR-001 |
| RF-003 | RN-006..010 | US-002 | CA-003 | PR-002 |
| RF-004 | RN-011..014 | US-003 | CA-004 | PR-002 |
| RF-005 | RN-015..022 | US-004 | CA-005 | PR-003 |
| RF-006 | RN-023..027 | US-005 | CA-006 | PR-004 |
| RF-007 | RN-028..031 | US-006 | CA-007 | PR-005 |
| RF-008..009 | RN-032..044 | US-007..008 | CA-008..009 | PR-006 |
| RF-010 | RN-045..054 | US-009 | CA-010 | PR-007 |
| RF-011 | RN-055..062 | US-010 | CA-011 | PR-008/PR-014 |
| RF-012 | RN-063 | US-011 | CA-012 | PR-009 |
| RF-013 | RN-064..070 | US-012 | CA-013 | PR-005 |
| RF-014 | RN-071..076 | US-013 | CA-014 | PR-010/PR-011 |
| RF-015..016 | RN-077..082 | US-014 | CA-015..016 | PR-012..013 |
| RF-017 | RN-083..087 | US-015 | CA-017 | PR-015 |
| RF-018..019 | RN-088..096 | US-016 | CA-018..019 | cross-functional |
| RF-020..021 | RN-097..102 | US-017 | CA-020..021 | cross-functional |

## Non-functional traceability

RNF-001..004 relate to RF-001/019/020 and RN-004/092..096; RNF-005..007/011..012/015..016 relate to RF-008..010/017..020 and RN-032..054/083..101; RNF-008..010/013/017..020 are cross-functional attributes verified through operations, continuity, regression, privacy, and documentation evidence.

## Coverage control

An RF without a story/CA is not ready for development. A rule without a process or requirement must be justified as a domain invariant. A criterion without an RF/story is orphaned. In this revision every listed RF has at least one set of RN/US/CA. Regulatory references are mapped in `07-compliance/regulatory-requirements.md`. IDs are never reassigned when scope is removed.
