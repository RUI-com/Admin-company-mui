# Components Reference Guide

## Chart Components

### BarChart Component

**File:** `src/components/BarChart.jsx`

A responsive bar chart component built with Nivo that displays comparative data across categories.

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isDashboard` | `boolean` | No | `false` | Enables dashboard-specific styling and layout |

#### Features

- **Responsive Design**: Automatically adapts to container size
- **Theme Integration**: Uses color tokens from the theme system
- **Interactive Elements**: Hover effects and tooltips
- **Customizable Styling**: Different configurations for dashboard vs full-page view
- **Data Visualization**: Displays food sales data across different countries

#### Usage Examples

**Basic Usage:**
```jsx
import BarChart from '../components/BarChart';

// Full-page bar chart
function ChartsPage() {
  return (
    <Box height="500px">
      <BarChart />
    </Box>
  );
}
```

**Dashboard Usage:**
```jsx
import BarChart from '../components/BarChart';

// Dashboard version with compact styling
function Dashboard() {
  return (
    <Box height="250px">
      <BarChart isDashboard={true} />
    </Box>
  );
}
```

#### Data Structure

The component uses `mockBarData` with the following structure:
```javascript
[
  {
    country: "AD",
    "hot dog": 137,
    "hot dogColor": "hsl(229, 70%, 50%)",
    burger: 96,
    burgerColor: "hsl(296, 70%, 50%)",
    sandwich: 72,
    sandwichColor: "hsl(97, 70%, 50%)",
    kebab: 140,
    kebabColor: "hsl(340, 70%, 50%)",
    fries: 90,
    friesColor: "hsl(12, 70%, 50%)",
    donut: 13,
    donutColor: "hsl(173, 70%, 50%)"
  }
  // ... more countries
]
```

#### Styling Configuration

```javascript
// Theme configuration applied to chart
theme={{
  axis: {
    domain: { line: { stroke: colors.grey[100] }},
    legend: { text: { fill: colors.grey[100] }},
    ticks: {
      line: { stroke: colors.grey[100], strokeWidth: 1 },
      text: { fill: colors.grey[100] }
    }
  },
  legends: { text: { fill: colors.grey[100] }}
}}
```

---

### LineChart Component

**File:** `src/components/LineChart.jsx`

A responsive line chart for displaying trends and time-series data.

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isCustomLineColors` | `boolean` | No | `false` | Enables custom color scheme for lines |
| `isDashboard` | `boolean` | No | `false` | Dashboard-optimized styling |

#### Features

- **Multi-Series Support**: Display multiple data series simultaneously
- **Smooth Curves**: Uses curve interpolation for smooth lines
- **Interactive Tooltips**: Hover to see detailed data points
- **Custom Styling**: Configurable colors and dashboard optimization
- **Responsive**: Adapts to container dimensions

#### Usage Examples

**Standard Line Chart:**
```jsx
import LineChart from '../components/LineChart';

function TrendsPage() {
  return (
    <Box height="400px">
      <LineChart />
    </Box>
  );
}
```

**Dashboard with Custom Colors:**
```jsx
import LineChart from '../components/LineChart';

function Dashboard() {
  return (
    <Box height="250px">
      <LineChart 
        isDashboard={true} 
        isCustomLineColors={true} 
      />
    </Box>
  );
}
```

#### Data Structure

```javascript
[
  {
    id: "japan",
    color: tokens("dark").greenAccent[500],
    data: [
      { x: "plane", y: 101 },
      { x: "helicopter", y: 75 },
      { x: "boat", y: 36 },
      // ... more data points
    ]
  },
  {
    id: "france", 
    color: tokens("dark").blueAccent[300],
    data: [
      // ... data points
    ]
  }
  // ... more series
]
```

---

### PieChart Component

**File:** `src/components/PieChart.jsx`

A responsive pie chart for displaying categorical data distributions.

#### Props

No props required - uses internal mock data configuration.

#### Features

- **Interactive Slices**: Click and hover interactions
- **Custom Colors**: Theme-aware color scheme
- **Legends**: Automatic legend generation
- **Responsive**: Scales with container
- **Accessible**: Screen reader friendly

#### Usage Examples

```jsx
import PieChart from '../components/PieChart';

function DataVisualization() {
  return (
    <Box height="400px">
      <PieChart />
    </Box>
  );
}
```

#### Data Structure

```javascript
[
  {
    id: "hack",
    label: "hack", 
    value: 239,
    color: "hsl(104, 70%, 50%)"
  },
  {
    id: "make",
    label: "make",
    value: 170,
    color: "hsl(162, 70%, 50%)"
  }
  // ... more categories
]
```

---

### GeographyChart Component

**File:** `src/components/GeographyChart.jsx`

A world map visualization component for geographic data representation.

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `isDashboard` | `boolean` | No | `false` | Optimized for dashboard layout |

#### Features

- **World Map**: Complete world geography visualization
- **Interactive**: Hover effects on countries
- **Data Overlay**: Display values on geographic regions
- **Theme Integration**: Follows application theme
- **Responsive**: Adapts to container size

#### Usage Examples

```jsx
import GeographyChart from '../components/GeographyChart';

// Full-page geography chart
function WorldDataPage() {
  return (
    <Box height="500px">
      <GeographyChart />
    </Box>
  );
}

// Dashboard version
function Dashboard() {
  return (
    <Box height="200px">
      <GeographyChart isDashboard={true} />
    </Box>
  );
}
```

---

## UI Components

### Header Component

**File:** `src/components/Header.jsx`

A standardized header component for consistent page titles across the application.

#### Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `title` | `string` | Yes | Main page title |
| `subtitle` | `string` | Yes | Descriptive subtitle |

#### Features

- **Consistent Styling**: Standardized typography across pages
- **Theme Integration**: Uses color tokens for consistent theming
- **Responsive Typography**: Adapts to different screen sizes
- **Accessibility**: Proper heading hierarchy

#### Usage Examples

```jsx
import Header from '../components/Header';

function MyPage() {
  return (
    <Box m="20px">
      <Header 
        title="Team Management" 
        subtitle="Managing the Team Members" 
      />
      {/* Page content */}
    </Box>
  );
}
```

#### Styling Details

```jsx
// Title styling
<Typography
  variant="h1"
  color={colors.grey[100]}
  fontWeight="bold"
  sx={{ 
    m: "0 0 5px 0",
    fontSize: '52px'
  }}
>
  {title}
</Typography>

// Subtitle styling  
<Typography 
  variant="h5" 
  color={colors.greenAccent[400]} 
  sx={{ letterSpacing: '3px' }}
>
  {subtitle}
</Typography>
```

---

### StatBox Component

**File:** `src/components/StatBox.jsx`

A comprehensive statistics display component with icon, value, description, and progress indicator.

#### Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `title` | `string` | Yes | Main statistic value/number |
| `subtitle` | `string` | Yes | Description of the statistic |
| `icon` | `ReactNode` | Yes | Icon component to display |
| `progress` | `string` | Yes | Progress value (0-1) for circular indicator |
| `increase` | `string` | Yes | Percentage change indicator |

#### Features

- **Visual Hierarchy**: Clear display of key metrics
- **Progress Indicator**: Integrated circular progress component
- **Flexible Icons**: Supports any Material-UI icon
- **Theme Awareness**: Consistent with application theme
- **Responsive Layout**: Adapts to container width

#### Usage Examples

**Email Statistics:**
```jsx
import StatBox from '../components/StatBox';
import EmailIcon from '@mui/icons-material/Email';
import { tokens } from '../theme';

function Dashboard() {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <StatBox
      title="12,361"
      subtitle="Emails Sent"
      progress="0.75"
      increase="+14%"
      icon={
        <EmailIcon
          sx={{ 
            color: colors.greenAccent[600], 
            fontSize: "26px" 
          }}
        />
      }
    />
  );
}
```

**Sales Statistics:**
```jsx
import PointOfSaleIcon from '@mui/icons-material/PointOfSale';

<StatBox
  title="431,225"
  subtitle="Sales Obtained"
  progress="0.50"
  increase="+21%"
  icon={
    <PointOfSaleIcon
      sx={{ 
        color: colors.greenAccent[600], 
        fontSize: "26px" 
      }}
    />
  }
/>
```

---

### ProgressCircle Component

**File:** `src/components/ProgressCircle.jsx`

A circular progress indicator using pure CSS gradients.

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `progress` | `string` | No | `"0.75"` | Progress value between 0 and 1 |
| `size` | `string` | No | `"40"` | Diameter in pixels |

#### Features

- **Pure CSS**: No external dependencies, uses conic gradients
- **Customizable Size**: Configurable diameter
- **Theme Integration**: Uses application color tokens
- **Performance**: Lightweight implementation
- **Smooth Animation**: CSS-based transitions

#### Usage Examples

**Default Progress Circle:**
```jsx
import ProgressCircle from '../components/ProgressCircle';

<ProgressCircle />  // 75% progress, 40px size
```

**Custom Progress and Size:**
```jsx
<ProgressCircle progress="0.65" size="60" />
```

**In StatBox Integration:**
```jsx
// Automatically integrated in StatBox component
<StatBox
  // ... other props
  progress="0.85"  // Passed to internal ProgressCircle
/>
```

#### CSS Implementation

```jsx
// Gradient calculation
const angle = progress * 360;

// Styling with conic gradient
sx={{
  background: `
    radial-gradient(${colors.primary[400]} 55%, transparent 56%),
    conic-gradient(
      transparent 0deg ${angle}deg, 
      ${colors.blueAccent[500]} ${angle}deg 360deg
    ),
    ${colors.greenAccent[500]}
  `,
  borderRadius: "50%",
  width: `${size}px`,
  height: `${size}px`,
}}
```

---

## Best Practices

### Component Usage Guidelines

1. **Consistent Theming**: Always use the `tokens` function for colors
2. **Responsive Design**: Consider `isDashboard` props for different layouts
3. **Accessibility**: Include proper ARIA labels and semantic HTML
4. **Performance**: Use React.memo for components that don't change frequently

### Example: Creating a Themed Component

```jsx
import { Box, useTheme } from '@mui/material';
import { tokens } from '../theme';

const MyComponent = ({ children, isDashboard = false }) => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <Box
      sx={{
        backgroundColor: colors.primary[400],
        borderRadius: '8px',
        padding: isDashboard ? '10px' : '20px',
        height: isDashboard ? '200px' : '400px'
      }}
    >
      {children}
    </Box>
  );
};

export default MyComponent;
```

### Data Integration Pattern

```jsx
// Custom hook for data fetching
const useChartData = () => {
  const [data, setData] = useState([]);
  
  useEffect(() => {
    // Replace with actual API call
    setData(mockBarData);
  }, []);
  
  return data;
};

// Usage in component
const MyChart = ({ isDashboard }) => {
  const data = useChartData();
  
  return (
    <ResponsiveBar
      data={data}
      // ... other props
    />
  );
};
```

This reference guide provides detailed information for implementing and customizing the chart and UI components in the portfolio dashboard application.