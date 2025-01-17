---
uid: General_Main_Release_10.2.0_CU10
---

# General Main Release 10.2.0 CU10 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### DataMiner Cube - Visual Overview: Automatically generated shapes representing bookings can now be sorted by custom property [ID_34572]

<!-- MR 10.2.0 [CU10] - FR 10.3.1 -->

When specifying that a shape should be created automatically for each booking in a particular set of bookings, it is now possible to have the automatically generated shapes sorted by a custom booking property.

For example, in an SRM environment, you can have a booking time range that includes pre-roll and post-roll, and timings that contain the custom properties *Start* and *End*. From now on, it is possible to have the automatically generated shapes sorted by one of those custom properties. To do so, you can specify a shape data field of type *ChildrenSort* to the group-level shape and set its value to `Property|<CustomProperty>,<asc/desc>`.

Examples:

```txt
ChildrenSort="Property|Start,asc"
ChildrenSort="Property|End,desc"
```

#### DataMiner upgrade: Enhanced method to delete locked files [ID_34779]

<!-- MR 10.1.0 [CU22] / 10.2.0 [CU10] - FR 10.3.1 -->

When, during a DataMiner upgrade, an attempt was made to delete files that were locked by certain processes, up to now, that attempt would fail, causing those files to remain on the system until the next upgrade.

From now on, when an attempt to delete a file during a DataMiner upgrade fails, the extension of that file will be replaced by `.SLReplace` and, later on in the upgrade process, the file will then be deleted by SLHelper.

#### Size of log entries in log files generated by SLLog will now be limited [ID_34801]

<!-- MR 10.2.0 [CU10] - FR 10.3.1 -->

In log files generated by SLLog, the size of the entries will now be limited:

- Messages will be trimmed to 5120 characters.
- Methods will be trimmed to 200 characters.
- Program names will be trimmed to 200 characters.

> [!NOTE]
> Method data typically also includes the process and thread IDs.

### Fixes

#### Standalone parameters belonging to another child of the same DVE parent element could be set to 'Not Initialized' when a row linked to a DVE child element was deleted [ID_34785]

<!-- MR 10.1.0 [CU22] / 10.2.0 [CU10] - FR 10.3.1 -->

When a row linked to a DVE child element was deleted, in some cases, standalone parameters belonging to another child of the same DVE parent element could be set to "Not Initialized".
