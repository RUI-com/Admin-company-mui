# Data Utilities & Mock Data Guide

## Overview

The application uses comprehensive mock data to simulate real-world data scenarios across all components and visualizations. This guide covers all available data sets, their structures, and usage patterns.

**Primary File:** `src/data/mockData.js`  
**Geographic Data:** `src/data/mockGeoFeatures.js`

---

## Data Sets

### Team Data

**Export:** `mockDataTeam`  
**Usage:** Team management scene, employee listings

#### Structure

```javascript
{
  id: number,           // Unique identifier
  name: string,         // Full name
  email: string,        // Email address
  age: number,          // Age in years
  phone: string,        // Phone number with formatting
  access: string        // Access level: "admin", "manager", "user"
}
```

#### Sample Data

```javascript
export const mockDataTeam = [
  {
    id: 1,
    name: "Jon Snow",
    email: "jonsnow@gmail.com", 
    age: 35,
    phone: "(665)121-5454",
    access: "admin"
  },
  {
    id: 2,
    name: "Cersei Lannister",
    email: "cerseilannister@gmail.com",
    age: 42,
    phone: "(421)314-2288", 
    access: "manager"
  }
  // ... 7 more entries
];
```

#### Usage Example

```javascript
import { mockDataTeam } from '../data/mockData';

const TeamGrid = () => {
  const columns = [
    { field: 'id', headerName: 'ID' },
    { field: 'name', headerName: 'Name', flex: 1 },
    { field: 'email', headerName: 'Email', flex: 1 },
    { field: 'age', headerName: 'Age', type: 'number' },
    { field: 'phone', headerName: 'Phone', flex: 1 },
    { field: 'access', headerName: 'Access Level', flex: 1 }
  ];

  return (
    <DataGrid
      rows={mockDataTeam}
      columns={columns}
      checkboxSelection
    />
  );
};
```

---

### Contacts Data

**Export:** `mockDataContacts`  
**Usage:** Contact management, customer information

#### Structure

```javascript
{
  id: number,           // Unique identifier
  name: string,         // Full name
  email: string,        // Email address
  age: number,          // Age in years
  phone: string,        // Phone number
  address: string,      // Street address
  city: string,         // City name
  zipCode: string,      // Postal code
  registrarId: number   // Registration ID
}
```

#### Sample Data

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
  // ... more entries
];
```

#### Usage Example

```javascript
import { mockDataContacts } from '../data/mockData';

const ContactsGrid = () => {
  return (
    <DataGrid
      rows={mockDataContacts}
      columns={contactColumns}
      pageSize={10}
      rowsPerPageOptions={[10, 25, 50]}
    />
  );
};
```

---

### Invoices Data

**Export:** `mockDataInvoices`  
**Usage:** Invoice management, financial tracking

#### Structure

```javascript
{
  id: number,           // Invoice ID
  name: string,         // Customer name
  email: string,        // Customer email
  cost: string,         // Invoice amount
  phone: string,        // Customer phone
  date: string          // Invoice date (YYYY-MM-DD)
}
```

#### Sample Data

```javascript
export const mockDataInvoices = [
  {
    id: 1,
    name: "Jon Snow",
    email: "jonsnow@gmail.com",
    cost: "21.24",
    phone: "(665)121-5454",
    date: "03/12/2022"
  }
  // ... more entries
];
```

#### Usage Example

```javascript
import { mockDataInvoices } from '../data/mockData';

const InvoicesGrid = () => {
  const columns = [
    { field: 'id', headerName: 'ID' },
    { field: 'name', headerName: 'Name', flex: 1 },
    { field: 'phone', headerName: 'Phone', flex: 1 },
    { field: 'email', headerName: 'Email', flex: 1 },
    { 
      field: 'cost', 
      headerName: 'Cost', 
      flex: 1,
      renderCell: (params) => (
        <Typography color={colors.greenAccent[500]}>
          ${params.row.cost}
        </Typography>
      )
    },
    { field: 'date', headerName: 'Date', flex: 1 }
  ];

  return <DataGrid rows={mockDataInvoices} columns={columns} />;
};
```

---

### Transactions Data

**Export:** `mockTransactions`  
**Usage:** Dashboard recent transactions, financial activity

#### Structure

```javascript
{
  txId: string,         // Transaction ID
  user: string,         // Username
  date: string,         // Transaction date (YYYY-MM-DD)
  cost: string          // Transaction amount
}
```

#### Sample Data

```javascript
export const mockTransactions = [
  {
    txId: "01e4dsa",
    user: "johndoe",
    date: "2021-09-01",
    cost: "43.95"
  },
  {
    txId: "0315dsaa", 
    user: "jackdower",
    date: "2022-04-01",
    cost: "133.45"
  }
  // ... more entries
];
```

#### Usage Example

```javascript
import { mockTransactions } from '../data/mockData';

