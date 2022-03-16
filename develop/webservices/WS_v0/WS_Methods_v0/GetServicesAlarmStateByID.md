---
uid: GetServicesAlarmStateByID
---

# GetServicesAlarmStateByID

Use this method to request the current alarm state of a specific service (referenced by ID).

## Input

| Item       | Format  | Description                                   |
|------------|---------|-----------------------------------------------|
| Connection | String  | The connection ID. See [Connect](xref:Connect). |
| DmaID      | Integer | The DataMiner Agent ID.                       |
| ServiceID  | Integer | The service ID.                               |

## Output

| Item                             | Format | Description                                       |
|----------------------------------|--------|---------------------------------------------------|
| GetServicesAlarmStateBy­IDResult | String | The current alarm state of the specified service. |