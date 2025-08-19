# Theme System & Layout Components Guide

## Theme System

### Overview

The application uses a comprehensive theming system built on Material-UI's theming capabilities with custom color tokens and dark/light mode support.

**File:** `src/theme.js`

### Color Token System

The `tokens` function generates color palettes based on the current theme mode (dark/light).

#### Usage

```javascript
import { tokens } from '../theme';
import { useTheme } from '@mui/material';

const MyComponent = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  
  return (
    <Box sx={{ backgroundColor: colors.primary[400] }}>
      Content
    </Box>
  );
};
```

#### Color Palettes

**Grey Palette**
```javascript
// Dark Mode
grey: {
  100: "#e0e0e0",  // Lightest
  200: "#c2c2c2",
  300: "#a3a3a3", 
  400: "#858585",
  500: "#666666",  // Mid-tone
  600: "#525252",
  700: "#3d3d3d",
  800: "#292929", 
  900: "#141414"   // Darkest
}

// Light Mode (inverted)
grey: {
  100: "#141414",  // Darkest becomes lightest
  200: "#292929",
  // ... inverted values
  900: "#e0e0e0"   // Lightest becomes darkest
}
```

**Primary Palette**
```javascript
// Dark Mode
primary: {
  100: "#d0d1d5",
  200: "#a1a4ab", 
  300: "#727681",
  400: "#1F2A40",  // Common background color
  500: "#141b2d",  // Main primary
  600: "#101624",
  700: "#0c101b",
  800: "#080b12",
  900: "#040509"
}
```

**Accent Palettes**
```javascript
// Green Accent (consistent across modes)
greenAccent: {
  100: "#dbf5ee",
  200: "#b7ebde",
  300: "#94e2cd", 
  400: "#70d8bd",
  500: "#4cceac",  // Primary green
  600: "#3da58a",
  700: "#2e7c67",
  800: "#1e5245", 
  900: "#0f2922"
}

// Red Accent
redAccent: {
  100: "#f8dcdb",
  200: "#f1b9b7",
  300: "#e99592",
  400: "#e2726e", 
  500: "#db4f4a",  // Primary red
  600: "#af3f3b",
  700: "#832f2c",
  800: "#58201e",
  900: "#2c100f"
}

// Blue Accent
blueAccent: {
  100: "#e1e2fe",
  200: "#c3c6fd", 
  300: "#a4a9fc",
  400: "#868dfb",
  500: "#6870fa",  // Primary blue
  600: "#535ac8",
  700: "#3e4396", 
  800: "#2a2d64",
  900: "#151632"
}
```

### Theme Configuration

#### Material-UI Theme Settings

```javascript
const themeSettings = (mode) => {
  const colors = tokens(mode);
  
  return {
    palette: {
      mode: mode,
      ...(mode === 'dark'
        ? {
            // Dark mode palette
            primary: { main: colors.primary[500] },
            secondary: { main: colors.greenAccent[500] },
            neutral: {
              dark: colors.grey[700],
              main: colors.grey[500], 
              light: colors.grey[100]
            },
            background: { default: colors.primary[500] }
          }
        : {
            // Light mode palette  
            primary: { main: colors.primary[100] },
            secondary: { main: colors.greenAccent[500] },
            neutral: {
              dark: colors.grey[700],
              main: colors.grey[500],
              light: colors.grey[100] 
            },
            background: { default: "#fcfcfc" }
          })
    },
    typography: {
      fontFamily: ["Source Sans Pro", "sans-serif"].join(","),
      fontSize: 12,
      h1: { fontSize: 40 },
      h2: { fontSize: 32 },
      h3: { fontSize: 24 },
      h4: { fontSize: 20 },
      h5: { fontSize: 16 },
      h6: { fontSize: 14 }
    }
  };
};
```

### Theme Context & Hook

#### ColorModeContext

```javascript
export const ColorModeContext = createContext({
  toggleColorMode: () => {}
});
```

#### useMode Hook

```javascript
export const useMode = () => {
  const [mode, setMode] = useState("dark");

  const colorMode = useMemo(
    () => ({
      toggleColorMode: () =>
        setMode((prev) => (prev === "light" ? "dark" : "light"))
    }),
    []
  );

  const theme = useMemo(() => createTheme(themeSettings(mode)), [mode]);
  return [theme, colorMode];
};
```

#### Implementation in App

```javascript
import { ColorModeContext, useMode } from './theme';
import { ThemeProvider } from '@mui/material';

function App() {
  const [theme, colorMode] = useMode();
  
  return (
    <ColorModeContext.Provider value={colorMode}>
      <ThemeProvider theme={theme}>
        <CssBaseline />
        {/* App content */}
      </ThemeProvider>
    </ColorModeContext.Provider>
  );
}
```

