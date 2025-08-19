## Theme and Color Mode

Files:
- `src/theme.js`

### Exports
- `tokens(mode: "light" | "dark"): Record<string, Record<number, string>>`
  - Returns color design tokens for the given mode.
- `themeSettings(mode: "light" | "dark"): ThemeOptions`
  - Builds MUI theme options using tokens.
- `ColorModeContext: React.Context<{ toggleColorMode: () => void }>`
  - Context to toggle color mode.
- `useMode(): [Theme, { toggleColorMode: () => void }]`
  - React hook returning the current `theme` and `colorMode` controls.

### Usage
Wrap your app as in `src/App.js`:
```jsx
import { ColorModeContext, useMode } from "./theme";
import { CssBaseline, ThemeProvider } from "@mui/material";

function App() {
  const [theme, colorMode] = useMode();
  return (
    <ColorModeContext.Provider value={colorMode}>
      <ThemeProvider theme={theme}>
        <CssBaseline />
        {/* ...app layout... */}
      </ThemeProvider>
    </ColorModeContext.Provider>
  );
}
```

Toggle color mode from anywhere via context:
```jsx
import { useContext } from "react";
import { ColorModeContext } from "../theme";

const ToggleButton = () => {
  const colorMode = useContext(ColorModeContext);
  return <button onClick={colorMode.toggleColorMode}>Toggle mode</button>;
};
```

