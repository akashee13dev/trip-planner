# Product Requirements Document (PRD)

## Project: Trip Planner

**Version:** 0.1 — Initial Product Requirements\
**Status:** Draft\
**Product direction:** Effortless Group Travel\
**Platform:** Responsive Web Application (Mobile-ready API architecture)

**Product statement:** Plan together. Travel effortlessly. Remember forever.

---

# 1. Product Overview

## 1.1 Vision

Build a universal travel-planning platform that makes organizing, coordinating, experiencing, and remembering trips effortless.

The product should solve the difficulties of group travel without overwhelming users with unnecessary features.

It should provide one centralized place to manage:

- Trip planning and collaboration.
- Places and day-wise itineraries.
- Maps and travel schedules.
- Group expenses and settlements.
- Reservations and booking information.
- Trip progress and coordination.
- Memories and travel journals.

## 1.2 Target Audience

The product targets everyone who travels:

| User type       | Primary need                                            |
| --------------- | ------------------------------------------------------- |
| Solo travellers | Organize trips and maintain travel records              |
| Couples         | Plan and coordinate trips together                      |
| Families        | Manage schedules, places, and reservations              |
| Friends         | Collaborate on plans and manage expenses                |
| Groups          | Coordinate decisions, itineraries, and responsibilities |

The initial product architecture should support all these user types without creating separate products for each.

## 1.3 Core Problem

Group travel planning is fragmented across multiple applications.

People typically use:

- WhatsApp for discussions.
- Google Maps for locations.
- Google Sheets for budgets.
- Notes for itineraries.
- Email for reservations.
- Separate applications for expense splitting.
- Photo galleries for memories.

This creates several problems:

1. Information is scattered.
2. Group decisions are difficult.
3. Nobody wants to take responsibility for planning.
4. Itinerary changes create confusion.
5. Expenses and settlements become complicated.
6. Travel memories are disconnected from the actual journey.

**Our solution:** A single collaborative workspace for the entire travel lifecycle.

---

# 2. Product Goals

## 2.1 Primary Goals

1. Make trip creation simple.
2. Make group collaboration effortless.
3. Provide a structured itinerary and map experience.
4. Simplify group expense management and settlements.
5. Help travellers coordinate during the journey.
6. Preserve trip memories through a structured journal.
7. Encourage users to return and create more trips.

## 2.2 Product Principles

- Simplicity over unnecessary complexity.
- Collaboration should be effortless.
- Users remain in control of their plans.
- Changes should not destroy historical information.
- Every module should have clear responsibilities.
- Backend business logic should be reusable across web and future mobile applications.
- Build complete, usable features rather than many incomplete features.

---

# 3. Scope and Product Lifecycle

The product supports four stages.

| Stage     | Description                                             | Priority  |
| --------- | ------------------------------------------------------- | --------- |
| Discovery | Discover destinations and experiences                   | Future    |
| Planning  | Create trips, collaborate, organize places and expenses | Must-have |
| Travel    | Follow itineraries, manage changes, track progress      | Must-have |
| Memories  | Maintain a journal and revisit completed journeys       | Important |

## 3.1 MVP Scope

The MVP focuses on:

- User registration and authentication.
- Trip creation and management.
- Email-based invitations.
- Role-based collaboration.
- Group suggestions and polls.
- Places and bucket lists.
- Day-wise itinerary.
- Map visualization.
- Manual visit tracking.
- Expense splitting and settlements.
- Reservation management.
- Trip journal.
- Activity feed and notifications.

## 3.2 Future Scope

The following should not delay the MVP:

- Hotel discovery and booking marketplace.
- Destination discovery.
- Automated place discovery.
- Gmail and external application integrations.
- Automatic reservation imports.
- GPS-based automatic visit detection.
- Continuous live location tracking.
- AI-powered itinerary generation.
- Automatic traffic-based itinerary optimization.
- Public travel community and social feed.
- Dedicated Android and iOS applications.

---

# 4. User Accounts and Profiles

## 4.1 Registration

Users should be able to register using:

- Name.
- Email address.
- Password.

Authentication and account recovery must be supported.

## 4.2 Profile

Users can update their profiles after registration.

Profile fields:

- Display name.
- Profile picture.
- Email.
- Phone number (optional).
- Other personal details (optional).

Avoid collecting unnecessary personal information.

## 4.3 Account Requirements

- A user can create multiple trips.
- A user can participate in multiple trips.
- A user can have different roles in different trips.
- Profile changes should not affect historical trip contributions.

---

# 5. Trip Management

