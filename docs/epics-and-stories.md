# Epics and Stories - TODO App Enhancement

## MVP Epics and Stories

### Epic: Add Priority Field to Tasks

#### Story: Add priority field to task data model
**Acceptance Criteria:**
- Task object includes a `priority` field
- Priority field accepts only "P1", "P2", or "P3" as valid values
- Priority field defaults to "P3" when not specified
- Existing tasks without priority field are handled gracefully

**Technical Requirements:**
- Update task interface/type definition to include `priority: 'P1' | 'P2' | 'P3'`
- Modify task constructor/factory to set default priority to "P3"
- Add migration logic to handle existing tasks without priority field
- Update frontend state management to include priority field

#### Story: Add priority dropdown to task creation form
**Acceptance Criteria:**
- Task creation form displays a priority dropdown/selector
- Dropdown shows three options: P1, P2, P3
- Dropdown defaults to P3 when creating a new task
- Priority value is included when submitting the form

**Technical Requirements:**
- Add select/dropdown component to TaskForm component
- Use MUI Select component for consistent styling
- Define priority options array: ['P1', 'P2', 'P3']
- Set initial form state for priority to "P3"
- Include priority in form submission handler

#### Story: Add priority dropdown to task edit form
**Acceptance Criteria:**
- Task edit form displays a priority dropdown/selector
- Dropdown shows three options: P1, P2, P3
- Dropdown pre-populates with the task's current priority value
- Updated priority value is saved when form is submitted

**Technical Requirements:**
- Add select/dropdown component to edit mode in TaskForm
- Use MUI Select component for consistent styling
- Pre-populate dropdown value from existing task.priority
- Update form submission handler to include modified priority
- Handle priority field in edit task function

#### Story: Display priority value on task list items
**Acceptance Criteria:**
- Each task in the list displays its priority value (P1, P2, or P3)
- Priority is visible and easy to identify
- Display updates immediately when priority is changed

**Technical Requirements:**
- Update TaskList component to display priority field
- Add priority text/label to each task item rendering
- Use MUI Typography or Chip component for display
- Ensure component re-renders when priority changes
- Position priority display appropriately in task layout

#### Story: Set default priority to P3 for new tasks
**Acceptance Criteria:**
- New tasks automatically have priority set to "P3"
- Default applies when priority is not explicitly provided
- Form UI reflects P3 as the default selection

**Technical Requirements:**
- Set default value in task creation function/constructor
- Initialize form state with priority: "P3"
- Add fallback logic: `priority: task.priority || 'P3'`
- Update task creation handler in App.js to ensure default
- Add unit tests for default priority behavior

#### Story: Persist priority to local storage
**Acceptance Criteria:**
- Priority value is saved to local storage when task is created
- Priority value is saved to local storage when task is updated
- Priority value is retrieved correctly from local storage on app load
- Local storage schema accommodates the new priority field

**Technical Requirements:**
- Update localStorage save function to include priority field
- Modify JSON serialization to handle priority
- Update localStorage load function to retrieve priority
- Add error handling for corrupted storage data
- Test localStorage operations with priority field

#### Story: Validate priority values (P1, P2, P3 only)
**Acceptance Criteria:**
- Only "P1", "P2", or "P3" are accepted as valid priority values
- Invalid priority values are rejected or ignored
- Invalid values default to "P3"
- Validation occurs before saving to local storage

**Technical Requirements:**
- Create validation function: `isValidPriority(value)`
- Implement validation logic: `['P1', 'P2', 'P3'].includes(value)`
- Add validation in form submission handler
- Add validation in localStorage load function
- Sanitize priority values with: `sanitizePriority(value) => valid ? value : 'P3'`

### Epic: Add Due Date Field to Tasks

#### Story: Add dueDate field to task data model
**Acceptance Criteria:**
- Task object includes an optional `dueDate` field
- dueDate field stores date in ISO format (YYYY-MM-DD)
- dueDate can be null or undefined (optional field)
- Existing tasks without dueDate field are handled gracefully

**Technical Requirements:**
- Update task interface/type to include `dueDate?: string | null`
- Store dates as ISO 8601 strings (YYYY-MM-DD format)
- Modify task constructor to accept optional dueDate parameter
- Update frontend state management to include dueDate field
- Handle null/undefined dueDate values throughout the app

#### Story: Add date picker to task creation form
**Acceptance Criteria:**
- Task creation form displays a date picker input
- Date picker allows users to select a due date
- Date picker is optional (users can leave it blank)
- Selected date is included when submitting the form

