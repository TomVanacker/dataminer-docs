---
uid: GetRedundancyGroupsLiteForView
---

# GetRedundancyGroupsLiteForView

Use this method to retrieve a list of all the redundancy groups from a specified view.

This method is a faster alternative to the method *GetRedundancyGroupsForView*, as it retrieves only basic information about the redundancy groups.

## Input

| Item            | Format  | Description                                                                      |
|-----------------|---------|----------------------------------------------------------------------------------|
| Connection      | String  | The connection ID. See [ConnectApp](xref:ConnectApp) . |
| ViewID          | Integer | The view ID.                                                                     |
| IncludeSubViews | Boolean | Indicates whether redundancy groups from subviews are included.                  |

## Output

| Item                                  | Format                                                                                     | Description                                  |
|---------------------------------------|--------------------------------------------------------------------------------------------|----------------------------------------------|
| GetRedundancyGroups­LiteForViewResult | Array of DMAElementLite (see [DMAElementLite](xref:DMAElementLite)) | The redundancy groups in the specified view. |
