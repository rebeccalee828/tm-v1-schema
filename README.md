# Preview
- Please note that these documents are still in preview stage and we do not guarantee any backward compatibility.

# Background
- These documents provide Trend Micro Vision One log schema details.

# User scenario
- Currently, these documents only support the following use cases:
    1. Support Trend Micro Vision One Search app UI usage

# Property Description
| Property       | Description                                    |
|----------------|------------------------------------------------|
| Name           | Field name of log                              |
| ProductCode    | Products which sends data to this field        |
| Description_EN | Description of this field                      |
| Sample         | Sample value of these field                    |
| DL_Searchable  | If log is searchable by this field             |
| DL_Type        | Data type of this field                        |
| DL_CommonKey   | The corresponding field name in General Search |

# ProductCode Mapping
| Code | Product                                        |
|------|------------------------------------------------|
| ALL  | All products                                   |
| pdi  | Trend Micro Deep Discovery Inspector           |
| sds  | Trend Cloud One - Endpoint & Workload Security |
| xes  | Endpoint Sensor                                |
| sao  | Trend Micro Apex One as a Service              |
| pds  | Trend Micro Deep Security Software             |
| sca  | Trend Micro Cloud App Security                 |
| ptp  | TippingPoint Security Management System        |
| stp  | Trend Cloud One - Network Security             |
| scs  | Trend Cloud One - Container Security           |
| sct  | Trend Cloud One - AWS CloudTrail Integration   |
| sig  | Zero Trust Secure Access - Internet Access     |
| szn  | Zero Trust Secure Access - Private Access      |
| sws  | Trend Micro Web Security                       |
| sem  | Trend Micro Email Security                     |
| ams  | Mobile Security                                |
| pts  | TXOne Stellar                                  |
| ptn  | TXOne EdgeOne                                  |

# Search Syntax
## Search Syntax: Simple Search
To perform a simple search, you must enclose your search string in double quotation marks ("").

| Search Target                     | Description                                                                                                                               | Syntax                                       | Example                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Partial match                     | Provides all results that contain the search string in any data field                                                                     | `"search_string"`                            | `"john"` <br/>Returns all results that contain the string "john" in any data field                                                                                                                                                                                                                                                  |
| Full match                        | Not available                                                                                                                             | -                                            | -                                                                                                                                                                                                                                                                                                                                   |
| Logical operator: Multiple fields | Provides all results that match the requirements specified for multiple fields using the following operators:<li>AND<li>OR<li>NOT         | `"search_string1" OPERATOR "search_string2"` | `"john_doe" AND "credit"` <br/>Only returns results in which the log data contains both "john_doe" and "credit" in any field (example: objectUser=john_doe2; fileName=creditcard.txt) <br/>`"john_doe" AND NOT "home"` <br/>Only returns results in which the log data contains "john_doe" but does not contain "home" in any field |
| Range operator: Integers          | Provides all results that match the requirements specified for multiple fields using the following operators:<br/><li>><li><<li>>= <li><= | -                                            | `"dpt >= 80" AND "dpt <= 443"` <br/>Only returns results in which the log data contains integers in a range from greater than or equal to 80 to less than or equal to 443                                                                                                                                                           |

When using the Simple Search method, take note of the following limitations:
* Ensure that the use of the space character exactly matches the results that you want. A double space within the search string omits any results that only include one space character in the same location.
* The performance of the search decreases when using multiple logical operators.
* Some search fields display substituted text for ID values and you cannot search for the text value. For example, "eventID" stores the numerical value "1" in the database but displays "TELEMETRY_PROCESS" in the search results. You cannot search for "TELEMETRY_PROCESS".

## Search Syntax: Complex Queries
The following table outlines different search syntax and provides example strings.