const RecentTransactions = () => {
  return (
    <Box>
      {mockTransactions.map((transaction, i) => (
        <Box
          key={`${transaction.txId}-${i}`}
          display="flex"
          justifyContent="space-between"
          alignItems="center"
          borderBottom={`4px solid ${colors.primary[500]}`}
          p="15px"
        >
          <Box>
            <Typography 
              color={colors.greenAccent[500]}
              variant="h5"
              fontWeight="600"
            >
              {transaction.txId}
            </Typography>
            <Typography color={colors.grey[100]}>
              {transaction.user}
            </Typography>
          </Box>
          <Box color={colors.grey[100]}>
            {transaction.date}
          </Box>
          <Box
            backgroundColor={colors.greenAccent[500]}
            p="5px 10px"
            borderRadius="4px"
          >
            ${transaction.cost}
          </Box>
        </Box>
      ))}
    </Box>
  );
};
```

---

## Chart Data Sets

### Bar Chart Data

**Export:** `mockBarData`  
**Usage:** BarChart component, comparative analysis

#### Structure

```javascript
{
  country: string,      // Country code (e.g., "AD", "AE")
  "hot dog": number,    // Hot dog sales
  "hot dogColor": string, // Color for hot dog bars
  burger: number,       // Burger sales
  burgerColor: string,  // Color for burger bars
  sandwich: number,     // Sandwich sales
  sandwichColor: string, // Color for sandwich bars
  kebab: number,        // Kebab sales
  kebabColor: string,   // Color for kebab bars
  fries: number,        // Fries sales
  friesColor: string,   // Color for fries bars
  donut: number,        // Donut sales
  donutColor: string    // Color for donut bars
}
```

#### Sample Data

```javascript
export const mockBarData = [
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
];
```

#### Usage Example

```javascript
import { mockBarData } from '../data/mockData';
import { ResponsiveBar } from '@nivo/bar';

const BarChart = ({ isDashboard = false }) => {
  return (
    <ResponsiveBar
      data={mockBarData}
      keys={["hot dog", "burger", "sandwich", "kebab", "fries", "donut"]}
      indexBy="country"
      margin={{ top: 50, right: 130, bottom: 50, left: 60 }}
      padding={0.3}
      colors={{ scheme: "nivo" }}
      // ... other props
    />
  );
};
```

---

### Pie Chart Data

**Export:** `mockPieData`  
**Usage:** PieChart component, categorical breakdown

#### Structure

```javascript
{
  id: string,           // Category identifier
  label: string,        // Display label
  value: number,        // Numeric value
  color: string         // HSL color value
}
```

#### Sample Data

```javascript
export const mockPieData = [
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
  },
  {
    id: "go",
    label: "go", 
    value: 322,
    color: "hsl(291, 70%, 50%)"
  }
  // ... more categories
];
```

#### Usage Example

```javascript
import { mockPieData } from '../data/mockData';
import { ResponsivePie } from '@nivo/pie';

const PieChart = () => {
  return (
    <ResponsivePie
      data={mockPieData}
      margin={{ top: 40, right: 80, bottom: 80, left: 80 }}
      innerRadius={0.5}
      padAngle={0.7}
      cornerRadius={3}
      // ... other props
    />
  );
};
```

---

### Line Chart Data

**Export:** `mockLineData`  
**Usage:** LineChart component, trend analysis

#### Structure

```javascript
{
  id: string,           // Series identifier
  color: string,        // Line color (theme token)
  data: Array<{         // Data points array
    x: string,          // X-axis value
    y: number           // Y-axis value
  }>
}
```

#### Sample Data

```javascript
export const mockLineData = [
  {
    id: "japan",
    color: tokens("dark").greenAccent[500],
    data: [
      { x: "plane", y: 101 },
      { x: "helicopter", y: 75 },
      { x: "boat", y: 36 },
      { x: "train", y: 216 },
      { x: "subway", y: 35 },
      { x: "bus", y: 236 },
      { x: "car", y: 88 },
      { x: "moto", y: 232 },
      { x: "bicycle", y: 281 },
      { x: "horse", y: 1 },
      { x: "skateboard", y: 35 },
      { x: "others", y: 14 }
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
];
```

#### Usage Example

```javascript
import { mockLineData } from '../data/mockData';
import { ResponsiveLine } from '@nivo/line';

const LineChart = ({ isCustomLineColors = false, isDashboard = false }) => {
  return (
    <ResponsiveLine
      data={mockLineData}
      margin={{ top: 50, right: 110, bottom: 50, left: 60 }}
      xScale={{ type: 'point' }}
      yScale={{ 
        type: 'linear', 
        min: 'auto', 
        max: 'auto', 
        stacked: true, 
        reverse: false 
      }}
      curve="catmullRom"
      // ... other props
    />
  );
};
```

---

### Geography Data

**Export:** `mockGeographyData`  
**Usage:** GeographyChart component, world map visualization

#### Structure

```javascript
{
  id: string,           // Country code
  value: number         // Numeric value for visualization
}
```

#### Sample Data

```javascript
export const mockGeographyData = [
  { id: "AFG", value: 520600 },
  { id: "AGO", value: 949905 },
  { id: "ALB", value: 329910 },
  { id: "ARE", value: 675484 },
  { id: "ARG", value: 432239 }
  // ... more countries
];
```

#### Usage with Geographic Features

```javascript
import { mockGeographyData } from '../data/mockData';
import { mockGeoFeatures } from '../data/mockGeoFeatures';
import { ResponsiveChoropleth } from '@nivo/geo';

const GeographyChart = ({ isDashboard = false }) => {
  return (
    <ResponsiveChoropleth
      data={mockGeographyData}
      features={mockGeoFeatures.features}
      margin={{ top: 0, right: 0, bottom: 0, left: 0 }}
      domain={[0, 1000000]}
      unknownColor="#666666"
      label="properties.NAME"
      valueFormat=".2s"
      // ... other props
    />
  );
};
```

---

## Geographic Features Data

**File:** `src/data/mockGeoFeatures.js`  
**Export:** `mockGeoFeatures`  
**Usage:** World map boundaries and country shapes

### Structure

```javascript
{
  type: "FeatureCollection",
  features: Array<{
    type: "Feature",
    properties: {
      NAME: string,       // Country name
      // ... other geographic properties
    },
    geometry: {
      type: "Polygon" | "MultiPolygon",
      coordinates: Array  // Geographic coordinates
    }
  }>
}
```

### Usage Example

```javascript
import { mockGeoFeatures } from '../data/mockGeoFeatures';

// Used internally by GeographyChart component
const features = mockGeoFeatures.features;
```

---

## Data Integration Patterns

### Custom Data Hook

```javascript
import { useState, useEffect } from 'react';
import { mockDataTeam } from '../data/mockData';

export const useTeamData = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulate API call delay
    const timer = setTimeout(() => {
      setData(mockDataTeam);
      setLoading(false);
    }, 500);

    return () => clearTimeout(timer);
  }, []);

  return { data, loading };
};
```

### Data Filtering

```javascript
import { mockDataTeam } from '../data/mockData';

