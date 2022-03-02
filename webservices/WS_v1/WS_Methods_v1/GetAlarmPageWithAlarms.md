---
uid: GetAlarmPageWithAlarms
---

# GetAlarmPageWithAlarms

Use this method to retrieve alarm page details, including limited alarms. This method combines the functionality of the GetAlarmPages and GetAlarms methods, so that the actual alarms only need to be fetched once.

## Input

| Item             | Format | Description                                                                                                  |
|------------------|--------|--------------------------------------------------------------------------------------------------------------|
| Connection       | String | The connection ID. See [ConnectApp](xref:ConnectApp) .                                                         |
| DMAAlarmFilterV2 | Array  | The filter that the alarms must match. See [DMAAlarmFilterV2](xref:DMAAlarmFilterV2). |

## Output

| Item                          | Format                                                                   | Description                                |
|-------------------------------|--------------------------------------------------------------------------|--------------------------------------------|
| GetAlarmPageWith­AlarmsResult | Array of DMAAlarm (see [DMAAlarm](xref:DMAAlarm)) | The alarms matching the filter on the page |
