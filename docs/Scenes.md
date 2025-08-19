## Scenes (Pages) and Routing

Routing is defined in `src/App.js` using `react-router-dom`.

### Routes
`/` → `src/scenes/dashboard/index.jsx` (Dashboard)
`/team` → `src/scenes/team/index.jsx`
`/contacts` → `src/scenes/contacts/index.jsx`
`/invoices` → `src/scenes/invoices/index.jsx`
`/form` → `src/scenes/form/index.jsx`
`/calendar` → `src/scenes/calendar/calendar.jsx`
`/faq` → `src/scenes/faq/index.jsx`
`/bar` → `src/scenes/bar/index.jsx`
`/pie` → `src/scenes/pie/index.jsx`
`/line` → `src/scenes/line/index.jsx`
`/geography` → `src/scenes/geography/index.jsx`

### Dashboard
Uses `Header`, four `StatBox` KPIs, and embeds `LineChart`, `BarChart`, `GeographyChart`.

### DataGrid Pages
Team, Contacts, Invoices use MUI X `DataGrid` with custom theming and toolbar.

### Form
`src/scenes/form/index.jsx` uses `Formik` and `yup` validation with responsive grid.

### Calendar
FullCalendar configured with dayGrid, timeGrid, list, and interaction plugins. Supports add/delete and sidebar event list.

### Chart Scenes
Bar, Line, Pie, Geography pages show full-size charts with `Header` and a tall container for responsiveness.

## Scenes (Pages) and Routing

Routing is defined in `src/App.js` using `react-router-dom`.

### Routes
`/` → `src/scenes/dashboard/index.jsx` (Dashboard)
`/team` → `src/scenes/team/index.jsx`
`/contacts` → `src/scenes/contacts/index.jsx`
`/invoices` → `src/scenes/invoices/index.jsx`
`/form` → `src/scenes/form/index.jsx`
`/calendar` → `src/scenes/calendar/calendar.jsx`
`/faq` → `src/scenes/faq/index.jsx`
`/bar` → `src/scenes/bar/index.jsx`
`/pie` → `src/scenes/pie/index.jsx`
`/line` → `src/scenes/line/index.jsx`
`/geography` → `src/scenes/geography/index.jsx`

### Dashboard
Uses `Header`, four `StatBox` KPIs, and embeds `LineChart`, `BarChart`, `GeographyChart`.

### DataGrid Pages
Team, Contacts, Invoices use MUI X `DataGrid` with custom theming and toolbar.

### Form
`src/scenes/form/index.jsx` uses `Formik` and `yup` validation with responsive grid.

### Calendar
FullCalendar configured with dayGrid, timeGrid, list, and interaction plugins. Supports add/delete and sidebar event list.

### Chart Scenes
Bar, Line, Pie, Geography pages show full-size charts with `Header` and a tall container for responsiveness.

