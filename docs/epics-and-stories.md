# Epics and Stories - TODO App Enhancement

## MVP Epics and Stories

### Epic: Add Priority Field to Tasks

#### Story: Add priority field to task data model
**Acceptance Criteria:**
- Task object includes a `priority` field
- Priority field accepts only "P1", "P2", or "P3" as valid values
- Priority field defaults to "P3" when not specified
- Existing tasks without priority field are handled gracefully

#### Story: Add priority dropdown to task creation form
**Acceptance Criteria:**
- Task creation form displays a priority dropdown/selector
- Dropdown shows three options: P1, P2, P3
- Dropdown defaults to P3 when creating a new task
- Priority value is included when submitting the form

#### Story: Add priority dropdown to task edit form
**Acceptance Criteria:**
- Task edit form displays a priority dropdown/selector
- Dropdown shows three options: P1, P2, P3
- Dropdown pre-populates with the task's current priority value
- Updated priority value is saved when form is submitted

#### Story: Display priority value on task list items
**Acceptance Criteria:**
- Each task in the list displays its priority value (P1, P2, or P3)
- Priority is visible and easy to identify
- Display updates immediately when priority is changed

#### Story: Set default priority to P3 for new tasks
**Acceptance Criteria:**
- New tasks automatically have priority set to "P3"
- Default applies when priority is not explicitly provided
- Form UI reflects P3 as the default selection

#### Story: Persist priority to local storage
**Acceptance Criteria:**
- Priority value is saved to local storage when task is created
- Priority value is saved to local storage when task is updated
- Priority value is retrieved correctly from local storage on app load
- Local storage schema accommodates the new priority field

#### Story: Validate priority values (P1, P2, P3 only)
**Acceptance Criteria:**
- Only "P1", "P2", or "P3" are accepted as valid priority values
- Invalid priority values are rejected or ignored
- Invalid values default to "P3"
- Validation occurs before saving to local storage

### Epic: Add Due Date Field to Tasks

#### Story: Add dueDate field to task data model
**Acceptance Criteria:**
- Task object includes an optional `dueDate` field
- dueDate field stores date in ISO format (YYYY-MM-DD)
- dueDate can be null or undefined (optional field)
- Existing tasks without dueDate field are handled gracefully

#### Story: Add date picker to task creation form
**Acceptance Criteria:**
- Task creation form displays a date picker input
- Date picker allows users to select a due date
- Date picker is optional (users can leave it blank)
- Selected date is included when submitting the form

#### Story: Add date picker to task edit form
**Acceptance Criteria:**
- Task edit form displays a date picker input
- Date picker pre-populates with the task's current due date (if set)
- Users can clear/remove the due date
- Updated due date is saved when form is submitted

#### Story: Display due date on task list items
**Acceptance Criteria:**
- Each task in the list displays its due date (if set)
- Date is displayed in a readable format
- Tasks without a due date show no date or indicate "No due date"
- Display updates immediately when due date is changed

#### Story: Validate date format (YYYY-MM-DD)
**Acceptance Criteria:**
- Due dates are stored in ISO format YYYY-MM-DD
- Date input accepts valid dates only
- Date format validation occurs before saving

#### Story: Handle invalid date values by ignoring them
**Acceptance Criteria:**
- Invalid date values are ignored and treated as absent
- Tasks with invalid dates behave as if they have no due date
- Invalid dates do not cause errors or app crashes
- Validation provides clear feedback for invalid dates

#### Story: Persist due date to local storage
**Acceptance Criteria:**
- Due date value is saved to local storage when task is created
- Due date value is saved to local storage when task is updated
- Due date value is retrieved correctly from local storage on app load
- Null/undefined due dates are handled properly in storage

### Epic: Implement Task Filtering

#### Story: Add filter tabs UI (All, Today, Overdue)
**Acceptance Criteria:**
- Three filter tabs are displayed: All, Today, Overdue
- Tabs are clearly labeled and easy to identify
- Active tab is visually distinct from inactive tabs
- Clicking a tab switches to that filter view
- Filter state persists during the session

#### Story: Implement "All" filter to show all tasks
**Acceptance Criteria:**
- "All" filter displays all tasks regardless of status or due date
- Both completed and incomplete tasks are shown
- Tasks with and without due dates are shown
- "All" is the default filter on app load

#### Story: Implement "Today" filter to show incomplete tasks due today
**Acceptance Criteria:**
- "Today" filter displays only tasks due today
- Only incomplete tasks are shown
- Completed tasks due today are hidden
- Tasks without due dates are not shown
- "Today" is calculated based on current date