**Technical Requirements:**
- Add date input field to TaskForm component
- Use HTML5 date input type or MUI DatePicker component
- Set input type="date" for native date picker
- Initialize form state for dueDate (null or empty string)
- Include dueDate in form submission handler
- Handle empty date values (convert to null)

#### Story: Add date picker to task edit form
**Acceptance Criteria:**
- Task edit form displays a date picker input
- Date picker pre-populates with the task's current due date (if set)
- Users can clear/remove the due date
- Updated due date is saved when form is submitted

**Technical Requirements:**
- Add date input field to edit mode in TaskForm
- Pre-populate input value with task.dueDate if exists
- Allow clearing date value (set to null)
- Update form submission handler to include modified dueDate
- Handle null dueDate values in edit task function

#### Story: Display due date on task list items
**Acceptance Criteria:**
- Each task in the list displays its due date (if set)
- Date is displayed in a readable format
- Tasks without a due date show no date or indicate "No due date"
- Display updates immediately when due date is changed

**Technical Requirements:**
- Update TaskList component to display dueDate field
- Format date for display using Date.toLocaleDateString() or similar
- Add conditional rendering: display only if dueDate exists
- Use MUI Typography component for date display
- Position date display appropriately in task layout

#### Story: Validate date format (YYYY-MM-DD)
**Acceptance Criteria:**
- Due dates are stored in ISO format YYYY-MM-DD
- Date input accepts valid dates only
- Date format validation occurs before saving

**Technical Requirements:**
- Create validation function: `isValidDate(dateString)`
- Use regex or Date object to validate YYYY-MM-DD format
- Implement validation: `/^\d{4}-\d{2}-\d{2}$/`
- Add validation in form submission handler
- Validate parsed dates are real (not invalid like 2024-02-30)

#### Story: Handle invalid date values by ignoring them
**Acceptance Criteria:**
- Invalid date values are ignored and treated as absent
- Tasks with invalid dates behave as if they have no due date
- Invalid dates do not cause errors or app crashes
- Validation provides clear feedback for invalid dates

**Technical Requirements:**
- Create sanitization function: `sanitizeDate(value)`
- Return null for invalid date values
- Add try-catch blocks around date parsing
- Implement validation in localStorage load function
- Add error boundary or fallback for date operations

#### Story: Persist due date to local storage
**Acceptance Criteria:**
- Due date value is saved to local storage when task is created
- Due date value is saved to local storage when task is updated
- Due date value is retrieved correctly from local storage on app load
- Null/undefined due dates are handled properly in storage

**Technical Requirements:**
- Update localStorage save function to include dueDate field
- Ensure JSON.stringify handles null dueDate values correctly
- Update localStorage load function to retrieve dueDate
- Parse dueDate as string (no Date object conversion needed)
- Test localStorage operations with null and valid dates

### Epic: Implement Task Filtering

#### Story: Add filter tabs UI (All, Today, Overdue)
**Acceptance Criteria:**
- Three filter tabs are displayed: All, Today, Overdue
- Tabs are clearly labeled and easy to identify
- Active tab is visually distinct from inactive tabs
- Clicking a tab switches to that filter view
- Filter state persists during the session

**Technical Requirements:**
- Add filter state to App component: `const [filter, setFilter] = useState('all')`
- Use MUI Tabs or ButtonGroup component for filter UI
- Create three tab/button elements: 'all', 'today', 'overdue'
- Add click handlers to update filter state
- Apply active styling based on current filter value
- Position filter tabs above task list

#### Story: Implement "All" filter to show all tasks
**Acceptance Criteria:**
- "All" filter displays all tasks regardless of status or due date
- Both completed and incomplete tasks are shown
- Tasks with and without due dates are shown
- "All" is the default filter on app load

**Technical Requirements:**
- Create filter function: `filterTasks(tasks, filterType)`
- For 'all' filter: return all tasks without filtering
- Set default filter state to 'all' in useState
- Apply filter function before rendering TaskList
- No additional logic needed for 'all' case

#### Story: Implement "Today" filter to show incomplete tasks due today
**Acceptance Criteria:**
- "Today" filter displays only tasks due today
- Only incomplete tasks are shown
- Completed tasks due today are hidden
- Tasks without due dates are not shown
- "Today" is calculated based on current date

**Technical Requirements:**
- Get today's date: `new Date().toISOString().split('T')[0]`
- Filter logic: `task.dueDate === todayString && !task.completed`
- Handle timezone considerations for date comparison
- Add 'today' case to filterTasks function
- Return filtered array of matching tasks

