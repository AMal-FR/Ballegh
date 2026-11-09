# Balagh (Report It)

> A mobile app that lets citizens report any emergency or public-service problem with a photo and an automatic GPS location. The system routes the report to the responsible agency, calculates its priority, merges duplicates, and follows up with the citizen until the problem is actually solved. It also evaluates reporter credibility and the quality of the agency's response.

## Problem Statement
- Citizens don't know whom to report to, and after reporting they never find out what happened.
- Agencies are flooded with duplicate, unordered reports.
- There is no way to tell a genuine report from a false one.
- There is no measurement of solution quality from the citizen's point of view.

## Actors
| Actor | Role |
|---|---|
| Citizen | Reports problems, tracks them, and rates the result |
| Official | Receives and handles reports, updates their status, monitors agency performance, and manages agencies, categories, users, and system settings |

## Key Features
1. Report creation with a photo and automatic GPS location, with automatic routing to the responsible agency
2. Report status tracking with push notifications
3. Quick emergency report (SOS)
4. Offline mode
5. Duplicate report merging
6. Smart priority calculation
7. Service rating
8. User trust score

## Repository Contents
| File | Description |
|---|---|
| `Team.md` | Team members and roles |
| `Requirements.md` | Business, User, System, and Domain requirements |
| `User_Stories.md` | User stories with acceptance criteria |
| `Diagrams.md` | Use case diagram and class diagram |

## Git Workflow (mandatory for all team members)
**Never push directly to `main`.** All new work goes on a new branch, then a Pull Request, then a merge into `main`.

```bash
git checkout main
git pull origin main
git checkout -b feature/<your-name>-<task>     # e.g. feature/ahmed-user-stories
# ... do your work ...
git add .
git commit -m "docs: add user stories for SOS"
git push -u origin feature/<your-name>-<task>
```
Then open a Pull Request on GitHub, have another team member review it, and merge it into `main`.

**Branch naming:** `feature/...` for additions, `fix/...` for corrections, `docs/...` for documents.
**Commit messages:** prefix with `docs:`, `feat:`, or `fix:` followed by a short description.
**Rule:** every member must have commits and at least one Pull Request under their own name.
