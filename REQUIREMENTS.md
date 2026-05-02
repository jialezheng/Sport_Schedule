# Requirements — Biola Sport Court Scheduling

This document captures the functional and non-functional requirements that
shaped the product backlog and the requirements traceability matrix (RTM).

CSCI 450 — Software Engineering, Spring 2026.

---

## 1. Stakeholders & users

- **Biola students** — the primary users; want to find an open court, see who's
  already playing, and join or post pickup games.
- **Biola faculty / staff** — secondary users; want to see official 25Live
  events on the same calendar so they don't double-book a court.
- **Recreation department / facility owners** — want their facilities listed,
  with accurate hours and current bookings.
- **Course staff (CSCI 450)** — final-submission audience; want to download from
  GitHub, install dependencies, and run the project end-to-end.

## 2. Functional requirements

Each requirement maps to an item in the Requirements Traceability Matrix (RTM).

| ID    | Requirement                                                                                  |
| ----- | -------------------------------------------------------------------------------------------- |
| R-01  | The user can browse all sports facilities, search by name, and filter by sport.              |
| R-02  | The user can view a facility's detail page, including hours, sports supported, and location. |
| R-03  | The user sees a per-day availability timeline marking open, occupied, selected, and closed cells in 30-minute increments. |
| R-04  | The user can post a pickup game by selecting a facility, sport, date, start/end time, and capacity. |
| R-05  | The user can join a pickup game with available capacity, and can later cancel their slot.    |
| R-06  | The user can chat inside a pickup game session with other participants.                      |
| R-07  | The user can view a calendar that merges 25Live campus events with user-posted pickup games, filterable by event type. |
| R-08  | The user has a profile page showing their name and avatar.                                   |
| R-09  | A user who created a pickup game is visually marked as the host on each card.                |
| R-10  | The system imports campus events from 25Live on a recurring schedule.                        |
| R-11  | The user can see their upcoming and past reservations on a "My Reservations" page.           |

## 3. Non-functional requirements

| ID     | Category        | Requirement                                                                            |
| ------ | --------------- | -------------------------------------------------------------------------------------- |
| NFR-01 | Performance     | Initial page load < 3 s on a typical campus Wi-Fi connection.                          |
| NFR-02 | Performance     | API endpoints return in < 500 ms under normal load (up to 50 concurrent users).        |
| NFR-03 | Availability    | Frontend served from Netlify CDN; API runs as serverless functions with auto-scaling.  |
| NFR-04 | Reliability     | 25Live sync failures must not break the user-facing app; cached data continues to serve. |
| NFR-05 | Security        | No secrets committed to the repo; all credentials provided via environment variables.  |
| NFR-06 | Privacy         | The app does not collect personal information beyond a display name and avatar.        |
| NFR-07 | Accessibility   | UI meets WCAG AA contrast on key interactive elements; all controls keyboard reachable. |
| NFR-08 | Usability       | Posting a pickup game completes in 5 or fewer clicks from the dashboard.               |
| NFR-09 | Compatibility   | Latest versions of Chrome, Safari, Firefox, and Edge on desktop and mobile.            |
| NFR-10 | Maintainability | TypeScript strict mode + ESLint enforced; ≥ 80% of utilities covered by Vitest tests.  |
| NFR-11 | Deployability   | A clean clone of the repo + `npm install` + `npm run dev` runs locally with no manual code changes. |
| NFR-12 | Documentation   | A `README.md`, `DEPLOY.md`, and `REQUIREMENTS.md` ship with the source.                |

## 4. External constraints

- **Database:** Postgres-compatible (Neon free tier in production, local
  Postgres for dev). The seed script and schema target Postgres syntax.
- **Calendar source:** Biola 25Live. Authentication is required and credentials
  must be provided at deploy time.
- **Hosting:** Netlify (static + serverless functions + scheduled functions).
  Netlify cron expressions in `netlify.toml` drive the 25Live sync.
- **Browsers:** Modern evergreen browsers; no IE 11 support.

## 5. Out of scope (v1.0)

The following items were considered but deferred to a future release:

- Native iOS / Android applications.
- Online payment for paid facility bookings.
- SSO with Biola single sign-on (currently a name-based identity).
- Push notifications for game reminders.
- Admin dashboard for recreation staff.
- Multi-campus support beyond Biola + La Mirada parks.

## 6. Assumptions

- Users have a modern web browser and an internet connection.
- 25Live credentials remain valid for the lifetime of the deployment.
- The 5 seed facilities (Chase Gymnasium, Al Barbour Field, Hope Outdoor
  Basketball Court, Neff Park, Gardenhill Park) are the canonical set; new
  facilities are added via `db:reset` + `db:seed`, not the UI.

---

Biola University · CSCI 450 · Spring 2026
