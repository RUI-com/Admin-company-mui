# Portfolio Dashboard API Documentation

## Overview

This is a comprehensive React-based portfolio dashboard application built with Material-UI and Nivo charts. The application provides a modern, responsive interface with dark/light theme support and various data visualization components.

## Table of Contents

1. [Core Components](#core-components)
2. [Chart Components](#chart-components)
3. [Layout Components](#layout-components)
4. [Scene Components](#scene-components)
5. [Theme System](#theme-system)
6. [Data Utilities](#data-utilities)
7. [Usage Examples](#usage-examples)

---

## Core Components

### Header

A reusable header component for page titles and subtitles.

**File:** `src/components/Header.jsx`

#### Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `title` | `string` | Yes | Main heading text |
| `subtitle` | `string` | Yes | Secondary text below title |

#### Usage

```jsx
import Header from '../components/Header';

<Header 
  title="Dashboard" 
  subtitle="Welcome to your dashboard" 
/>
```

#### Features
- Responsive typography using Material-UI variants
- Theme-aware styling with color tokens
- Large, bold title (52px font size)
- Subtitle with green accent color and letter spacing

---

### StatBox

A statistics display component with icon, progress indicator, and metrics.

**File:** `src/components/StatBox.jsx`

#### Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `title` | `string` | Yes | Main statistic value |
| `subtitle` | `string` | Yes | Description of the statistic |
| `icon` | `ReactNode` | Yes | Icon component to display |
| `progress` | `string` | Yes | Progress value (0-1) for progress circle |
| `increase` | `string` | Yes | Percentage increase text |

#### Usage

```jsx
import StatBox from '../components/StatBox';
import EmailIcon from '@mui/icons-material/Email';

<StatBox
  title="12,361"
  subtitle="Emails Sent"
  progress="0.75"
  increase="+14%"
  icon={<EmailIcon sx={{ color: colors.greenAccent[600], fontSize: "26px" }} />}
/>
```

#### Features
- Integrated ProgressCircle component
- Flexible icon support
- Theme-aware color scheme
- Responsive layout with flexbox

---

### ProgressCircle

A circular progress indicator using CSS conic gradients.

**File:** `src/components/ProgressCircle.jsx`

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `progress` | `string` | No | `"0.75"` | Progress value (0-1) |
| `size` | `string` | No | `"40"` | Size in pixels |

#### Usage

```jsx
import ProgressCircle from '../components/ProgressCircle';

<ProgressCircle progress="0.65" size="50" />
```

#### Features
- Pure CSS implementation using conic gradients
- Theme-aware colors
- Customizable size
- Radial gradient background

---

## Chart Components

### BarChart

A responsive bar chart component using Nivo.

**File:** `src/components/BarChart.jsx`

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isDashboard` | `boolean` | No | `false` | Optimized styling for dashboard view |

#### Usage

```jsx
import BarChart from '../components/BarChart';

// Full page chart
<BarChart />

// Dashboard version
<BarChart isDashboard={true} />
```

#### Features
- Uses mock data from `mockBarData`
- Theme-aware styling for axes and legends
- Responsive design
- Food sales data visualization (hot dog, burger, sandwich, etc.)
- Custom color scheme and patterns

#### Data Structure
```javascript
// Expected data format
[
  {
    country: "AD",
    "hot dog": 137,
    "burger": 96,
    "sandwich": 72,
    // ...
  }
]
```

---

### LineChart

A responsive line chart component for trend visualization.

**File:** `src/components/LineChart.jsx`

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isCustomLineColors` | `boolean` | No | `false` | Use custom line colors |
| `isDashboard` | `boolean` | No | `false` | Dashboard optimized view |

#### Usage

```jsx
import LineChart from '../components/LineChart';

// Standard line chart
<LineChart />

// With custom colors for dashboard
<LineChart isDashboard={true} isCustomLineColors={true} />
```

#### Features
- Multiple data series support
- Smooth curve interpolation
- Interactive tooltips and legends
- Theme-aware styling
- Responsive design

---

### PieChart

A responsive pie chart component for categorical data.

**File:** `src/components/PieChart.jsx`

#### Props

No props - uses internal mock data.

#### Usage

```jsx
import PieChart from '../components/PieChart';

<PieChart />
```

#### Features
- Interactive pie slices
- Custom color scheme
- Theme-aware legends and text
- Responsive sizing
- Built-in mock data

---

### GeographyChart

A world map visualization component.

**File:** `src/components/GeographyChart.jsx`

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isDashboard` | `boolean` | No | `false` | Dashboard optimized view |

#### Usage

```jsx
import GeographyChart from '../components/GeographyChart';

<GeographyChart isDashboard={true} />
```

#### Features
- World map with country data
- Interactive hover effects
- Theme-aware coloring
- Geographic data visualization

---

## Layout Components

### Sidebar

Navigation sidebar with collapsible menu items.

**File:** `src/scenes/global/Sidebar.jsx`

#### Features
- Collapsible/expandable sidebar
- Navigation menu with React Router integration
- User profile section with avatar
- Theme-aware styling
- Icon-based navigation items

#### Navigation Items
- Dashboard (Home)
- Team Management
- Contacts Information
- Invoices Balances
- Profile Form
- Calendar
- FAQ Page
- Charts (Bar, Pie, Line, Geography)

#### Usage

```jsx
import Sidebar from '../scenes/global/Sidebar';

<Sidebar />
```

#### Internal Components

**Item Component**
```jsx
const Item = ({ title, to, icon, selected, setSelected }) => {
  // Navigation item with selection state
}
```

---

### Topbar

Top navigation bar with search and utility buttons.

**File:** `src/scenes/global/Topbar.jsx`

#### Features
- Search functionality
- Theme toggle (light/dark mode)
- Notification, settings, and profile buttons
- Theme-aware styling

#### Usage

```jsx
import Topbar from '../scenes/global/Topbar';

<Topbar />
```

#### Interactive Elements
- Search input field
- Theme mode toggle button
- Notifications button
- Settings button
- User profile button

---

## Scene Components

### Dashboard

Main dashboard page with statistics and charts overview.

**File:** `src/scenes/dashboard/index.jsx`

#### Features
- Statistics overview with StatBox components
- Multiple chart visualizations
- Recent transactions list
- Download reports functionality
- Responsive grid layout

#### Layout Structure
- Header with download button
- 4 StatBox components in first row
- Line chart for revenue trends
- Recent transactions sidebar
- Bar chart for campaign performance
- Geography chart for global data
- Progress indicators for various metrics

#### Usage

```jsx
import Dashboard from '../scenes/dashboard';

<Route path="/" element={<Dashboard />} />
```

---

## Theme System

### Color Tokens

**File:** `src/theme.js`

The theme system provides a comprehensive color palette for both dark and light modes.

#### Color Palettes

**Dark Mode Colors:**
```javascript
{
  grey: { 100: "#e0e0e0", 200: "#c2c2c2", ... 900: "#141414" },
  primary: { 100: "#d0d1d5", 200: "#a1a4ab", ... 900: "#040509" },
  greenAccent: { 100: "#dbf5ee", ... 900: "#0f2922" },
  redAccent: { 100: "#f8dcdb", ... 900: "#2c100f" },
  blueAccent: { 100: "#e1e2fe", ... 900: "#151632" }
}
```

**Light Mode Colors:**
```javascript
{
  grey: { 100: "#141414", 200: "#292929", ... 900: "#e0e0e0" },
  primary: { 100: "#040509", 200: "#080b12", ... 900: "#d0d1d5" },
  // Accent colors remain the same
}
```

#### Theme Hook

**useMode Hook:**
```javascript
const [theme, colorMode] = useMode();
```

Returns:
- `theme`: Material-UI theme object
- `colorMode`: Object with `toggleColorMode` function

#### Usage

```jsx
import { useMode, ColorModeContext, tokens } from './theme';

function App() {
  const [theme, colorMode] = useMode();
  
  return (
    <ColorModeContext.Provider value={colorMode}>
      <ThemeProvider theme={theme}>
        {/* Your app components */}
      </ThemeProvider>
    </ColorModeContext.Provider>
  );
}
```

#### Accessing Colors in Components

```jsx
import { useTheme } from '@mui/material';
import { tokens } from '../theme';

const MyComponent = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  
  return (
    <Box sx={{ backgroundColor: colors.primary[400] }}>
      {/* Component content */}
    </Box>
  );
};
```

---

## Data Utilities

### Mock Data

**File:** `src/data/mockData.js`

Provides sample data for all components and visualizations.

#### Available Data Sets

**Team Data:**
```javascript
export const mockDataTeam = [
  {
    id: 1,
    name: "Jon Snow",
    email: "jonsnow@gmail.com",
    age: 35,
    phone: "(665)121-5454",
    access: "admin"
  }
  // ... more team members
];
```

**Contacts Data:**
```javascript
export const mockDataContacts = [
  {
    id: 1,
    name: "Jon Snow",
    email: "jonsnow@gmail.com",
    age: 35,
    phone: "(665)121-5454",
    address: "0912 Won Street, Alabama, SY 10001",
    city: "New York",
    zipCode: "10001",
    registrarId: 123512
  }
  // ... more contacts
];
```

**Chart Data:**
- `mockDataInvoices`: Invoice data for data grid
- `mockTransactions`: Recent transactions data
- `mockBarData`: Bar chart data for food sales
- `mockPieData`: Pie chart data for categorical breakdown
- `mockLineData`: Line chart data for trend analysis

#### Usage

```jsx
import { mockDataTeam, mockBarData } from '../data/mockData';

// Use in components
const teamMembers = mockDataTeam;
```

---

## Usage Examples

### Creating a New Chart Component

```jsx
import { useTheme } from "@mui/material";
import { tokens } from "../theme";

const MyCustomChart = ({ isDashboard = false }) => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <div style={{ 
      height: isDashboard ? "250px" : "500px",
      backgroundColor: colors.primary[400]
    }}>
      {/* Your chart implementation */}
    </div>
  );
};

export default MyCustomChart;
```

### Adding a New Scene/Page

```jsx
import { Box } from "@mui/material";
import Header from "../../components/Header";
import { tokens } from "../../theme";

const MyNewScene = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <Box m="20px">
      <Header title="My Page" subtitle="Page description" />
      
      <Box
        backgroundColor={colors.primary[400]}
        borderRadius="8px"
        p="20px"
      >
        {/* Your page content */}
      </Box>
    </Box>
  );
};

export default MyNewScene;
```

### Using StatBox with Custom Data

```jsx
import StatBox from '../components/StatBox';
import TrendingUpIcon from '@mui/icons-material/TrendingUp';
import { tokens } from '../theme';

const MyStats = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <StatBox
      title="1,234"
      subtitle="Active Users"
      progress="0.85"
      increase="+12%"
      icon={
        <TrendingUpIcon
          sx={{ 
            color: colors.greenAccent[600], 
            fontSize: "26px" 
          }}
        />
      }
    />
  );
};
```

### Implementing Theme Toggle

```jsx
import { useContext } from 'react';
import { IconButton, useTheme } from '@mui/material';
import { ColorModeContext, tokens } from '../theme';
import LightModeOutlinedIcon from '@mui/icons-material/LightModeOutlined';
import DarkModeOutlinedIcon from '@mui/icons-material/DarkModeOutlined';