## 5.1 Trip Creation

Trip creation should be quick.

Required information:

- Trip name.
- Destination.

Optional information:

- Start date.
- End date.
- Description.
- Cover image.
- Currency.

Users should be able to create a trip without providing every detail upfront.

## 5.2 Trip Lifecycle

Proposed statuses:

| Status    | Meaning                      |
| --------- | ---------------------------- |
| Draft     | Initial trip created         |
| Planning  | Trip is being organized      |
| Upcoming  | Travel dates are approaching |
| Ongoing   | Trip is currently happening  |
| Completed | Trip has finished            |

Statuses should be derived from dates and trip progress wherever practical.

Users should not need to manually update statuses unnecessarily.

## 5.3 Trip Navigation

Each trip should provide access to:

1. Overview.
2. Itinerary.
3. Places.
4. Map.
5. Expenses.
6. Reservations.
7. Journal.
8. Members.
9. Settings.

These are sections within a trip, not separate dashboard products.

## 5.4 Trip Overview

The overview should provide a compact summary containing:

- Destination and dates.
- Number of members.
- Interactive map preview.
- Day-wise itinerary preview.
- Upcoming reservations.
- Expense summary.
- Recent member activities.
- Current trip progress.
- Next planned activity.

The overview must remain clean and avoid overwhelming users with too much information.

---

# 6. Collaboration and Permissions

## 6.1 Permission Model

Permissions are assigned per trip.

A user can be an Editor in one trip and a Viewer in another.

Proposed roles:

| Role   | Permissions                                         |
| ------ | --------------------------------------------------- |
| Owner  | Full control, ownership transfer, deletion          |
| Admin  | Manage members and trip configuration               |
| Editor | Manage itinerary, places, expenses and reservations |
| Viewer | Read-only access                                    |

The Owner remains responsible for the trip.

## 6.2 Invitations

MVP supports email invitations.

Invitation workflow:

1. Owner or authorized Admin enters an email address.
2. Selects the member's role.
3. System sends an invitation.
4. Recipient signs in or creates an account.
5. Recipient accepts the invitation.
6. Recipient joins the trip.

Invitation states:

- Pending.
- Accepted.
- Expired.
- Cancelled.

Additional requirements:

- Prevent duplicate active invitations.
- Allow invitation cancellation.
- Allow role changes.
- Allow member removal.
- Reject unauthorized access.

## 6.3 Joining a Trip

After accepting an invitation, users should see a compact introduction:

- Trip name.
- Destination.
- Dates.
- Members.
- Assigned role.

Users can then explore the trip overview.

No lengthy onboarding process is required.

## 6.4 Group Decision-Making

Members should be able to:

- Suggest destinations and places.
- Create polls.
- Vote on suggestions.
- Discuss suggestions.
- Add comments.
- React using emojis.
- View poll results.

An approved suggestion should not automatically modify the itinerary.

An authorized member must explicitly add it to the itinerary.

Poll configuration and voting rules will be finalized during detailed design.

## 6.5 Member Removal and Leaving

When a member leaves or is removed:

- Access is revoked.
- Historical contributions remain.
- Expenses remain recorded.
- Comments and suggestions remain.
- Journal entries remain.
- Photos and attachments remain.
- The member is identified as a former member.

Leaving a trip does not automatically settle financial obligations.

## 6.6 Ownership Transfer

The current Owner can initiate ownership transfer to an existing member.

Requirements:

- Recipient must accept.
- Previous Owner receives an appropriate role.
- Historical records remain unchanged.
- Transfer is recorded in the activity history.

---

# 7. Places and Itinerary Management

## 7.1 Places

Users can manually add places.

Place information:

| Field                | Requirement |
| -------------------- | ----------- |
| Place name           | Required    |
| Address              | Optional    |
| Latitude / Longitude | Optional    |
| Category             | Required    |
| Description          | Optional    |
| Cover image          | Optional    |
| Estimated duration   | Optional    |
| Notes                | Optional    |

Supported categories:

- Tourist attraction.
- Restaurant.
- Hotel.
- Shopping.
- Nature.
- Adventure.
- Other.

Places can be added to the bucket list or directly to an itinerary.

## 7.2 Bucket List

A bucket list contains places the group wants to visit but has not scheduled.

Users should be able to:

- Add places.
- Edit places.
- Remove places.
- Discuss places.
- Vote on suggestions.
- Schedule a place.
- Move scheduled places back to the bucket list.

Avoid duplicate places within the same trip where possible.

## 7.3 Day-wise Itinerary