const useFilteredTeam = (accessLevel) => {
  return useMemo(() => {
    if (!accessLevel) return mockDataTeam;
    return mockDataTeam.filter(member => member.access === accessLevel);
  }, [accessLevel]);
};

// Usage
const adminMembers = useFilteredTeam('admin');
const managerMembers = useFilteredTeam('manager');
```

### Data Transformation

```javascript
import { mockTransactions } from '../data/mockData';

const useTransactionSummary = () => {
  return useMemo(() => {
    const totalCost = mockTransactions.reduce(
      (sum, transaction) => sum + parseFloat(transaction.cost), 
      0
    );
    
    const transactionCount = mockTransactions.length;
    
    const averageCost = totalCost / transactionCount;

    return {
      totalCost: totalCost.toFixed(2),
      transactionCount,
      averageCost: averageCost.toFixed(2)
    };
  }, []);
};
```

### Data Validation

```javascript
import * as yup from 'yup';

// Validation schema for team data
export const teamMemberSchema = yup.object().shape({
  id: yup.number().required('ID is required'),
  name: yup.string().required('Name is required'),
  email: yup.string().email('Invalid email').required('Email is required'),
  age: yup.number().min(18, 'Must be at least 18').required('Age is required'),
  phone: yup.string().required('Phone is required'),
  access: yup.string().oneOf(['admin', 'manager', 'user']).required('Access level is required')
});

// Usage
const validateTeamMember = async (data) => {
  try {
    await teamMemberSchema.validate(data);
    return { isValid: true, errors: null };
  } catch (error) {
    return { isValid: false, errors: error.errors };
  }
};
```

---

## Best Practices

### Data Usage Guidelines

1. **Consistent Structure**: Maintain consistent data structures across similar components
2. **Type Safety**: Use TypeScript interfaces for better type checking
3. **Performance**: Use React.memo and useMemo for expensive data transformations
4. **Validation**: Always validate data before using in components
5. **Error Handling**: Implement proper error handling for data operations

### Example: Type-Safe Data Usage

```typescript
// types.ts
interface TeamMember {
  id: number;
  name: string;
  email: string;
  age: number;
  phone: string;
  access: 'admin' | 'manager' | 'user';
}

interface Transaction {
  txId: string;
  user: string;
  date: string;
  cost: string;
}

// Component usage
const TeamGrid: React.FC = () => {
  const [teamData, setTeamData] = useState<TeamMember[]>([]);
  
  useEffect(() => {
    setTeamData(mockDataTeam);
  }, []);

  return (
    <DataGrid
      rows={teamData}
      columns={teamColumns}
    />
  );
};
```

### Data Migration Pattern

```javascript
// For transitioning from mock data to real API
const useDataSource = (useMockData = true) => {
  if (useMockData) {
    return {
      teamData: mockDataTeam,
      contactsData: mockDataContacts,
      transactionsData: mockTransactions
    };
  } else {
    // Return API data
    return {
      teamData: apiTeamData,
      contactsData: apiContactsData, 
      transactionsData: apiTransactionsData
    };
  }
};
```

This comprehensive guide covers all data utilities and mock data sets available in the portfolio dashboard application, providing complete information for data integration and usage patterns.