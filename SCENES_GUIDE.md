# Scenes & Pages Guide

## Overview

Scenes are full-page components that represent different sections of the dashboard application. Each scene is designed as a complete page with its own layout, functionality, and data management.

## Scene Components

### Dashboard Scene

**File:** `src/scenes/dashboard/index.jsx`

The main landing page displaying key metrics, charts, and recent activity.

#### Features

- **Statistics Overview**: Four StatBox components showing key metrics
- **Multiple Visualizations**: Line chart, bar chart, geography chart
- **Recent Transactions**: Live transaction feed
- **Download Reports**: Export functionality
- **Responsive Grid Layout**: CSS Grid implementation

#### Layout Structure

```jsx
// Grid configuration
<Box
  display="grid"
  gridTemplateColumns="repeat(12, 1fr)"
  gridAutoRows="140px"
  gap="20px"
>
  {/* Row 1: Statistics */}
  <Box gridColumn="span 3">
    <StatBox {...emailStats} />
  </Box>
  <Box gridColumn="span 3">
    <StatBox {...salesStats} />
  </Box>
  <Box gridColumn="span 3">
    <StatBox {...clientStats} />
  </Box>
  <Box gridColumn="span 3">
    <StatBox {...trafficStats} />
  </Box>

  {/* Row 2: Line Chart & Transactions */}
  <Box gridColumn="span 8" gridRow="span 2">
    <LineChart isDashboard={true} />
  </Box>
  <Box gridColumn="span 4" gridRow="span 2">
    {/* Transactions list */}
  </Box>

  {/* Row 3: Bar Chart & Geography */}
  <Box gridColumn="span 4" gridRow="span 2">
    <BarChart isDashboard={true} />
  </Box>
  <Box gridColumn="span 4" gridRow="span 2">
    <GeographyChart isDashboard={true} />
  </Box>
</Box>
```

#### Usage Example

```jsx
import Dashboard from '../scenes/dashboard';
import { Route } from 'react-router-dom';

// In App.js routing
<Route path="/" element={<Dashboard />} />
```

#### Key Metrics Displayed

1. **Emails Sent**: 12,361 (+14%)
2. **Sales Obtained**: 431,225 (+21%)
3. **New Clients**: 32,441 (+5%)
4. **Traffic Received**: 1,325,134 (+43%)

---

### Team Management Scene

**File:** `src/scenes/team/index.jsx`

A data grid displaying team members with role-based access indicators.

#### Features

- **Data Grid**: Material-UI DataGrid component
- **Role Visualization**: Color-coded access levels
- **Sortable Columns**: All columns support sorting
- **Responsive Design**: Adapts to screen size
- **Custom Cell Rendering**: Special rendering for access levels

#### Data Grid Configuration

```jsx
const columns = [
  { field: "id", headerName: "ID" },
  {
    field: "name",
    headerName: "Name", 
    flex: 1,
    cellClassName: "name-column--cell"
  },
  {
    field: "age",
    headerName: "Age",
    type: "number",
    headerAlign: "left",
    align: "left"
  },
  {
    field: "phone",
    headerName: "Phone Number",
    flex: 1
  },
  {
    field: "email", 
    headerName: "Email",
    flex: 1
  },
  {
    field: "accessLevel",
    headerName: "Access Level",
    flex: 1,
    renderCell: ({ row: { access } }) => {
      return (
        <Box
          width="60%"
          m="0 auto"
          p="5px"
          display="flex"
          justifyContent="center"
          backgroundColor={
            access === "admin"
              ? colors.greenAccent[600]
              : access === "manager"
              ? colors.greenAccent[700]
              : colors.greenAccent[700]
          }
          borderRadius="4px"
        >
          {access === "admin" && <AdminPanelSettingsOutlinedIcon />}
          {access === "manager" && <SecurityOutlinedIcon />}
          {access === "user" && <LockOpenOutlinedIcon />}
          <Typography color={colors.grey[100]} sx={{ ml: "5px" }}>
            {access}
          </Typography>
        </Box>
      );
    }
  }
];
```

#### Usage Example

```jsx
import Team from '../scenes/team';

// In routing
<Route path="/team" element={<Team />} />
```

#### Access Level Indicators

- **Admin**: Green background with admin icon
- **Manager**: Darker green with security icon  
- **User**: Standard green with unlock icon

---

### Form Scene

**File:** `src/scenes/form/index.jsx`

A comprehensive form for adding new employee profiles with validation.

