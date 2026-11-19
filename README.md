# SpendWise — Week 6

SpendWise is a lightweight expense-tracking web application built with HTML, CSS, and JavaScript.

## Improvements Made This Week
- Added interactive expense creation with category selection (`Transport`, `Food`, `Shopping`, `Utilities`, `Other`).
- Added input validation and user feedback messages for empty names or invalid amounts.
- Implemented live summary calculations for total spending and entry count.
- Added individual item deletion and a "Clear All" action with an empty-state message.

## How Conditionals Are Used
Conditional statements (`if` / `else` / logical checks) control validation and UI states:
- **Empty list check:** In `renderExpenses()`, `if (expenses.length === 0)` displays a friendly empty-state message instead of an empty list.
- **Form validation:** On form submit, `if (title === "")` blocks blank expense names, and `if (Number.isNaN(amount) || amount <= 0)` rejects non-numeric, zero, or negative amounts.
- **Clear confirmation check:** Clicking "Clear All" checks `if (expenses.length === 0)` so users get clear feedback when the list is already empty.

## How Arrays Are Used to Store Data
- All recorded expenses are stored in the `expenses` array (`let expenses = []`), where each element is an object containing `title`, `amount`, and `category`.
- `expenses.push(newExpense)` appends new entries to the array.
- `for` loops iterate over `expenses` using zero-based indexing (`0` to `expenses.length - 1`) to calculate the total amount and render each row.
- `expenses.splice(i, 1)` removes a specific expense by index when its "Delete" button is clicked, and `expenses = []` resets all entries.

## How the DOM Is Updated
- DOM elements are selected using `document.getElementById()` (such as `#expense-form`, `#expense-list`, `#total-spent`, `#expense-count`, and `#feedback-message`).
- `textContent` is used to safely update totals, counts, feedback messages, and list labels without parsing raw HTML strings.
- `renderExpenses()` rebuilds the `#expense-list` using `document.createElement()` and `appendChild()`, while `updateSummary()` keeps the total and count synchronized after every change.

## How User Interactions Are Handled Through Events
- `addEventListener("submit", ...)` on `#expense-form` listens for form submissions and calls `event.preventDefault()` to stop the browser from reloading the page.
- `addEventListener("click", ...)` on each item's "Delete" button removes that entry and refreshes the view.
- `addEventListener("click", ...)` on `#clear-all-btn` resets the expense list when clicked.

## Challenges Encountered and Resolutions
- **Preventing page reloads on form submit:** Submitting an HTML form normally refreshes the page and clears in-memory state; adding `event.preventDefault()` kept the state intact and allowed custom validation.
- **Handling invalid numeric inputs:** Typing non-numeric text or numbers less than or equal to `0` could break totals; checking `Number.isNaN(amount) || amount <= 0` caught invalid values before pushing to `expenses`.
- **Keeping UI totals and list items in sync:** Calling `updateSummary()` inside `renderExpenses()` ensured that adding, deleting, or clearing expenses always updates both the list and the summary cards together.