#### Story: Implement "Overdue" filter to show incomplete tasks past due date
**Acceptance Criteria:**
- "Overdue" filter displays only tasks past their due date
- Only incomplete tasks are shown
- Completed tasks that were overdue are hidden
- Tasks without due dates are not shown
- Overdue status is calculated based on current date

**Technical Requirements:**
- Get today's date for comparison: `new Date().toISOString().split('T')[0]`
- Filter logic: `task.dueDate < todayString && !task.completed && task.dueDate`
- Handle null dueDate values (exclude from overdue)
- Add 'overdue' case to filterTasks function
- Use string comparison for date comparison (works with ISO format)

#### Story: Hide completed tasks in Today filter view
**Acceptance Criteria:**
- Completed tasks do not appear in "Today" filter
- Only incomplete tasks due today are displayed
- Marking a task as complete removes it from Today view
- Unmarking a completed task shows it in Today view (if due today)

**Technical Requirements:**
- Add `!task.completed` condition to Today filter logic
- Combined filter: `task.dueDate === todayString && !task.completed`
- Ensure filter recomputes when task completion status changes
- Test toggling completion status in Today view
- Verify completed tasks are excluded from results

#### Story: Hide completed tasks in Overdue filter view
**Acceptance Criteria:**
- Completed tasks do not appear in "Overdue" filter
- Only incomplete overdue tasks are displayed
- Marking a task as complete removes it from Overdue view
- Unmarking a completed task shows it in Overdue view (if overdue)

**Technical Requirements:**
- Add `!task.completed` condition to Overdue filter logic
- Combined filter: `task.dueDate < todayString && !task.completed && task.dueDate`
- Ensure filter recomputes when task completion status changes
- Test toggling completion status in Overdue view
- Verify completed tasks are excluded from results

#### Story: Show completed tasks in All filter view
**Acceptance Criteria:**
- Completed tasks are visible in "All" filter
- Completed tasks are displayed alongside incomplete tasks
- Completed status is clearly indicated (e.g., strikethrough)

**Technical Requirements:**
- 'All' filter returns all tasks without completion status filtering
- Apply visual styling for completed tasks (CSS: text-decoration: line-through)
- Update TaskList component to show completion status
- No additional filtering logic needed for 'all' case
- Ensure existing completion checkbox/toggle still works

---

## Post-MVP Epics and Stories

### Epic: Add Visual Priority Indicators

#### Story: Add red badge for P1 priority tasks
**Acceptance Criteria:**
- P1 priority tasks display a red badge/indicator
- Red badge is clearly visible and distinguishable
- Badge appears consistently across all views
- Badge color meets contrast requirements for readability

