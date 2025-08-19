## Mock Data and Shapes

Location: `src/data/`

### Exports from `mockData.js`
- `mockDataTeam: Array<{ id:number, name:string, email:string, age:number, phone:string, access:"admin"|"manager"|"user" }>`
- `mockDataContacts: Array<{ id:number, name:string, email:string, age:number, phone:string, address:string, city:string, zipCode:string, registrarId:number }>`
- `mockDataInvoices: Array<{ id:number, name:string, email:string, cost:string, phone:string, date:string }>`
- `mockTransactions: Array<{ txId:string, user:string, date:string, cost:string }>`
- `mockBarData: Array<{ country:string, "hot dog":number, burger:number, kebab:number, donut:number }>`
- `mockPieData: Array<{ id:string, label:string, value:number, color:string }>`
- `mockLineData: Array<{ id:string, color:string, data:Array<{ x:string, y:number }> }>`
- `mockGeographyData: Array<{ id:string, value:number }>` where `id` is ISO3 code

### Exports from `mockGeoFeatures.js`
- `geoFeatures: GeoJSON FeatureCollection` used by `@nivo/geo`.

### Usage Examples
```jsx
import { mockDataTeam } from "../data/mockData";
import { DataGrid } from "@mui/x-data-grid";

export default function TeamTable() {
  return <DataGrid rows={mockDataTeam} columns={[{ field: "id" }, { field: "name" }]} />;
}
```

