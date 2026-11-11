# People and HR

The common HR vocabulary -- employees and their employment, the departments, teams and positions they sit in, the places they work, and the time off they take -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Human Resources, HRIS, HR Tech, HR, HCM, Human Capital Management, Workforce Management, People Operations in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| employee | 61 | 55 | id 86%, work_email 76%, last_name 71%, first_name 67%, status 58% | employees 44, people 9, workers 8, employee 8 |
| department | 21 | 13 | id 77%, name 77% | departments 17, department 3, cost-centers 2, cost_centers 2 |
| team | 7 | 5 | id 80%, name 60% | teams 7 |
| position | 14 | 11 | id 100%, name 73% | positions 12, job-titles 1, job_titles 1, jobtitles 1 |
| work_location | 27 | 20 | id 80%, name 75%, status 50% | locations 16, location 5, branches 4, offices 3 |
| absence | 19 | 17 | id 88%, employee_id 71%, end_at 65%, status 65%, type 65%, start_at 59% | absences 9, leave_requests 3, leave 3, leaves 2 |
| employment | 19 | 14 | id 86%, status 64%, employment_type 57%, effective_date 50%, employee_id 50%, job_title 50% | jobs 14, employments 4, contracts 4, employment 1 |

Cohort: 171 providers with harvested OpenAPI, 61 crosswalks. Of the providers exposing a employee: 67% create, 95% list, 87% fetch, 57% update, 25% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An employee is agreed: id, work email, first and last name and status are core across 55 providers with a readable schema -- the sharpest core of any people concept so far.
- Absences agree too: start, end, status, type and the employee are all core, so a time-off request maps cleanly between HR systems.
- Teams barely exist as a resource of their own (7 providers); most HR systems model the organisation through departments and managers instead.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Employee Benefits is not a cohort tag: benefits administration is its own domain.
- `roles` is not a position and `groups` is not a team: reviewed, both were permission roles and SCIM, LMS or payment groups far more often than an org structure.
- `members` is not an employee segment (workspace members, analytics dimensions).
- Time off is `/absences`: absences lead (9) the spread of time-off spellings, and `/holidays` -- a public-holiday calendar -- is not a request and is not counted.
- Employment is `/employments`, though 14 providers say `jobs`: `jobs` is a job posting in the recruiting context. Role name over a colliding word, as with `/cardholders`.
- A work location is `/work-locations` for the same reason: `/locations` means a store or a restaurant in commerce and point of sale.
- Five Workday listings, two ADP, two HiBob and two Ethena listings are merged as duplicates.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