**Technical Requirements:**
- Use MUI Chip component with color="error" for P1 badge
- Set badge background color to red (#d32f2f or similar)
- Add priority badge to TaskList item rendering
- Create helper function: `getPriorityColor(priority)`
- Ensure text color contrasts with red background

#### Story: Add orange badge for P2 priority tasks
**Acceptance Criteria:**
- P2 priority tasks display an orange badge/indicator
- Orange badge is clearly visible and distinguishable from P1 and P3
- Badge appears consistently across all views
- Badge color meets contrast requirements for readability

**Technical Requirements:**
- Use MUI Chip component with color="warning" for P2 badge
- Set badge background color to orange (#ff9800 or similar)
- Use same helper function: `getPriorityColor('P2')` returns orange
- Apply consistent styling across all task displays
- Ensure text color contrasts with orange background

#### Story: Add gray badge for P3 priority tasks
**Acceptance Criteria:**
- P3 priority tasks display a gray badge/indicator
- Gray badge is clearly visible and distinguishable from P1 and P2
- Badge appears consistently across all views
- Badge color meets contrast requirements for readability

**Technical Requirements:**
- Use MUI Chip component with color="default" for P3 badge
- Set badge background color to gray (#9e9e9e or similar)
- Use same helper function: `getPriorityColor('P3')` returns gray
- Apply consistent styling across all task displays
- Ensure text color contrasts with gray background

#### Story: Replace text priority display with color-coded badges
**Acceptance Criteria:**
- Priority text (P1, P2, P3) is replaced with or accompanied by color badges
- Color coding is consistent: red for P1, orange for P2, gray for P3
- Badges are visually clear and enhance user understanding
- Priority remains identifiable even with badges

**Technical Requirements:**
- Update TaskList to render Chip components instead of plain text
- Map priority values to colors: {P1: 'error', P2: 'warning', P3: 'default'}
- Use MUI Chip with label={task.priority} and color prop
- Apply consistent badge styling (size, padding, border-radius)
- Keep priority text visible within badge for accessibility

### Epic: Add Overdue Task Highlighting

#### Story: Detect overdue tasks based on current date
**Acceptance Criteria:**
- System correctly identifies tasks past their due date
- Detection compares task due date with current date
- Tasks without due dates are not flagged as overdue
- Completed tasks are not flagged as overdue
- Overdue status updates automatically as dates change

**Technical Requirements:**
- Create helper function: `isOverdue(task)`
- Logic: `task.dueDate && task.dueDate < today && !task.completed`
- Get current date: `new Date().toISOString().split('T')[0]`
- Use string comparison for ISO date format
- Call isOverdue function in TaskList rendering logic

#### Story: Apply red highlighting to overdue task rows
**Acceptance Criteria:**
- Overdue incomplete tasks are visually highlighted in red
- Highlighting makes overdue tasks stand out clearly
- Highlighting applies to the entire task row or background
- Highlighting is removed when task is completed or date is updated
- Red highlighting is visually distinct from priority badges

**Technical Requirements:**
- Add conditional className to task list items: `{isOverdue(task) ? 'overdue' : ''}`
- Define CSS class: `.overdue { background-color: #ffebee; border-left: 4px solid #d32f2f; }`
- Apply styling only when isOverdue returns true
- Use light red background to avoid overwhelming the UI
- Ensure highlighting updates when task status changes

### Epic: Implement Advanced Task Sorting

#### Story: Sort overdue tasks to appear first
**Acceptance Criteria:**
- Overdue incomplete tasks appear at the top of the task list
- Overdue tasks are prioritized above all other tasks
- Sorting updates automatically when a task becomes overdue
- Completed tasks are not included in overdue sorting

**Technical Requirements:**
- Create sorting function: `sortTasks(tasks)`
- Add isOverdue check as first sort criterion
- Use Array.sort() with custom comparator function
- Sort logic: return -1 if task1 is overdue and task2 is not
- Apply sort function before rendering filtered task list

#### Story: Sort by priority within each group (P1 → P2 → P3)
**Acceptance Criteria:**
- Within overdue tasks, P1 appears before P2, P2 before P3
- Within non-overdue tasks, P1 appears before P2, P2 before P3
- Priority sorting is consistent across all task groups
- All priority levels are handled correctly

**Technical Requirements:**
- Map priorities to sort values: {P1: 1, P2: 2, P3: 3}
- Add priority comparison to sort function (second criterion)
- Compare: `priorityMap[task1.priority] - priorityMap[task2.priority]`
- Apply only when overdue status is equal
- Handle missing priority values (default to P3)

#### Story: Sort by due date ascending within priority groups
**Acceptance Criteria:**
- Tasks with the same priority are sorted by due date (soonest first)
- Date sorting is ascending (earlier dates appear first)
- Sorting applies within both overdue and non-overdue groups
- Date comparison is accurate

**Technical Requirements:**
- Add due date comparison to sort function (third criterion)
- Use string comparison: `task1.dueDate.localeCompare(task2.dueDate)`
- Apply only when overdue status and priority are equal
- Handle null dueDate values (place at end)
- ISO date format allows direct string comparison

#### Story: Place tasks without due dates at the end of the list
**Acceptance Criteria:**
- Tasks without due dates appear after all tasks with due dates
- Undated tasks are sorted by priority among themselves (P1 → P2 → P3)
- Undated tasks do not interfere with dated task sorting
- Both completed and incomplete undated tasks follow this rule

**Technical Requirements:**
- Check for null/undefined dueDate in sort function
- Return 1 if task has no due date (push to end)
- Return -1 if comparing task has due date but current doesn't
- Allow priority sorting for undated tasks among themselves
- Handle dueDate presence as part of sort comparison logic

#### Story: Maintain sort order when filters are applied
**Acceptance Criteria:**
- Sorting rules apply consistently in All, Today, and Overdue views
- Filter changes do not break or reset the sort order
- Sort order is intuitive and predictable in each filter view
- Performance remains acceptable with sorting applied

**Technical Requirements:**
- Apply sortTasks() after filterTasks(): `sortTasks(filterTasks(tasks, filter))`
- Ensure sort function is pure (no side effects)
- Test sorting with each filter type (all, today, overdue)
- Optimize sort performance for larger task lists (consider memoization)
- Verify sort order updates when task properties change
