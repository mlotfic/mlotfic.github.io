---
layout: post
cover_color: #000000

keywords: 

title: "EPLAN Path Variables"

description: >- 
  **EPLAN Path Variables**

date: 2024-01-03 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-01-03-eplan-path-variables.md
categories: [EPLAN, path variables]
tags: [EPLAN, path variables]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: Eplan Path Variables
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---


# List of Eplan Path Variables

Here are available EPLAN path variables: $(PROJPROP_<ID>)Project property. In order to identify such a path variable, the ID of the respective property is included in the name.

## software version information related path variables

|Path variable	              | Meaning                                                                                                         |
| :-------------------------- | :-------------------------------------------------------------------------------------------------------------- |
|$(BIN)	                      | A program directory generated on installation contains the program libraries (*.dll) of the individual modules. |
|$(CFG)	                      | A configuration directory generated on installation containing the xml files of the individual modules.         |
|$(CFG_COMPANY)	              | Configuration directory generated on installation, contains the company settings.                               |
|$(CFG_STATION)	              | Configuration directory generated on installation, contains the station settings.                               |
|$(CFG_USER)	                | Configuration directory generated on installation, contains the user settings.                                  |
|$(DOC)	                      | Project-specific directory for documents.                                                                       |
|$(EPLAN)	                    | An upper-level main directory generated on installation.                                                        |
|$(EPLAN_DATA)	              | A superior directory for master data, generated on installation.                                                |
|$(EPLAN_EXECUTABLE)	        | The directory to Eplan.exe.                                                                                     |
|$(ENVVAR_<Variable_Name>)    | OS environment variable.                                                                                        |
|$(EPLAN_VARIANT)             | Name of the started product variant.                                                                            |
|$(EPLAN_VERSION)             | Version number of the used Eplan.                                                                               |
|$(EPLAN_VERSION_SHORT)       | Main version number of the used Eplan.                                                                          |

---

## master data related path variables

|Path variable	              | Meaning                                                                                                         |
| :-------------------------- | :-------------------------------------------------------------------------------------------------------------- |
|$(MD_DOCUMENTS)              | The directory for documents defined under Options > Settings > User > Management > Directories.                 |
|$(MD_DXFDWG)                 | The directory for DXF / DWG files defined under Options > Settings > User >Management > Directories.            |
|$(MD_FCTDEFS)                | The directory for function definitions available under Options > Settings >User > Management > Directories.     |
|$(MD_FORMS)                  | The directory for forms defined under Options > Settings > User > Management > Directories.                     |
|$(MD_FRAMES)                 | The directory for plot frames defined under Options > Settings > User >Management > Directories.                |
|$(MD_IMG)                    | The directory for images defined under Options > Settings > User > Management > Directories.                    |
|$(MD_JOBFILESERVER)          | Directory for the Batch Server files.                                                                           |
|$(MD_MACROS)                 | The directory for macros and outlines defined under Options > Settings >User > Management > Directories.        |
|$(MD_MECHANICALMODELS)       | The directory for mechanical models defined under Options > Settings >User > Management > Directories.          |
|$(MD_PARTS)                  | The directory for parts defined under Options > Settings > User >Management > Directories.                      |
|$(MD_PROJECTS)               | The directory for projects defined under Options > Settings > User >Management > Directories.                   |
|$(MD_SCHEME)                 | The directory for schemes defined under Options > Settings > User >Management > Directories.                    |
|$(MD_SCRIPTS)                | The directory for scripts defined under Options > Settings > User >Management > Directories.                    |
|$(MD_SYMBOLS)                | The directory for symbols defined under Options > Settings > User >Management > Directories.                    |
|$(MD_TEMPLATES)              | The directory for templates defined under Options > Settings > User >Management > Directories.                  |
|$(MD_TRANSLATE)              | The directory for translation files defined under Options > Settings >User > Management > Directories.          |
|$(MD_XML)                    | The directory for XML files defined under Options > Settings > User > Management > Directories.                 |

---

## Project related path variables

|Path variable	              | Meaning                                                                                                         |
| :-------------------------- | :-------------------------------------------------------------------------------------------------------------- |
|$(P)                         | Full project directory of the currently selected project.                                                       |
|$(PROJECTNAME)               | Project name of the currently selected project, without directory path and file extension.                      |
|$(PROJECTPATH)               | Full project directory of the currently selected project.                                                       |
|$(RIGHTS_DB_PATH)            | Directory of the user rights database.                                                                          |
|$(TMP)                       | The directory used by the operating system for temporary files.                                                 |
|$(IMG)                       | Project-specific directory for images.                                                                          |
|$(LOCALDATE)                 | Current local date.                                                                                             |
|$(LOCALTIME)                 | Current local time.                                                                                             |

---

#### ➲ **Next post:** [Eplan Pages](https://mlotfic.github.io/posts/eplan-page-1-intro)

> ⛓️‍💥 Mahmoud Lotfi
