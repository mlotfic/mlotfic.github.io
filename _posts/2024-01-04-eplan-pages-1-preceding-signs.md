---
layout: post
cover_color: #000000

keywords: 

title: "EPLAN Preceding Signs (IEC 81346)"

description: >- 
  **EPLAN Preceding Signs**

date: 2024-01-04 10:00:00 +0800
author: Mahmoud Lotfi
file_name: 2024-01-04-eplan-preceding-signs.md
categories: [EPLAN, preceding signs]
tags: [EPLAN, preceding signs]
pin: False
math: true
mermaid: true
comments: true
toc: true
render_with_liquid: false

image:
  path: /assets/img/posts/eplan.jpg
  alt: Eplan Preceding Signs (IEC 81346)
  lqip: data:image/webp;base64,UklGRjoAAABXRUJQVlA4IC4AAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
---

# Preceding signs

- Every identifier block is assigned particular preceding signs (prefixes).
- Except for the "Functional assignment" and "User defined" identifier blocks, the prefixes are pre-defined and cannot be changed.
- The following preceding signs can be used:
    1. "==" ("#")("≠") Functional assignment
    2. "=" Function designation
    3. "++" Installation site
    4. "+" Location designation
    5. "&" Document type
    6. "Free" User-defined.

## Functional assignment

- The "Functional assignment" identifier block represents the link between plants, technical facilities and devices.
- Possible prefixes in Eplan are "==" or "#" or "≠".

### Example

```cs

```

## Function designation

- The "Function designation" identifier block is used to identify plants, plant sections, and technical facilities.
- Possible prefix in Eplan is "=".

### Example

```cs

```

## Installation site

- The "Installation site" identifier block specifies the topographical location of devices or technical facilities, e.g., the building, hallway, room, etc.
- Possible preceding sign in Eplan is "++".

## Location designation

- The "Location designation" identifier block specifies the physical location of devices or technical facilities, such as enclosure, control panel, etc.
- Possible preceding sign in Eplan is "+".

### Higher-level function number

- The identifier block "Higher-level function number" is used to structure fluid power devices. This identifier is necessary if the project includes multiple higher-level functions.