The itinerary organizes scheduled places by travel date.

Each activity can contain:

- Place.
- Date.
- Planned start time.
- Planned end time.
- Estimated visit duration.
- Travel duration.
- Notes.
- Attachments.

Supported operations:

- Schedule a place.
- Move it to another day.
- Change its time.
- Reorder activities.
- Remove it from the itinerary.
- Mark it as visited.
- Mark it as skipped.

Removing an activity from an itinerary must not delete the underlying place.

## 7.4 Dynamic Schedule

The system should help users understand delays and their impact on upcoming activities.

For each upcoming activity, display:

- Original planned time.
- Expected time.
- Delay, if any.

Example:

| Activity | Planned  | Expected |
| -------- | -------- | -------- |
| Museum   | 10:00 AM | 10:30 AM |
| Lunch    | 12:00 PM | 12:30 PM |
| Beach    | 3:00 PM  | 3:30 PM  |

The expected time should be recalculated based on actual progress and estimated travel durations.

The original schedule must remain unchanged unless an authorized user explicitly edits it.

The system can suggest:

- Rearranging activities.
- Skipping an activity.
- Moving an activity to another day.

The system must never silently change the itinerary.

Live traffic integrations can be introduced later.

---

# 8. Visit Tracking

Visit tracking should remain manual in the MVP.

Proposed activity states:

| State       | Description                  |
| ----------- | ---------------------------- |
| Upcoming    | Activity is planned          |
| In Progress | Member has started the visit |
| Visited     | Member completed the visit   |
| Skipped     | Activity was skipped         |

Members can:

- Start a visit.
- Complete a visit.
- Record actual arrival and departure times.
- Add photos.
- Add notes.
- Add expenses.
- Comment and react.
- Move activities to another day.

GPS-based automatic arrival detection is outside the MVP.

---

# 9. Map Experience

The map should be itinerary-first.

## 9.1 Core Requirements

- Display planned destinations.
- Display locations in itinerary order.
- Connect destinations using routes.
- Support day-wise map selection.
- Highlight the selected day.
- Show place details when selected.
- Display distance and estimated travel duration when available.
- Allow users to switch between travel days.

## 9.2 Visual Experience

The map should be clean and intuitive.

Where practical:

- Animate route drawing.
- Highlight the selected route.
- Provide smooth transitions between days.
- Show the selected destination clearly.

## 9.3 Member Location Sharing

Members should be able to manually share their current location.

The map can display:

- Member avatar.
- Display name.
- Last shared location.
- Last updated time.

Location sharing must be opt-in.

MVP should avoid continuous background tracking. Location history and automatic live tracking are future capabilities.

---

# 10. Expense Management

## 10.1 Product Direction

Expense management should function as an independent expense-splitting module inside the main application.

It should be designed with clean module boundaries so it can potentially become a separate microservice later.

Do not introduce microservice infrastructure in the MVP.

## 10.2 Expense Creation

An expense should support:

- Expense title.
- Amount.
- Currency.
- Category.
- Date.
- Paid by.
- Participants.
- Split method.
- Description.
- Receipt attachment.

## 10.3 Split Methods

MVP supports:

1. Equal split.
2. Custom amount split.
3. Selected-member split.

Multiple members should be able to pay expenses.

## 10.4 Balances

The system should calculate:

- Total trip expenditure.
- Individual contributions.
- Individual share.
- Amount owed.
- Amount receivable.
- Member-wise balances.

All financial calculations must happen on the backend.

## 10.5 Settlement

The application should simplify settlements by calculating who owes whom.

Example:

| Member   | Amount          |
| -------- | --------------- |
| Akash    | Receives ₹1,000 |
| Member B | Owes ₹600       |
| Member C | Owes ₹400       |

Users can record settlements manually.

The system should maintain settlement history.

## 10.6 Expense History

Users should be able to:

- View all expenses.
- Filter by member.
- Filter by category.
- Edit permitted expenses.
- View changes.
- Export expense information.

Historical financial changes should be auditable.

---

# 11. Reservation Management

The MVP supports reservation management, not booking discovery or transactions.

Users manually add reservations.

Supported types:

- Hotels and accommodation.
- Flights.
- Trains.
- Buses.
- Activities.
- Restaurants.
- Other bookings.

Reservation information:

| Field                     | Requirement             |
| ------------------------- | ----------------------- |
| Reservation name          | Required                |
| Type                      | Required                |
| Date and time             | Optional, based on type |
| Confirmation number       | Optional                |
| Amount                    | Optional                |
| Booking website/reference | Optional                |
| Attachments               | Optional                |
| Notes                     | Optional                |
| Status                    | Required                |