#### Features

- **Formik Integration**: Form state management
- **Yup Validation**: Schema-based validation
- **Responsive Layout**: Mobile-first design
- **Real-time Validation**: Field-level error display
- **Phone Number Validation**: Regex-based phone validation

#### Form Schema

```javascript
const userSchema = yup.object().shape({
  firstName: yup.string().required("required"),
  lastName: yup.string().required("required"),
  email: yup.string().email("invalid email").required("required"),
  contact: yup
    .string()
    .matches(phoneRegExp, "Phone number is not valid")
    .required("required"),
  address1: yup.string().required("required"),
  address2: yup.string().required("required")
});

const phoneRegExp = /^((\+[1-9]{1,4}[ -]?)|(\([0-9]{2,3}\)[ -]?)|([0-9]{2,4})[ -]?)*?[0-9]{3,4}[ -]?[0-9]{3,4}$/;
```

#### Form Implementation

```jsx
<Formik
  onSubmit={handleFormSubmit}
  initialValues={initialValues}
  validationSchema={userSchema}
>
  {({
    values,
    errors,
    touched,
    handleBlur,
    handleChange,
    handleSubmit,
  }) => (
    <form onSubmit={handleSubmit}>
      <Box
        display="grid"
        gap="30px"
        gridTemplateColumns="repeat(4, minmax(0, 1fr))"
        sx={{
          "& > div": { 
            gridColumn: isNonMobile ? undefined : "span 4" 
          }
        }}
      >
        <TextField
          fullWidth
          variant="filled"
          type="text"
          label="First Name"
          onBlur={handleBlur}
          onChange={handleChange}
          value={values.firstName}
          name="firstName"
          error={!!touched.firstName && !!errors.firstName}
          helperText={touched.firstName && errors.firstName}
          sx={{ gridColumn: "span 2" }}
        />
        {/* Additional fields... */}
      </Box>
    </form>
  )}
</Formik>
```

#### Usage Example

```jsx
import Form from '../scenes/form';

<Route path="/form" element={<Form />} />
```

---

### Calendar Scene

**File:** `src/scenes/calendar/calendar.jsx`

Interactive calendar component with event management capabilities.

#### Features

- **FullCalendar Integration**: Complete calendar functionality
- **Event Management**: Add, edit, delete events
- **Multiple Views**: Month, week, day views
- **Interactive**: Click to add events
- **Responsive**: Mobile-friendly interface

#### Usage Example

```jsx
import Calendar from '../scenes/calendar/calendar';

<Route path="/calendar" element={<Calendar />} />
```

---

### Chart Scenes

Individual scenes for each chart type, providing full-page chart experiences.

#### Bar Chart Scene

**File:** `src/scenes/bar/index.jsx`

```jsx
import BarChart from '../../components/BarChart';
import Header from '../../components/Header';

const Bar = () => {
  return (
    <Box m="20px">
      <Header title="Bar Chart" subtitle="Simple Bar Chart" />
      <Box height="75vh">
        <BarChart />
      </Box>
    </Box>
  );
};
```

#### Line Chart Scene

**File:** `src/scenes/line/index.jsx`

```jsx
import LineChart from '../../components/LineChart';
import Header from '../../components/Header';

const Line = () => {
  return (
    <Box m="20px">
      <Header title="Line Chart" subtitle="Simple Line Chart" />
      <Box height="75vh">
        <LineChart />
      </Box>
    </Box>
  );
};
```

#### Pie Chart Scene

**File:** `src/scenes/pie/index.jsx`

```jsx
import PieChart from '../../components/PieChart';
import Header from '../../components/Header';

const Pie = () => {
  return (
    <Box m="20px">
      <Header title="Pie Chart" subtitle="Simple Pie Chart" />
      <Box height="75vh">
        <PieChart />
      </Box>
    </Box>
  );
};
```

#### Geography Scene

**File:** `src/scenes/geography/index.jsx`

```jsx
import GeographyChart from '../../components/GeographyChart';
import Header from '../../components/Header';

const Geography = () => {
  return (
    <Box m="20px">
      <Header title="Geography" subtitle="Simple Geography Chart" />
      <Box height="75vh">
        <GeographyChart />
      </Box>
    </Box>
  );
};
```

---

## Data Management Scenes

### Contacts Scene

**File:** `src/scenes/contacts/index.jsx`

Contact management with detailed information display.

#### Features

