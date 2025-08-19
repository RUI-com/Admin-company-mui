## Components

All components are React function components exported as default from their files in `src/components` or `src/scenes/*`.

### BarChart
- File: `src/components/BarChart.jsx`
- Export: default `BarChart`
- Props:
  - `isDashboard?: boolean` (default: `false`) — hides axis legends and adjusts layout when used in compact dashboard cards.
- Example:
```jsx
import BarChart from "../components/BarChart";

export default function SalesQuantityCard() {
  return (
    <div style={{ height: 250 }}>
      <BarChart isDashboard />
    </div>
  );
}
```

### LineChart
- File: `src/components/LineChart.jsx`
- Export: default `LineChart`
- Props:
  - `isCustomLineColors?: boolean` — when true, colors come from series `datum.color`.
  - `isDashboard?: boolean` (default: `false`) — compact axes and labels for dashboard usage.
- Example:
```jsx
import LineChart from "../components/LineChart";

export default function RevenueTrend() {
  return (
    <div style={{ height: 300 }}>
      <LineChart isDashboard />
    </div>
  );
}
```

### PieChart
- File: `src/components/PieChart.jsx`
- Export: default `PieChart`
- Props: none
- Example:
```jsx
import PieChart from "../components/PieChart";

export default function Breakdown() {
  return (
    <div style={{ height: 400 }}>
      <PieChart />
    </div>
  );
}
```

### GeographyChart
- File: `src/components/GeographyChart.jsx`
- Export: default `GeographyChart`
- Props:
  - `isDashboard?: boolean` (default: `false`) — uses compact projection and shows/hides legend.
- Example:
```jsx
import GeographyChart from "../components/GeographyChart";

export default function GeoTraffic() {
  return (
    <div style={{ height: 400 }}>
      <GeographyChart />
    </div>
  );
}
```

### Header
- File: `src/components/Header.jsx`
- Export: default `Header`
- Props:
  - `title: string`
  - `subtitle: string`
- Example:
```jsx
import Header from "../components/Header";

export default function PageHeader() {
  return <Header title="Team" subtitle="Manage teammates" />;
}
```

### ProgressCircle
- File: `src/components/ProgressCircle.jsx`
- Export: default `ProgressCircle`
- Props:
  - `progress?: number|string` (default: `"0.75"`) — 0..1 progress, used to compute conic gradient.
  - `size?: number|string` (default: `"40"`) — in pixels.
- Example:
```jsx
import ProgressCircle from "../components/ProgressCircle";

export default function KPI() {
  return <ProgressCircle progress={0.6} size={80} />;
}
```

### StatBox
- File: `src/components/StatBox.jsx`
- Export: default `StatBox`
- Props:
  - `title: string`
  - `subtitle: string`
  - `icon: ReactNode`
  - `progress: number|string` — forwarded to `ProgressCircle`.
  - `increase: string` — delta text (e.g., `"+12%"`).
- Example:
```jsx
import StatBox from "../components/StatBox";
import ShoppingCartIcon from "@mui/icons-material/ShoppingCart";

export default function SalesStat() {
  return (
    <StatBox
      title="431,225"
      subtitle="Sales Obtained"
      progress={0.5}
      increase="+21%"
      icon={<ShoppingCartIcon />}
    />
  );
}
```

### Layout Components

#### Sidebar
- File: `src/scenes/global/Sidebar.jsx`
- Export: default `Sidebar`
- Props: none (internal state manages collapse and active menu)
- Usage: Placed in `App` within `.app` layout; provides navigation links.

#### Topbar
- File: `src/scenes/global/Topbar.jsx`
- Export: default `Topbar`
- Props: none; uses `ColorModeContext` to toggle light/dark.