Reservations can be associated with:

- A trip.
- An itinerary activity, optionally.

Users should be able to view upcoming reservations from the trip overview.

---

# 12. Trip Journal

## 12.1 Purpose

The journal should preserve the actual journey, not just the planned itinerary.

It should reuse existing trip information to minimize duplicate data entry.

## 12.2 Journal Features

Users can maintain day-wise memories containing:

- Visited places.
- Photos.
- Videos or attachments where supported.
- Notes.
- Personal memories.
- Dates.
- Locations.
- Member contributions.

## 12.3 Journey View

The completed trip should provide a structured journey view:

- Day-wise timeline.
- Places visited.
- Photos and memories.
- Travel dates.
- Map visualization.
- Member contributions.

The journal should allow users to revisit the entire trip as a chronological experience.

AI-generated travel stories and automatic social sharing are future features.

---

# 13. Notifications and Activity Feed

## 13.1 Activity Feed

The activity feed records important trip events.

Examples:

- Member joined.
- Place added.
- Place moved to another day.
- Poll created.
- Poll completed.
- Expense added.
- Reservation updated.
- Visit completed.
- Journal entry added.
- Ownership transferred.

## 13.2 Notifications

Users should receive configurable notifications for important events.

Priority events:

- Trip invitations.
- Invitation acceptance.
- Member joining or leaving.
- Polls and voting.
- Comments and mentions.
- Important itinerary updates.
- Expense updates.

Users should be able to control notification preferences.

Avoid sending unnecessary notifications for every minor action.

---

# 14. Completed Trip Management

Completed trips should remain accessible.

Users should be able to:

- View historical itinerary.
- View visited places.
- View routes.
- View reservations.
- Review expenses.
- View settlement history.
- Add or edit journal entries.
- Add photos and memories.

Historical visit times should not be casually modified.

Financial corrections should maintain change history.

Trip deletion remains Owner-controlled.

---

# 15. Trip Visibility and Access

The product should distinguish between visibility and permissions.

Visibility describes who can discover or view a trip.

Permissions describe what an authorized user can do.

Initial direction:

| Visibility | Behaviour                                           |
| ---------- | --------------------------------------------------- |
| Private    | Owner and invited members                           |
| Friends    | Friends can view, subject to configured permissions |
| Public     | Discoverable by other users                         |

For the MVP:

- Prioritize private trips and invited-member access.
- Do not build a public community feed.
- Do not expose private expenses, reservations, or personal information through public visibility.

The exact Friends relationship model needs to be finalized before implementation.

---

# 16. Non-Functional Requirements

## 16.1 Architecture

The product should use an API-first architecture.

Initial architecture direction:

**Responsive Web Application + Versioned Backend APIs + Modular Monolith**

Do not introduce microservices prematurely.

## 16.2 API Design

- Use versioned endpoints such as `/api/v1/`.
- Maintain consistent request and response structures.
- Provide standardized error responses.
- Validate all inputs on the backend.
- Maintain OpenAPI/Swagger documentation.
- Enforce authorization at the API level.
- Keep business logic out of the frontend.

## 16.3 Security

- Secure authentication.
- Role-based authorization.
- Trip-level access control.
- Secure invitation handling.
- Input validation.
- Protection against unauthorized resource access.
- Secure attachment access.
- Privacy-controlled location sharing.
- Audit history for sensitive changes.

## 16.4 Data Integrity

- Database constraints.
- Transactional financial operations.
- Consistent expense calculations.
- Historical record preservation.
- Referential integrity.
- Appropriate deletion and archival policies.

## 16.5 Testing

Required testing levels:

- Unit tests.
- Integration tests.
- API tests.
- Authorization tests.
- Financial calculation tests.
- API contract tests.
- End-to-end tests.

## 16.6 Future Mobile Compatibility

The backend must not depend on web-specific business logic.

Future mobile applications should consume the same versioned APIs and business rules.

---

# 17. MVP Development Roadmap

Development should happen in complete, usable increments.

## Phase 1 — Trip Foundation and Collaboration

**Goal:** Users can create trips and collaborate.

Features:

- Registration and authentication.
- Profile management.
- Trip creation.
- Trip lifecycle.
- Trip overview.
- Member invitations.
- Role-based permissions.
- Member management.
- Activity feed foundation.

**Milestone:** A user can create a trip, invite friends, and collaborate with them.

## Phase 2 — Itinerary and Maps

**Goal:** Groups can organize and follow their journeys.