- **Data Grid**: Comprehensive contact information
- **Search and Filter**: Built-in grid functionality
- **Export Capabilities**: Data export options
- **Responsive Columns**: Adaptive column sizing

#### Usage Example

```jsx
import Contacts from '../scenes/contacts';

<Route path="/contacts" element={<Contacts />} />
```

### Invoices Scene

**File:** `src/scenes/invoices/index.jsx`

Invoice management and tracking system.

#### Features

- **Invoice Listing**: Complete invoice data grid
- **Status Tracking**: Payment status indicators
- **Financial Metrics**: Cost and balance calculations
- **Date Management**: Invoice date tracking

#### Usage Example

```jsx
import Invoices from '../scenes/invoices';

<Route path="/invoices" element={<Invoices />} />
```

---

## FAQ Scene

**File:** `src/scenes/faq/index.jsx`

Frequently asked questions with expandable accordion interface.

#### Features

- **Accordion Layout**: Expandable question sections
- **Search Functionality**: Find specific questions
- **Categorized Content**: Organized FAQ sections
- **Responsive Design**: Mobile-friendly layout

#### Usage Example

```jsx
import FAQ from '../scenes/faq';

<Route path="/faq" element={<FAQ />} />
```

---

## Scene Patterns and Best Practices

### Standard Scene Structure

```jsx
import { Box, useTheme } from '@mui/material';
import { tokens } from '../../theme';
import Header from '../../components/Header';

const MyScene = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <Box m="20px">
      {/* Standard header */}
      <Header 
        title="Page Title" 
        subtitle="Page Description" 
      />
      
      {/* Main content area */}
      <Box
        backgroundColor={colors.primary[400]}
        borderRadius="8px"
        p="20px"
      >
        {/* Scene-specific content */}
      </Box>
    </Box>
  );
};

export default MyScene;
```

### Data Grid Pattern

```jsx
import { DataGrid } from '@mui/x-data-grid';
import { mockData } from '../../data/mockData';

const DataScene = () => {
  const columns = [
    { field: 'id', headerName: 'ID', width: 90 },
    { field: 'name', headerName: 'Name', flex: 1 },
    // ... more columns
  ];

  return (
    <Box m="20px">
      <Header title="Data Management" subtitle="Manage your data" />
      
      <Box
        height="75vh"
        sx={{
          "& .MuiDataGrid-root": {
            border: "none",
          },
          "& .MuiDataGrid-cell": {
            borderBottom: "none",
          },
          // ... more DataGrid styling
        }}
      >
        <DataGrid
          rows={mockData}
          columns={columns}
          checkboxSelection
        />
      </Box>
    </Box>
  );
};
```

### Chart Scene Pattern

```jsx
import ChartComponent from '../../components/ChartComponent';

const ChartScene = () => {
  return (
    <Box m="20px">
      <Header 
        title="Chart Title" 
        subtitle="Chart Description" 
      />
      
      <Box height="75vh">
        <ChartComponent />
      </Box>
    </Box>
  );
};
```

### Form Scene Pattern

```jsx
import { Formik } from 'formik';
import * as yup from 'yup';

const FormScene = () => {
  const handleFormSubmit = (values) => {
    console.log(values);
  };

  return (
    <Box m="20px">
      <Header title="Form Title" subtitle="Form Description" />
      
      <Formik
        onSubmit={handleFormSubmit}
        initialValues={initialValues}
        validationSchema={validationSchema}
      >
        {/* Form implementation */}
      </Formik>
    </Box>
  );
};
```

## Routing Configuration

All scenes are configured in the main App.js file:

```jsx
import { Routes, Route } from 'react-router-dom';

// Import all scenes
import Dashboard from './scenes/dashboard';
import Team from './scenes/team';
import Contacts from './scenes/contacts';
// ... other imports

function App() {
  return (
    <Routes>
      <Route path="/" element={<Dashboard />} />
      <Route path="/team" element={<Team />} />
      <Route path="/contacts" element={<Contacts />} />
      <Route path="/invoices" element={<Invoices />} />
      <Route path="/form" element={<Form />} />
      <Route path="/faq" element={<FAQ />} />
      <Route path="/calendar" element={<Calendar />} />
      <Route path="/bar" element={<Bar />} />
      <Route path="/pie" element={<Pie />} />
      <Route path="/line" element={<Line />} />
      <Route path="/geography" element={<Geography />} />
    </Routes>
  );
}
```

This guide provides comprehensive information about implementing and customizing scene components in the portfolio dashboard application.