#### Story: Implement "Overdue" filter to show incomplete tasks past due date
**Acceptance Criteria:**
- "Overdue" filter displays only tasks past their due date
- Only incomplete tasks are shown
- Completed tasks that were overdue are hidden
- Tasks without due dates are not shown
- Overdue status is calculated based on current date

#### Story: Hide completed tasks in Today filter view
**Acceptance Criteria:**
- Completed tasks do not appear in "Today" filter
- Only incomplete tasks due today are displayed
- Marking a task as complete removes it from Today view
- Unmarking a completed task shows it in Today view (if due today)

#### Story: Hide completed tasks in Overdue filter view
**Acceptance Criteria:**
- Completed tasks do not appear in "Overdue" filter
- Only incomplete overdue tasks are displayed
- Marking a task as complete removes it from Overdue view
- Unmarking a completed task shows it in Overdue view (if overdue)

#### Story: Show completed tasks in All filter view
**Acceptance Criteria:**
- Completed tasks are visible in "All" filter
- Completed tasks are displayed alongside incomplete tasks
- Completed status is clearly indicated (e.g., strikethrough)

---

## Post-MVP Epics and Stories

### Epic: Add Visual Priority Indicators

#### Story: Add red badge for P1 priority tasks
**Acceptance Criteria:**
- P1 priority tasks display a red badge/indicator
- Red badge is clearly visible and distinguishable
- Badge appears consistently across all views

#### Story: Detect overdue tasks based on current date
**Acceptance Criteria:**
- System correctly identifies tasks past their due date
- Detection compares task due date with current date
- Tasks without due dates are not flagged as overdue
- Completed tasks are not flagged as overdue
- Overdue status updates automatically as dates change

#### Story: Apply red highlighting to overdue task rows
**Acceptance Criteria:**
- Overdue incomplete tasks are visually highlighted in red
- Highlighting makes overdue tasks stand out clearly
- Highlighting applies to the entire task row or background
- Highlighting is removed when task is completed or date is updated
- Red highlighting is visually distinct from priority badge
#### Story: Add orange badge for P2 priority tasks
**Acceptance Criteria:**
- P2 priority tasks display an orange badge/indicator
- Orange badge is clearly visible and distinguishable from P1 and P3
- Badge appears consistently across all views
- Badge color meets contrast requirements for readability

#### Story: Add gray badge for P3 priority tasks
**Acceptance Criteria:**
- P3 priority tasks display a gray badge/indicator
- Gray badge is clearly visible and distinguishable from P1 and P2
- Badge appears consistently across all views

#### Story: Sort overdue tasks to appear first
**Acceptance Criteria:**
- Overdue incomplete tasks appear at the top of the task list
- Overdue tasks are prioritized above all other tasks
- Sorting updates automatically when a task becomes overdue
- Completed tasks are not included in overdue sorting

#### Story: Sort by priority within each group (P1 → P2 → P3)
**Acceptance Criteria:**
- Within overdue tasks, P1 appears before P2, P2 before P3
- Within non-overdue tasks, P1 appears before P2, P2 before P3
- Priority sorting is consistent across all task groups
- All priority levels are handled correctly

#### Story: Sort by due date ascending within priority groups
**Acceptance Criteria:**
- Tasks with the same priority are sorted by due date (soonest first)
- Date sorting is ascending (earlier dates appear first)
- Sorting applies within both overdue and non-overdue groups
- Date comparison is accurate

#### Story: Place tasks without due dates at the end of the list
**Acceptance Criteria:**
- Tasks without due dates appear after all tasks with due dates
- Undated tasks are sorted by priority among themselves (P1 → P2 → P3)
- Undated tasks do not interfere with dated task sorting
- Both completed and incomplete undated tasks follow this rule

#### Story: Maintain sort order when filters are applied
**Acceptance Criteria:**
- Sorting rules apply consistently in All, Today, and Overdue views
- Filter changes do not break or reset the sort order
- Sort order is intuitive and predictable in each filter view
- Performance remains acceptable with sorting or accompanied by color badges
- Color coding is consistent: red for P1, orange for P2, gray for P3
- Badges are visually clear and enhance user understanding
- Priority remains identifiable even with badges

### Epic: Add Overdue Task Highlighting
- Story: Detect overdue tasks based on current date
- Story: Apply red highlighting to overdue task rows

### Epic: Implement Advanced Task Sorting
- Story: Sort overdue tasks to appear first
- Story: Sort by priority within each group (P1 → P2 → P3)
- Story: Sort by due date ascending within priority groups
- Story: Place tasks without due dates at the end of the list
- Story: Maintain sort order when filters are applied
