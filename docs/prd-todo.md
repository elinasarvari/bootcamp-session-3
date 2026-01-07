# Product Requirements Document (PRD) - TODO App Enhancement

## 1. Overview

We are upgrading the basic TODO app to support due dates, priorities, and filters so users can better organize and manage their tasks. The current app only supports a title and completed status. This enhancement will make the app more practical and useful without adding excessive complexity. The focus is on creating a simple, teachable MVP with no backend changes required.

---

## 2. MVP Scope

- Add `dueDate` field (optional, ISO format YYYY-MM-DD)
  - Invalid date values should be ignored and treated as absent
- Add `priority` field with three levels: P1, P2, P3
  - Default priority should be P3
  - Values must be one of: "P1" | "P2" | "P3"
- Implement filter tabs: **All**, **Today**, **Overdue**
  - "All" view: shows all tasks including completed
  - "Today" view: shows incomplete tasks due today
  - "Overdue" view: shows incomplete tasks past their due date
- Maintain local storage only (no backend or external storage changes)
- Data model requirements:
  - `title`: required (existing field)
  - `priority`: "P1" | "P2" | "P3", default "P3" (new field)
  - `dueDate`: optional YYYY-MM-DD string (new field)
  - `completed`: boolean (existing field)

---

## 3. Post-MVP Scope

- Visual highlighting for overdue tasks (e.g., red highlighting to make them stand out)
- Color-coded priority badges:
  - P1: Red badge
  - P2: Orange badge
  - P3: Gray badge
- Advanced sorting logic:
  - Overdue tasks first
  - Then by priority (P1 → P2 → P3)
  - Then by due date (ascending, soonest first)
  - Tasks without due dates appear last

---

## 4. Out of Scope

- Notifications (push, email, or in-app)
- Recurring tasks
- Multi-user support or collaboration features
- Keyboard navigation and special accessibility features
- External storage or backend integration (staying local only)
- Task descriptions or additional metadata beyond title, priority, and due date
