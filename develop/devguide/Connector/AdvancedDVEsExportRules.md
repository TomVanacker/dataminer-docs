---
uid: AdvancedDVEsExportRules
---

# Export rules

Export rules allow you to change the properties of exported parameters, e.g. the position of the parameter in the DVE. An export rule overwrites a declaration in the parent element.

```xml
<ExportRule table="" tag=" " attribute="" value=""/>
```

- **table**: ID of the DVE table or an asterisk (“*”) in case the rule should be applied to all dynamic element types.
- **tag**: The tag to overrule. The full path of the tag needs to be specified: starting from the root tag, each child tag in the path must be included and separated with a forward slash (“/”).
- **attribute**: In case an attribute should be modified, specify the name of the attribute here.
- **value**: New value that will be used in the DVE protocol.

There is no restriction on the number of export rules that can be defined. Note, however, that the export rules are evaluated sequentially. For example, if there are two export rules that set the default page for a DVE protocol, the default page setting of the last export rule will be applied, as this rule will be processed last.

From DataMiner version 7.5.6.3 onwards, it is possible to use regular expressions in export rules, making it possible to define more complex export rules.

|Symbol|Meaning|
|--- |--- |
|.|A single character.|
|\\d|Matches a digit [0-9].|
|\\w|Matches an alphanumeric character.|
|\\ |Used to escape special characters. For example, \\. matches a dot and \\\\ matches a backslash.|
|^|Match at the beginning of the input string.|
|$|Match at the end of the input string.|

From DataMiner 8.5.1 onwards (RN 7831), hidden DVE tables (i.e. tables with RTDisplay="false"), can be exported using an export rule. In other words, a table not displayed in the DVE “parent” element can be visible in the DVE “child” element.

## Examples

- The following export sets the default page of all DVE protocols generated by this protocol to "Task Manager":

    ```xml
    <ExportRule table="*" tag="Protocol/Display" attribute="defaultPage" value="Task Manager"/>
    ```

    To set the default page of all exported protocols to "Task Manager" and define the page order depending the DVE source table:

    ```xml
    <ExportRule table="*" tag="Protocol/Display" attribute="defaultPage" value="Task Manager"/>
    <ExportRule table="100" tag="Protocol/Display" attribute="pageOrder" value="Task Manager;Disk Info"/>
    <ExportRule table="200" tag="Protocol/Display" attribute="pageOrder" value="Task Manager;Process Info"/>
    ```

    As export rules are processed in sequence, this means you can also define to set all default pages to Task Manager, except for exported table 200 as follows:

    ```xml
    <ExportRule table="*" tag="Protocol/Display" attribute="defaultPage" value="Task Manager"/>
    <ExportRule table="200" tag="Protocol/Display" attribute="defaultPage" value="Disk Info"/>
    ```

    However, the result below sets all defaultPages to 'Task Manager', since table '*' is the last rule.

    ```xml
    <ExportRule table="100" tag="Protocol/Display" attribute="defaultPage" value="Disk Info"/>
    <ExportRule table="*" tag="Protocol/Display" attribute="defaultPage" value="Task Manager"/>
    ```

- It is also possible to define an export rule to adjust the RTDisplay setting of parameters.

    The following export rule shows the webpage on the DVE (Parameter 211 is a column parameter containing the IP addresses and table 200 is linked to table 4000):

    ```xml
    <ExportRule table="4000" tag="Protocol/Display" attribute="pageOrder" value="General;Input/Output;Webpage#http://[id:211]"/>
    ```

- The following examples make use of regular expressions.

    To remove a specific string in the parameter names, the following configuration can be used:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="MCR"/>
    ```

    Or we could specify to do this only when the string is a prefix:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="^MCR"/>
    ```

    Or when the string is a suffix:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="MCR$"/>
    ```

    We do not have to remove it; we could also replace it by another prefix:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="PBR" regex="MCR$"/>
    ```

    It could also be that the string you want to remove is not consistent. In this case, regular expressions are very useful. For example, if you want to remove the prefix in the protocol names, but the prefix could be trailing by 4, 7 or 8, you can specify the following to remove “MCR” with each digit behind it:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="MCR\n"/>
    ```

    Or we could be more precise:

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="MCR[478]"/>
    ```

    Another thing that we could do is remove each prefix of 3 capital letters followed by a space except if the prefix is 'MCR':

    ```xml
    <ExportRule table="*" tag="Protocol/Params/Param/Name" value="" regex="(^[A-Z]{3} )(?!MCR )"/>
    ```

    Here we specify: match 3 capital letters at the beginning of the string followed by a space (a space gets interpreted as well), but do not match when these 3 letters are MCR.

> [!NOTE]
> This could also be combined with the whereTag and whereValue attribute. For example, to change the column to 2 if the parameter name is 'My param' and if the column is not containing more than two digits. (This example is just by way of illustration, as it is very unlikely that this would be used in a production environment).
>
> ```xml
> <ExportRule table="*" tag="Protocol/Params/Param/Display/Positions/Position/Column" value="2" regex="\d{2}" whereTag="Protocol/Params/Param/Name" whereValue="My param"/>
> ```