Features:

- Place management.
- Bucket list.
- Group suggestions.
- Polls and voting.
- Day-wise itinerary.
- Activity scheduling.
- Manual visit tracking.
- Map visualization.
- Dynamic expected-time calculation.
- Manual member location sharing.

**Milestone:** A group can organize its complete journey and follow the itinerary.

## Phase 3 — Expense Management

**Goal:** Groups can manage and settle shared expenses.

Features:

- Expense creation.
- Multiple payers.
- Equal and custom splits.
- Member balances.
- Settlement calculations.
- Settlement recording.
- Expense history.
- Export.

**Milestone:** A group can understand exactly who owes whom.

## Phase 4 — Trip Lifecycle and Journal

**Goal:** Preserve the journey beyond the travel dates.

Features:

- Reservation management.
- Trip journal.
- Day-wise memories.
- Photo and attachment management.
- Completed trip experience.
- Historical trip review.

**Milestone:** Users can revisit and preserve their completed journeys.

## Phase 5 — Integration and Release

**Goal:** Deliver a reliable end-to-end MVP.

Activities:

- Integrate all modules.
- Complete authorization testing.
- Validate expense calculations.
- Test concurrent collaboration.
- Test itinerary changes.
- Verify historical data integrity.
- Improve performance.
- Complete security testing.
- Fix usability issues.
- Prepare deployment and monitoring.

**Milestone:** A stable, usable MVP ready for real group travel.

---

# 18. Success Metrics

The product should measure the following outcomes.

| Metric                     | What it measures                         |
| -------------------------- | ---------------------------------------- |
| Trip creation rate         | Users successfully create trips          |
| Invitation acceptance rate | Invited members join trips               |
| Collaboration rate         | Members actively participate             |
| Itinerary completion rate  | Groups complete planned activities       |
| Expense settlement rate    | Groups successfully settle expenses      |
| Journal participation      | Users maintain trip memories             |
| Repeat trip creation       | Users return and create additional trips |

These metrics should be measured through meaningful user actions, not merely page views.

---

# 19. Important Product Rules

1. Creating a trip must not require completing every trip detail.
2. A user can have different permissions across different trips.
3. Poll results must not silently modify the itinerary.
4. Removing an itinerary activity must not delete the underlying place.
5. The original itinerary schedule must be preserved when calculating delays.
6. Automatic suggestions must not modify plans without confirmation.
7. Manual visit tracking is sufficient for the MVP.
8. Location sharing must be opt-in.
9. Removing a member must not delete historical contributions.
10. Leaving a trip must not erase financial obligations.
11. Ownership transfer requires recipient acceptance.
12. Financial calculations must be performed on the backend.
13. Completed trips must preserve historical information.
14. Journal entries should reuse existing trip data where possible.
15. All trip resources must enforce trip-level permissions.

---

# 20. Open Decisions Before Finalizing the PRD

The following require more detailed product decisions before implementation.

| Area               | Decision required                                              |
| ------------------ | -------------------------------------------------------------- |
| Friends visibility | How are friends established and managed?                       |
| Currency           | Is each trip limited to one currency in the MVP?               |
| Polls              | Single choice, multiple choice, or both?                       |
| Location sharing   | How long should the last shared location remain visible?       |
| Maps               | Which map and routing provider should be used?                 |
| Place coordinates  | Should address lookup be supported in the MVP?                 |
| Journal            | Can entries be edited by everyone or only their authors?       |
| Expenses           | How should rounding differences be handled?                    |
| Reservations       | Which statuses should be supported?                            |
| Notifications      | Which events should trigger email versus in-app notifications? |
| Trip tabs          | Should Closed mean Completed, Archived, or both?               |

These decisions should be resolved during PRD review and system design, without expanding the initial MVP unnecessarily.

---

# 21. Product Definition

**Product:** Trip Planner

**Positioning:** Effortless Group Travel

**Core value:** One place to plan, coordinate, experience, and remember trips together.

**Primary differentiator:** The best group travel experience through simple collaboration, structured planning, itinerary coordination, and expense management.

**Initial platform:** Responsive web application.

**Architecture direction:** API-first modular monolith with versioned APIs.

**Development philosophy:** Build a simple, reliable, complete solution first. Expand based on validated user needs.

**Long-term direction:** A universal travel platform supporting the complete journey from planning to memories.

---

*End of PRD v0.1 — Initial Discovery-Based Draft*\
*This document captures agreed product decisions. Open decisions remain explicitly marked for review rather than treated as finalized requirements.*