| Search Target                         | Description                                                                                                                                                                                                        | Syntax                                                                 | Example                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Partial match                         | Provides all results for the specified field that contain the search string                                                                                                                                        | `<field_name>: <search_string>`                                        | `endpointName: windows` <br/>Returns all results that contain "windows" in the endpoint name                                                                                                                                                                                                                                                                                                   |
| Full match                            | Provides all results for the specified field that contain the exact search string specified                                                                                                                        | `<field_name>: "<search_string>"`                                      | `endpointName: "john_doe"` <br\>Only returns results in which the endpoint name is "john_doe"                                                                                                                                                                                                                                                                                                  |
| Logical operator: Multiple fields     | Provides all results that match the requirements specified for multiple fields using the following operators:<li>AND<li>OR<li>NOT                                                                                  | `<field_name>: <search_string> OPERATOR <field_name>: <search_string>` | `endpointName: "john_doe" AND fileName: credit` <br/>Only returns results in which the endpoint name is "john_doe" and the file name related to the detection contains the text "credit" <br/>`endpointName: "john_doe" AND NOT fileName: home` <br/>Only returns results in which the endpoint name is "john_doe" and the file name related to the detection does not contain the text "home" |
| Logical operator: Multiple values     | Provides all results that match the requirements specified for multiple values in the same field using the following operators:<li>AND<li>OR<li>NOT                                                                | `<field_name>: (<search_string> OPERATOR <search_string>)`             | `endpointName: ("john_doe" OR "jane_doe")` <br/>Returns results in which the endpoint name is "john_doe" or "jane_doe"                                                                                                                                                                                                                                                                         |
| Wildcard usage                        | Provides results that match the field values substituting for the following wildcard characters:<li>*: Used as a substitute for one or more characters in the specified location                                   | `<field_name>: <search_string>*`                                       | `endpointName: "john*"` <br/>Returns all results that contain "john" as the first 4 characters in the endpoint name <br/>Example results: "john", "john_doe"", "johndoe", "johnd"                                                                                                                                                                                                              |
| Null values                           | Provides results in which the corresponding field value is NULL                                                                                                                                                    | `<field_name>: null`                                                   | `fileName: null` <br/>Returns all results in which the fileName value does not exist                                                                                                                                                                                                                                                                                                           |
| Special characters / Escape character | When a search string includes a double quote (") or backslash (\\), you must use the backslash escape character "\\" to indicate that the special character is part of the search criteria and not special markup. | `<field_name>: "\<"or\><search_string>"`                               | `fullFilePath: "C:\\notepad\\tmp.txt"` <br/>Returns all results in which the fullFilePath value is exactly:<br/>`C:\notepad\tmp.txt`                                                                                                                                                                                                                                                           |

<b>Important:</b>
* Wildcard usage not supported with these data types:
  * Network Activity Data: IP addresses
* Special characters / Escape character: Partial matching not supported.

# EventId, EventSubId Mapping
## Endpoint Activity Data
### eventId
| eventId | Data Field Mapping         |
| ------- | -------------------------- |
| 1       | TELEMETRY_PROCESS          |
| 2       | TELEMETRY_FILE             |
| 3       | TELEMETRY_CONNECTION       |
| 4       | TELEMETRY_DNS              |
| 5       | TELEMETRY_REGISTRY         |
| 6       | TELEMETRY_ACCOUNT          |
| 7       | TELEMETRY_INTERNET         |
| 8       | TELEMETRY_MODIFIED_PROCESS |
| 9       | TELEMETRY_WINDOWS_HOOK     |
| 10      | TELEMETRY_WINDOWS_EVENT    |
| 11      | TELEMETRY_AMSI             |
| 12      | TELEMETRY_WMI              |
| 13      | TELEMETRY_MEMORY           |
| 14      | TELEMETRY_BM               |

### eventSubId
| eventSubId | Data Field Mapping                             |
| ---------- | ---------------------------------------------- |
| 1          | TELEMETRY_PROCESS_OPEN                         |
| 2          | TELEMETRY_PROCESS_CREATE                       |
| 3          | TELEMETRY_PROCESS_TERMINATE                    |
| 4          | TELEMETRY_PROCESS_LOAD_IMAGE                   |
| 5          | TELEMETRY_PROCESS_EXECUTE                      |
| 6          | TELEMETRY_PROCESS_CONNECT                      |
| 7          | TELEMETRY_PROCESS_TRACME                       |
| 101        | TELEMETRY_FILE_CREATE                          |
| 102        | TELEMETRY_FILE_OPEN                            |
| 103        | TELEMETRY_FILE_DELETE                          |
| 104        | TELEMETRY_FILE_SET_SECURITY                    |
| 105        | TELEMETRY_FILE_COPY                            |
| 106        | TELEMETRY_FILE_MOVE                            |
| 107        | TELEMETRY_FILE_CLOSE                           |
| 108        | TELEMETRY_FILE_MODIFY_TIMESTAMP                |
| 109        | TELEMETRY_FILE_MODIFY                          |
| 201        | TELEMETRY_CONNECTION_CONNECT                   |
| 202        | TELEMETRY_CONNECTION_LISTEN                    |
| 203        | TELEMETRY_CONNECTION_CONNECT_INBOUND           |
| 204        | TELEMETRY_CONNECTION_CONNECT_OUTBOUND          |
| 301        | TELEMETRY_DNS_QUERY                            |
| 401        | TELEMETRY_REGISTRY_CREATE                      |
| 402        | TELEMETRY_REGISTRY_SET                         |
| 403        | TELEMETRY_REGISTRY_DELETE                      |
| 404        | TELEMETRY_REGISTRY_RENAME                      |
| 501        | TELEMETRY_ACCOUNT_ADD                          |
| 502        | TELEMETRY_ACCOUNT_DELETE                       |
| 503        | TELEMETRY_ACCOUNT_IMPERSONATE                  |
| 504        | TELEMETRY_ACCOUNT_MODIFY                       |
| 601        | TELEMETRY_INTERNET_OPEN                        |
| 602        | TELEMETRY_INTERNET_CONNECT                     |
| 603        | TELEMETRY_INTERNET_DOWNLOAD                    |
| 701        | TELEMETRY_MODIFIED_PROCESS_CREATE_REMOTETHREAD |
| 702        | TELEMETRY_MODIFIED_PROCESS_WRITE_MEMORY        |
| 703        | TELEMETRY_MODIFIED_PROCESS_WRITE_PROCESS       |
| 704        | TELEMETRY_MODIFIED_PROCESS_READ_PROCESS        |
| 705        | TELEMETRY_MODIFIED_PROCESS_WRITE_PROCESS_NAME  |
| 801        | TELEMETRY_WINDOWS_HOOK_SET                     |
| 901        | TELEMETRY_AMSI_EXECUTE                         |
| 1001       | TELEMETRY_MEMORY_MODIFY                        |
| 1002       | TELEMETRY_MEMORY_MODIFY_PERMISSION             |
| 1003       | TELEMETRY_MEMORY_READ                          |
| 1101       | TELEMETRY_BM_INVOKE                            |
| 1102       | TELEMETRY_BM_INVOKE_API                        |

## Mobile Activity Data
### eventId
| eventId | Data Field Mapping |
| ------- | ------------------ |
| 2       | TELEMETRY_FILE     |
| 7       | TELEMETRY_INTERNET |
| 15      | TELEMETRY_APP      |
| 16      | TELEMETRY_SYSTEM   |

### eventSubId
| eventSubId | Data Field Mapping                  |
| ---------- | ----------------------------------- |
| 101        | TELEMETRY_FILE_CREATE               |
| 102        | TELEMETRY_FILE_OPEN                 |
| 103        | TELEMETRY_FILE_DELETE               |
| 105        | TELEMETRY_FILE_COPY                 |
| 106        | TELEMETRY_FILE_MOVE                 |
| 601        | TELEMETRY_INTERNET_OPEN             |
| 602        | TELEMETRY_INTERNET_CONNECT          |
| 1201       | TELEMETRY_APP_START                 |
| 1202       | TELEMETRY_APP_STOP                  |
| 1203       | TELEMETRY_APP_INSTALL               |
| 1204       | TELEMETRY_APP_UNINSTALL             |
| 1301       | TELEMETRY_SYSTEM_PREF_EVENT_ENABLE  |
| 1302       | TELEMETRY_SYSTEM_PREF_EVENT_DISABLE |