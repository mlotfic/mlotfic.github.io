# project properties

## Eplan Project pages and page properties

**Project pages** are individual pages within a project that are used to organize the project in a logical and efficient manner. 

**Page properties** are properties that are assigned to a page that define its properties and settings. 

**Example:**

```
Project pages are the actual pages that contain the electrical design of a project. They are the building blocks of the project and are used to organize the project in a logical and efficient manner. 

Page properties are properties that are assigned to a page that define its properties and settings. 

Example:

Project name
Description 
Language
Project directory

```
## project properties categories

01. `Formats` - Defines formatting options for documentation and output layouts 
02. `All categories` - Displays all available project property categories
03. `Archive data` - Contains properties related to archived project information
04. `Customer` - Stores details about the customer for whom the project is created
05. `Data` - General project data and metadata fields
06. `End customer` - Information about the final recipient or end user of the project
07. `Parts` - Defines part-related data and component properties
08. `Revision` - Manages revision control and versioning information
09. `Settings` - Contains general project configuration and system settings
10. `Special` - Holds special or custom project properties for advanced use cases
11. `Thermal design` - Includes properties related to thermal calculations and design parameters

---

## 05. Data

- General project data and metadata fields

### important

|category | Property                                 | id     | value                                | Description                                                      |
|---------|------------------------------------------|--------|--------------------------------------|------------------------------------------------------------------|
| Data    | Project description                      | 1001   | Grinding machine                     | Defines the project’s main purpose or title                      |
| Data    | Job number                               | 1002   | 001                                  | Unique identifier for the project job                            |
| Data    | Commission                               | 1003   | EPLAN                                | Organization or entity commissioning the project                 |
| Data    | Company name                             | 1004   | EPLAN GmbH & Co. KG                  | Name of the company responsible for the project                  |
| Data    | Company address 1                        | 1005   | An der alten Ziegelei 2              | Primary company address line                                     |
| Data    | Company address 2                        | 1006   | D-40789 Monheim am Rhein / Germany   | Secondary company address line                                   |
| Data    | Project: Type                            | 1007   | Grinding machine, Type 1             | Specifies the type or classification of the project              |
| Data    | Place of installation                    | 1008   | Hall 17 / Section B                  | Location where the system or machine is installed                |
| Data    | Environmental consideration              | 1009   | None                                 | Notes any environmental factors considered in the project        |
| Data    | Manufacturing date                       | 1010   | 2016/2017                            | Indicates the manufacturing period of the system                 |
| Data    | Supplementary field [1]                  | 1011   | EPLAN sample project                 | Additional field for project metadata or notes                   |
| Data    | EPLAN Report control                     | 1012   | Individual                           | Defines report generation control settings                       |
| Data    | EPLAN PLC circuit                        | 1013   | 0,75 mm²                             | Specifies conductor cross-section for PLC circuits               |
| Data    | EPLAN Control line                       | 1014   | 1,5 mm²                              | Defines conductor size for control lines                         |
| Data    | EPLAN Protective wire                    | 1015   | 1,5 mm²                              | Defines conductor size for protective wires                      |
| Data    | EPLAN Main circuit                       | 1016   | 2,5 mm²                              | Defines conductor size for main circuits                         |
| Data    | EPLAN Type 4-fold terminal               | 1017   | Terminal blocks Phoenix UK           | Specifies terminal type and manufacturer for 4-fold terminals    |
| Data    | EPLAN Type 2-fold terminal               | 1018   | Terminal blocks Phoenix UK           | Specifies terminal type and manufacturer for 2-fold terminals    |
| Data    | EPLAN Protection class enclosure         | 1019   | IP43                                 | Defines enclosure protection rating                              |
| Data    | EPLAN Color enclosure                    | 1020   | RAL 9016                             | Specifies enclosure color according to RAL standard              |
| Data    | EPLAN Base enclosure                     | 1021   | RITTAL VX                            | Defines base enclosure type and manufacturer                     |
| Data    | EPLAN Enclosure                          | 1022   | RITTAL VX                            | Specifies enclosure model used in the project                    |
| Data    | EPLAN Special customer regulations       | 1023   | No                                   | Indicates if special customer requirements apply                 |
| Data    | EPLAN Control voltage                    | 1024   | 24 V DC                              | Defines control voltage level for the system                     |
| Data    | EPLAN Input lead                         | 1025   | NYM 5x6 mm²                          | Specifies input cable type and size                              |
| Data    | EPLAN Power supply                       | 1026   | 400 V 50 Hz 50 A                     | Defines power supply parameters for the system                   |

### others

| category| Property                                 | id     | value                                | Description                                                      |
|---------|------------------------------------------|--------|--------------------------------------|------------------------------------------------------------------|
| Data    | AutomationML GUID                        | 1027   |                                      | Unique identifier for AutomationML data exchange                 |
| Data    | AutomationML: Area                       | 1028   |                                      | Defines the AutomationML area within the project structure       |
| Data    | AutomationML: Building                   | 1029   |                                      | Specifies the building context for AutomationML integration      |
| Data    | AutomationML: Company                    | 1030   |                                      | Company information linked to AutomationML metadata              |
| Data    | AutomationML: Plant                      | 1031   |                                      | Defines the plant or facility associated with AutomationML data  |
| Data    | AutomationML: Works                      | 1032   |                                      | Specifies the works or production site for AutomationML mapping  |
| Data    | Control voltage                          | 1033   |                                      | Defines the control voltage level used in the project            |
| Data    | Customer code                            | 1034   |                                      | Unique code identifying the customer                             |
| Data    | Degree of protection                     | 1035   |                                      | Specifies the IP protection class for enclosures or devices      |
| Data    | Enclosures                               | 1036   |                                      | Defines enclosure types used in the project                      |
| Data    | Feed-in                                  | 1037   |                                      | Specifies feed-in points for electrical power or signals         |
| Data    | Input lead                               | 1038   |                                      | Defines input cable type and specifications                      |
| Data    | Location                                 | 1039   |                                      | Physical or logical location of the project or component         |
| Data    | Make                                     | 1040   |                                      | Manufacturer or brand of the equipment                           |
| Data    | Part features                            | 1041   |                                      | Defines specific part attributes or characteristics              |
| Data    | Project name (full)                      | 1042   |                                      | Full path and name of the project file                           |
| Data    | Project path                             | 1043   |                                      | Directory path where the project is stored                       |
| Data    | Project path (full)                      | 1044   |                                      | Complete file path including project name                        |
| Data    | Project: Template                        | 1045   |                                      | Template file used for project creation                          |
| Data    | Regulation                               | 1046   |                                      | Defines applicable standards or regulations                      |
| Data    | Supplementary field                      | 1047   |                                      | Additional metadata fields for user-defined project information  |
| Data    | User supplementary field 1               | 1048   |                                      | Custom user field for additional project data                    |
| Data    | User supplementary field 2               | 1049   |                                      | Second custom user field for project data                        |

---