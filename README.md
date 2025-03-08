# Amazigh Calendar Webpage

This repository contains the code for a simple, interactive Amazigh calendar webpage.  It displays the Amazigh calendar alongside the corresponding Gregorian calendar dates, allows navigation between months, and provides conversion between Amazigh and Gregorian dates.

**Live Demo:** [https://abdelhaqueidali.github.io/Amazigh-Calendar-MA/](https://abdelhaqueidali.github.io/Amazigh-Calendar-MA/)

## Features

*   **Dual Calendar Display:** Shows both the Amazigh and Gregorian calendar dates for the selected month.  The Amazigh calendar is the primary display, with Gregorian dates shown as secondary information.
*   **Month Navigation:**  Buttons to navigate to the previous and next month.
*   **"Go to Today" Button:**  Quickly jumps back to the current date.
*   **Date Selection:** Clicking on a day in the calendar selects it, highlighting the cell and updating input fields.
*   **Date Conversion:**
    *   Input fields for both Gregorian and Amazigh dates (DD/MM/YYYY format).
    *   A "Go to Date" button applies the date entered in *either* input field.
    *   Entering a Gregorian date automatically calculates and displays the equivalent Amazigh date.
    *   Entering an Amazigh date automatically calculates and displays the equivalent Gregorian date.
    *   Error handling for invalid date input.
*   **Current Date Highlighting:** The current day is highlighted with a distinct background color ("today" class).
*   **Selected Date Highlighting:** The currently selected day is highlighted with a different background color ("selected" class).
*   **Amazigh Month Names:** Uses the proper Amazigh month names (e.g., "ⵉⵏⵏⴰⵢⵔ", "ⴱⵕⴰⵢⵕ").
* **Amazigh Day Names:**  Uses Amazigh names for the days of the week.
* **Clear Gregorian/Amazigh Display:**  Shows the currently displayed Gregorian and Amazigh dates above the calendar grid.  Also displays the *current* (today's) Gregorian and Amazigh date, which is separate from the selected date display.
* **Responsive Design:** Adapts to different screen sizes.

## Technologies Used

*   **HTML:**  Structure of the webpage.
*   **CSS:**  Styling and layout.
*   **JavaScript:**  Calendar logic, date calculations, event handling, and DOM manipulation.

## Code Overview

The JavaScript code (`<script>` tag in the HTML) handles the core functionality:

1.  **`getAmazighDate(gregorianDate)`:**  Converts a Gregorian `Date` object to an Amazigh date object (`{year, month, day}`).  The Amazigh year is calculated by adding 950 to the Gregorian year.  The day difference is handled, accounting for month boundaries and year changes.

2.  **`getGregorianDate(amazighYear, amazighMonth, amazighDay)`:** Converts an Amazigh date (year, month, day) to a Gregorian `Date` object.  This is the inverse of `getAmazighDate`.  It correctly handles the 13-day offset and wraps around year boundaries.

3.  **`renderCalendar(date)`:**  This is the main function that updates the calendar display.
    *   Calculates the Amazigh date corresponding to the input `date` (which is a Gregorian date).
    *   Determines the first day of the Amazigh month (converted to Gregorian for display purposes).
    *   Calculates the number of days in the month (using the Gregorian date).
    *   Gets the day of the week the month starts on (using the Gregorian date of the 1st of the *Amazigh* month).
    *   Clears the previous calendar content.
    *   Generates the calendar table rows and cells.  Empty cells are created for days before the start of the month and, importantly, *are kept visible* with a border.
    *   Adds the "today" class to the current day's cell.
    *   Adds the "selected" class to the selected day's cell.
    *   Adds event listeners to each cell for date selection.  Clicking a cell updates the `selectedDate`, the input fields, and re-renders the calendar.
    *   Updates the display of the current month and year (both Amazigh and Gregorian).
    *   Displays the current (today's) Amazigh and Gregorian dates.
    * **Gregorian Sub-display in cells:** Each cell displays *both* the Amazigh day number *and* a smaller Gregorian date (month and day) in a `<div>` with the class `gregorian-date`.  This is a key improvement.

4.  **`getMonthName(monthIndex)`:**  Returns the Amazigh name of the month, given its index (0-11).

5.  **`formatDate(date)`:**  Formats a `Date` object as "DD/MM/YYYY".  Handles cases where the date might be null or undefined.

6.  **Event Listeners:**
    *   "Prev Month" and "Next Month" buttons:  Decrement/increment the `currentDate` and `selectedDate`, re-render the calendar, and update the input fields.
    *   "Go to Today" button:  Resets `currentDate` and `selectedDate` to the current date, re-renders, and updates inputs.
    *   "Go to Date" button:  Parses the date from *either* the Gregorian or Amazigh input field, updates `currentDate` and `selectedDate`, re-renders the calendar, and updates *both* input fields to reflect the change.  Includes error handling for invalid date formats.
    *   Click events on calendar cells (handled within `renderCalendar`).

7.  **Initial `renderCalendar(currentDate)` call:**  Displays the calendar for the current month on page load.

## How to Use

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/AbdelhaqueIdali/Amazigh-Calendar-MA.git
    ```

2.  **Open `index.html` in your browser.**  No server is required; it's a static webpage.

## Improvements over a Basic Calendar

*   **Bidirectional Date Conversion:** The key improvement is the ability to enter *either* a Gregorian *or* an Amazigh date and have the other date calculated automatically.  This is significantly more user-friendly than a calendar that only converts in one direction.
*   **Clear Separation of Current and Selected Dates:** The "Today is:" section always shows the actual current date, while the calendar heading and top display show the date of the currently *displayed* month (which may be different).
*   **Gregorian Dates Within Cells:** Showing the Gregorian date alongside the Amazigh date within each calendar cell makes the calendar much more useful for users who are familiar with the Gregorian calendar.
*   **Robust Date Handling:** The code carefully handles the day offset between the calendars and ensures correct calculations even when crossing month and year boundaries.
*   **Input Validation:** The "Go to Date" button includes basic validation to prevent errors from invalid date strings.
*   **User-Friendly Input:** Uses DD/MM/YYYY format, which is common and easily understood.
* **Empty cell visibility:** Empty cells maintain visible border.

## Potential Further Enhancements

*   **More Robust Input Validation:**  Implement more comprehensive date validation to prevent invalid dates (e.g., February 30th).  Consider using a date picker library.
*   **Localization:**  Add support for displaying the calendar in different languages (e.g., providing options for English, French, and Arabic month/day names).
*   **Holidays/Events:**  Allow displaying Amazigh holidays or other significant events on the calendar.
*   **Year Navigation:** Add buttons or a dropdown to easily navigate to different years.
*   **Accessibility:**  Improve accessibility by adding ARIA attributes and ensuring proper keyboard navigation.
*   **Testing:** Add unit tests to verify the date conversion logic.
*   **Date Picker Library:** Replace the simple text inputs with a proper date picker component (e.g., from a library like Flatpickr, Pikaday, or a framework-specific component) for a better user experience. This would automatically handle date validation and formatting.