const ThemeToggle = () => {
  const theme = useTheme();
  const colorMode = useContext(ColorModeContext);

  return (
    <IconButton onClick={colorMode.toggleColorMode}>
      {theme.palette.mode === 'dark' ? (
        <DarkModeOutlinedIcon />
      ) : (
        <LightModeOutlinedIcon />
      )}
    </IconButton>
  );
};
```

---

## Dependencies

The application uses the following key dependencies:

- **React 18.2.0**: Core framework
- **Material-UI 5.15.5**: UI component library
- **Nivo**: Data visualization library
- **React Router DOM 6.21.3**: Routing
- **React Pro Sidebar 0.7.1**: Sidebar component
- **Formik & Yup**: Form handling and validation

## Getting Started

1. **Installation:**
   ```bash
   npm install
   ```

2. **Development:**
   ```bash
   npm start
   ```

3. **Build:**
   ```bash
   npm run build
   ```

## File Structure

```
src/
├── components/          # Reusable components
│   ├── Header.jsx
│   ├── StatBox.jsx
│   ├── ProgressCircle.jsx
│   └── [Chart components]
├── scenes/              # Page components
│   ├── global/         # Global layout components
│   ├── dashboard/      # Dashboard page
│   └── [Other pages]
├── data/               # Mock data and utilities
├── theme.js            # Theme configuration
├── App.js              # Main application
└── index.js            # Entry point
```

This documentation covers all public APIs, components, and utilities in the portfolio dashboard application. Each component is designed to be reusable and theme-aware, following Material-UI best practices.