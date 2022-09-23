# Preview
- Please be noted that these documents is still in preview stage and does not guarantee any backward compatibility.

# Background
- These documents provides Trend Micro Vision One log schema detail.

# User scenario
- For now, these documents only try to support the following use cases:
    1. Support vision one search app UI usage.

# Log Mapping
| Log                    |  Document                |
|------------------------|--------------------------|
| Endpoint Activity Data |  doc/telemetry.yaml      |
| Detections             |  doc/detection.yaml      |
| Message Activity Data  |  doc/messaging.yaml      |
| Cloud Activity Data    |  doc/cloudtrail.yaml     |

# Property Description
| Property              |  Description                                  |
|-----------------------|-----------------------------------------------|
| Name                  |  Field name of log                            |
| ProductCode           |  Products which sends data to this field      |
| Description_EN        |  Description of this field                    |
| Sample                |  Sample value of these field                  |
| DL_Searchable         |  If log is searchable by this field           |
| DL_Type               |  Data type of this field                      |

# ProductCode Mapping 
| Code |  Product                                               |
|------|--------------------------------------------------------|
| pdi  | Deep Discovery Inspector                               |
| sds  | Trend Micro Cloud One - Endpoint & Workload Security   |
| xes  | Endpoint Sensor                                        |
| sao  | Apex One as a Service                                  |
| pds  | Deep Security Software                                 |
| sca  | Cloud App Security                                     |
| ptp  | TippingPoint Security Management System                |
| stp  | Trend Micro Cloud One - Network Security               |
| sig  | SASE Secure Web Gateway (Internet Access Gateway)      |
| sws  | Trend Micro Web Security                               |
| sem  | Trend Micro Email Security                             |