---

## Layout Components

### Sidebar Component

**File:** `src/scenes/global/Sidebar.jsx`

A collapsible navigation sidebar with user profile and menu items.

#### Features

- **Collapsible Design**: Toggle between expanded/collapsed states
- **Navigation Integration**: React Router DOM integration
- **User Profile Section**: Avatar and user information display
- **Icon-based Menu**: Material-UI icons for each menu item
- **Theme Awareness**: Adapts to current theme mode
- **Selection State**: Highlights currently selected menu item

#### Props

No props required - manages internal state.

#### Menu Structure

```javascript
const menuItems = [
  // Data Section
  { title: "Dashboard", to: "/", icon: <HomeOutlinedIcon /> },
  { title: "Manage Team", to: "/team", icon: <PeopleOutlinedIcon /> },
  { title: "Contacts Information", to: "/contacts", icon: <ContactsOutlinedIcon /> },
  { title: "Invoices Balances", to: "/invoices", icon: <ReceiptOutlinedIcon /> },
  
  // Pages Section  
  { title: "Profile Form", to: "/form", icon: <PersonOutlinedIcon /> },
  { title: "Calendar", to: "/calendar", icon: <CalendarTodayOutlinedIcon /> },
  { title: "FAQ Page", to: "/faq", icon: <HelpOutlineOutlinedIcon /> },
  
  // Charts Section
  { title: "Bar Chart", to: "/bar", icon: <BarChartOutlinedIcon /> },
  { title: "Pie Chart", to: "/pie", icon: <PieChartOutlineOutlinedIcon /> },
  { title: "Line Chart", to: "/line", icon: <TimelineOutlinedIcon /> },
  { title: "Geography Chart", to: "/geography", icon: <MapOutlinedIcon /> }
];
```

#### Internal Components

**Item Component**
```javascript
const Item = ({ title, to, icon, selected, setSelected }) => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  
  return (
    <MenuItem
      active={selected === title}
      style={{ color: colors.grey[100] }}
      onClick={() => setSelected(title)}
      icon={icon}
    >
      <Typography>{title}</Typography>
      <Link to={to} />
    </MenuItem>
  );
};
```

#### State Management

```javascript
const Sidebar = () => {
  const [isCollapsed, setIsCollapsed] = useState(true);
  const [selected, setSelected] = useState("Dashboard");
  
  // Component implementation
};
```

#### Styling Configuration

```javascript
sx={{
  "& .pro-sidebar-inner": {
    background: `${colors.primary[400]} !important`
  },
  "& .pro-icon-wrapper": {
    backgroundColor: "transparent !important"
  },
  "& .pro-inner-item": {
    padding: "5px 35px 5px 20px !important"
  },
  "& .pro-inner-item:hover": {
    color: "#868dfb !important"
  },
  "& .pro-menu-item.active": {
    color: "#6870fa !important"
  }
}}
```

#### Usage Example

```javascript
import Sidebar from '../scenes/global/Sidebar';

function Layout() {
  return (
    <div className="app">
      <Sidebar />
      <main className="content">
        {/* Page content */}
      </main>
    </div>
  );
}
```

---

### Topbar Component

**File:** `src/scenes/global/Topbar.jsx`

Top navigation bar with search functionality and utility buttons.

#### Features

- **Search Bar**: Input field with search icon
- **Theme Toggle**: Switch between light/dark modes
- **Utility Buttons**: Notifications, settings, profile access
- **Responsive Design**: Adapts to screen size
- **Theme Integration**: Uses color tokens

#### Components

**Search Bar**
```javascript
<Box
  display="flex"
  backgroundColor={colors.primary[400]}
  borderRadius="3px"
>
  <InputBase 
    sx={{ ml: 2, flex: 1 }} 
    placeholder="Search" 
  />
  <IconButton type="button" sx={{ p: 1 }}>
    <SearchIcon />
  </IconButton>
</Box>
```

**Theme Toggle Button**
```javascript
<IconButton onClick={colorMode.toggleColorMode}>
  {theme.palette.mode === "dark" ? (
    <DarkModeOutlinedIcon />
  ) : (
    <LightModeOutlinedIcon />
  )}
</IconButton>
```

**Utility Buttons**
```javascript
<Box display="flex">
  {/* Theme toggle */}
  <IconButton onClick={colorMode.toggleColorMode}>
    {/* Theme icon */}
  </IconButton>
  
  {/* Notifications */}
  <IconButton>
    <NotificationsOutlinedIcon />
  </IconButton>
  
  {/* Settings */}
  <IconButton>
    <SettingsOutlinedIcon />
  </IconButton>
  
  {/* Profile */}
  <IconButton>
    <PersonOutlinedIcon />
  </IconButton>
</Box>
```

#### Context Usage

```javascript
import { useContext } from 'react';
import { ColorModeContext } from '../../theme';

const Topbar = () => {
  const colorMode = useContext(ColorModeContext);
  
  // Component implementation
};
```

#### Usage Example

```javascript
import Topbar from '../scenes/global/Topbar';

function Layout() {
  return (
    <div className="app">
      <Sidebar />
      <main className="content">
        <Topbar />
        {/* Page content */}
      </main>
    </div>
  );
}
```

---

## Layout Patterns

### Application Layout Structure

```javascript
// App.js structure
function App() {
  const [theme, colorMode] = useMode();
  
  return (
    <ColorModeContext.Provider value={colorMode}>
      <ThemeProvider theme={theme}>
        <CssBaseline />
        <div className='app'>
          <Sidebar />
          <main className="content">
            <Topbar />
            <Routes>
              {/* Route definitions */}
            </Routes>
          </main>
        </div>
      </ThemeProvider>
    </ColorModeContext.Provider>
  );
}
```

### CSS Layout Classes

```css
/* index.css */
.app {
  display: flex;
  position: relative;
}

.content {
  flex-grow: 1;
  padding: 0;
}
```

### Page Layout Pattern

```javascript
const PageComponent = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <Box m="20px">
      {/* Standard page header */}
      <Header title="Page Title" subtitle="Page Description" />
      
      {/* Page content with theme-aware styling */}
      <Box
        backgroundColor={colors.primary[400]}
        borderRadius="8px"
        padding="20px"
      >
        {/* Page-specific content */}
      </Box>
    </Box>
  );
};
```

---

## Theme Customization

### Adding New Color Palettes

```javascript
// In tokens function
export const tokens = (mode) => ({
  // Existing palettes...
  
  // New custom palette
  customAccent: {
    100: "#e8f5e8",
    200: "#c8e6c9", 
    300: "#a5d6a7",
    400: "#81c784",
    500: "#66bb6a",  // Primary custom color
    600: "#4caf50",
    700: "#388e3c",
    800: "#2e7d32",
    900: "#1b5e20"
  }
});
```

### Custom Component Theming

```javascript
const CustomComponent = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  return (
    <Box
      sx={{
        backgroundColor: colors.primary[400],
        color: colors.grey[100],
        borderRadius: '8px',
        padding: '16px',
        '&:hover': {
          backgroundColor: colors.primary[300]
        }
      }}
    >
      Custom themed content
    </Box>
  );
};
```

### Responsive Theme Usage

```javascript
import { useMediaQuery } from '@mui/material';

const ResponsiveComponent = () => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);
  const isMobile = useMediaQuery(theme.breakpoints.down('md'));

  return (
    <Box
      sx={{
        backgroundColor: colors.primary[400],
        padding: isMobile ? '10px' : '20px',
        fontSize: isMobile ? '14px' : '16px'
      }}
    >
      Responsive content
    </Box>
  );
};
```

---

## Best Practices

### Theme Usage Guidelines

1. **Always use color tokens**: Never hardcode colors
2. **Consistent spacing**: Use Material-UI spacing system
3. **Responsive design**: Consider mobile-first approach
4. **Accessibility**: Ensure proper contrast ratios
5. **Performance**: Use useMemo for expensive theme calculations

### Example: Proper Theme Implementation

```javascript
import { useTheme, Box, Typography } from '@mui/material';
import { tokens } from '../theme';

const ThemedComponent = ({ children, variant = "default" }) => {
  const theme = useTheme();
  const colors = tokens(theme.palette.mode);

  const getVariantStyles = () => {
    switch (variant) {
      case "primary":
        return {
          backgroundColor: colors.primary[400],
          color: colors.grey[100]
        };
      case "accent":
        return {
          backgroundColor: colors.greenAccent[500],
          color: colors.grey[900]
        };
      default:
        return {
          backgroundColor: colors.grey[100],
          color: colors.grey[900]
        };
    }
  };

  return (
    <Box
      sx={{
        ...getVariantStyles(),
        borderRadius: '8px',
        padding: theme.spacing(2),
        margin: theme.spacing(1)
      }}
    >
      {children}
    </Box>
  );
};
```

This comprehensive guide covers the theme system and layout components, providing everything needed to understand and extend the application's theming and layout capabilities.